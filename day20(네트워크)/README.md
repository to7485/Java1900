## NetWork

### http통신과 socket통신의 차이점

-단방향 통신인 http통신
http통신은 Client의 요청(Request)이 있을 때만 서버가 응답(Response)하여 해당 정보를 전송하고 곧바로 연결을 종료하는 방식입니다.<br>
Client가 요청을 보내는 경우에만 Server가 응답하는 단방향 통신으로 반대로 Server가 Client에게 요청을 보낼수는 없습니다.<br>

-양방향 통신인 Socket통신
Server와 Client가 특정 Port를 통해 실시간으로 양방향 통신을 하는 방식입니다.<br>
Http통신과는 다르게 Server와 Client가 Port를 통해 연결되어 있어서 실시간으로 양방향 통신을 할 수 잇습니다.<br>
Streaming이나 실시간 채팅, 게임 등과 같이 즉각적으로 정보를 주고받는 경우에 사용됩니다.<br>

Socket통신의 규칙
1. 먼저 기다리는 측을 Server라고 하며, Server에서는 Port를 열고 Client의 접속을 기다립니다.
2. 그리고 접속을 하는 측을 Client라고 하며, Server의 IP와 Port에 접속하여 통신이 연결됩니다.
3. Server와 Client 간의 통신은 Send, Receive의 형태로 주고받습니다.
4. 그리고 통신이 끝나면 close()로 접속을 끊습니다.

chat 패키지 생성

#### MyServer 클래스 생성
```
package chat;

import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

public class MyServer extends Thread{
	
	ServerSocket ss;
	
	public MyServer() {
		try {
			//서버소켓을 생성시에 서비스 포트번호를 지정한다.
			//물론 클라이언트가 접속할 때 필요하다.
			//서비스 포트번호의 범위는 약 2000번 이후의 번호를 사용
			ss = new ServerSocket(3000);
			//서버가 준비되었다.
			
			System.out.println("서버 완료!");
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	//스레드가 해야 할 일들...
	@Override
	public void run() {
		// 무한반복 속에서 접속자들을 항상 받아들인다.
		while(true) {
			try {
				Socket s = ss.accept(); //접속자를 받아들인다.
				//접속자가 올 때 까지 아래 내용을 수행하지 않고 대기상태에 빠진다.
				
				//위에서 지정한 포트로 접속한 클라이언트의 ip주소를 가져온다.
				String ip = s.getInetAddress().getHostAddress();
				System.out.println(ip + "님 왔다 감!");
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} 
		}
	}
	
	public static void main(String[] args) {
		//프로그램의 시작!
		MyServer ms = new MyServer();
		ms.start();
		
		//new MyServer().start();
		//현재 객체가 Thread로부터 상속 받았으므로
		//자신이 곧 스레드다.
		//그래서 생성하자마자 start()호출하여 Thread가 시작하도록 했다.
	}
}
```

MyServer 코드에서는  ServerSocket과 Socket 두가지 소켓을 볼 수 있습니다.<br>
서버소켓은 말 그대로 서버 프로그램에서 사용하는 소켓으로 ServerSocket 객체를 생성하여 클라이언트가 연결해오는 것을 기다립니다.<br>
클라이언트가 연결해 올 때 마다 요청은 큐(Request Queue)에 쌓이고, 각각의 클라이언트에 연결해 accept() 함으로써 요청을 큐에서 꺼내고 Socket객체가 리턴됩니다.<br>

이렇게 리턴되는 Socket을 활용하여 클라이언트와 데이터를 주고받으며, 예시와 같은 환경에서는 Socket을 생성한 스레드에 주어서 클라이언트와 데이터를 주고 받습니다.<br>
 
서버를 열고 클라이언트가 접속하는 프로그램을 만들어보자<br>

message 패키지 생성

#### MyServer 클래스 생성
```java

package message;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.ServerSocket;
import java.net.Socket;

public class MyServer extends Thread {
ServerSocket ss;
	
	public MyServer(){
		try {
			ss = new ServerSocket(3001);
			System.out.println("서버 시작!");
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
	
	public static void main(String[] args) {
		// 프로그램의 시작!
		new MyServer().start();
	}

	@Override
	public void run() {
		// thread가 해야할 일
		// (접속자를 받고, 바로 문자열을 받아낸다.
		//   그 문자열을 ip와 함께 화면에 출력! )
		while(true){
			try {
				Socket s = ss.accept(); // 접속자가 발생할 때까지 
							// 대기한다.
				// 클라이언트는 접속하자마자 문자열을 보내기 때문에
				// 여기서는 문자열을 받아야 한다.
				BufferedReader reader = 
					new BufferedReader(new InputStreamReader(s.getInputStream()));
				String msg = reader.readLine();//접속자가보낸 메세지								
				String ip = s.getInetAddress().getHostAddress();
				
				System.out.println(ip+" : "+msg);
				
			  } catch (Exception e) {
				  // TODO: handle exception
			  }
		}
	}
}
```
버퍼(buffer)
- 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는
  임시 메모리영역
- 입출력 속도 향상을 위해 버퍼 사용(빠른 이유는 아래 사진으로 설명)
- 버퍼를 이용한 입력( Buffered Reader)
- 버퍼를 이용한 출력( Buffered Writer)

![image](https://user-images.githubusercontent.com/54658614/226521287-18ecb07a-124b-443c-ae75-4ac5c2a37742.png)

#### MyClient 클래스 생성
```java
package message;

import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;

public class MyClient {
	public static void main(String[] args) {
		// 프로그램 시작
		
				System.out.println("입력:");
				Scanner scan = new Scanner(System.in);
				String msg = scan.nextLine(); 
				
				if(msg != null && msg.trim().length() > 0){
					Socket s = null;
					try {
						//서버의 아이피와 포트
						s = new Socket("192.168.200.102", 3001);
						// 서버 접속!!
						
						// 문자열을 서버로 보내기 위해 스트림 준비
						PrintWriter out = 
							new PrintWriter(s.getOutputStream());
						
						// 서버로 문자열 보내기
						out.write(msg);
						
						// 스트림에 적재한 내용을 비워라
						out.flush();
						
						if(out != null)
							out.close(); // 스트림 닫기
						
					} catch (Exception e) {
						// TODO: handle exception
					} finally {
						try {
							if(s != null)
								s.close(); // 소켓 닫기
								
						} catch (Exception e2) {
							// TODO: handle exception
						}
					}
			}
	}
}

```

둘 이상의 클라이언트가 접속하고<br>
클라이언트 간의 문자전달도 가능한 구조의 서버프로그램을 만들어보자.

#### ChatServer클래스 생성
```java
public class ChatServer extends Thread{
	ServerSocket ss;
	///////////////////////////////////////////////////
	ArrayList<CopyClient> list; //복사본 클라이언트를 담을 리스트를 준비
	//////////////////////////////////////////////////추가

	public ChatServer() {
		try {
			//////////////////////////////////////////////////
			list = new ArrayList<CopyClient>();//리스트 생성
			///////////////////////////////////////////////////
			ss = new ServerSocket(3200);
			// ServerSocket이 생성되었다는 이유만으로
			// 서버의 기능이 완료된 것이다.
			System.out.println("서버 시작!");

		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}	
	}

	public static void main(String[] args) {
		new ChatServer().start();
	}

	@Override
	public void run() {
		// 접속자를 기다린다.
		while(true){
			try {
				Socket s = ss.accept();
				String ip = s.getInetAddress().getHostAddress();
				System.out.println(ip + "님 접속");
				
				
				////////////////////////////////////////////
				CopyClient cc = new CopyClient(s, this);
				list.add(cc);
				cc.start();// 클라이언트의 복사본의 스레드 구동!!
				//이렇게 해야 copy클라이언트의 스레드에서
				//inputStream을 통해 클라이언트로부터 넘어온 값을 
				//처리할 수 있다.
				////////////////////////////////////////////

			} catch (Exception e) {
				// TODO: handle exception
			}
		}
	}
	
	////////////////////////////////////////////////////////////////////////////
	public void sendMessage(String msg){
		// 접속자들은 CopyClient로 만들어져서 ArrayList에
		// 모두 저장된 상태다.
		try {
			for(CopyClient cc : list){
				cc.out.println(msg);//서버의 접속자들에게 메세지 전달!
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
	
	public void removeClient(CopyClient cc){
		list.remove(cc);// 인자로 전달된 CopyClient객체를
				// ArrayList에서 삭제!!
		sendMessage("☆★☆★"+cc.ip+"님 퇴장!☆★☆★");
		//위는 남아있는 구성원들에게 퇴장메세지 전달!
	}
	///////////////////////////////////////////////////////////////////
}

```
#### ChatClient 클래스 정의
```java
public class ChatClient extends JFrame implements Runnable{

	// 화면 구성
	// 클라이언트에서 값을 보내고 받는걸 조금 쉽게 확인하기 위해서
	// 만든 Frame이므로 외울 필요없다. 일단 따라서 쓰고 보내는버튼(send_bt)과
	// 보여지는 화면(area)가 뭔지만 알고가자. 실전에서 jFrame안쓴다.
	JTextArea area;//메시지를 화면에 출력하는 공간
	JTextField input;
	JButton send_bt;//메시지 전송버튼
	JPanel south_p;

	// 서버 접속을 위한 객체
	Socket s;
	BufferedReader in;
	PrintWriter out;
	Thread t;

	public ChatClient(){
		area = new JTextArea();
		this.add(area);

		// BorderLayout배치관리자로 지전된 JPanel 생성
		south_p = new JPanel(new BorderLayout());
		south_p.add(input = new JTextField());// 패널객체의 가운데 추가
		south_p.add(send_bt = new JButton("보내기"),
				BorderLayout.EAST);

		this.add(south_p, BorderLayout.SOUTH);

		// 이벤트 감지자 등록
		this.addWindowListener(new WindowAdapter() {

			@Override
			public void windowClosing(WindowEvent e) {
				// 종료하기 전에 서버 접속 해제
				// 종료 메세지를 보낸다.(서버의 스레드를 소멸시키기 위함이다.)
				out.println("xx:~X");//종료시 xx:~X라는 메시지 전달
				// 위의 메세지가 서버로 갔다가 다시
				// 스레드 쪽으로 돌아온다.
			}
		});

		send_bt.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent arg0) {
				sendData();//서버로 메시지를 전달하기 위한 메서드			
			}
		});

		setBounds(100, 100, 400, 500);
		setVisible(true);

		connected(); // 서버 접속

		//서버로부터 전달되는 메세지를 감지하여 받는 스레드 생성
		t = new Thread(this);
		t.start();
	}

	private void connected(){
		try {		
			// 서버 접속
			s = new Socket("192.168.10.244", 3200);
			in = new BufferedReader(new InputStreamReader(
					s.getInputStream()));
			out = new PrintWriter(s.getOutputStream(), true);
		} catch (Exception e) {
			// TODO: handle exception
		}
	}

	public static void main(String[] args) {
		new ChatClient();
	}

	@Override
	public void run() {
		// 서버로부터 전달되는 메세지를 기다렸다가
		// 메세지가 도착하면 화면에 출력
		while(true){
			try {
				String msg = in.readLine();// 대기상태
				if(msg.equals("xx:~X"))		
					break;

				if(msg != null)
					area.append(msg+"\r\n");

			} catch (Exception e) {
				// TODO: handle exception
			}
		}
		closed();//열려있는 스트림을 닫는 메서드
		System.exit(0); // 프로그램 종료!!
	}

	private void sendData(){
		String msg = input.getText().trim();
		if(msg.length() > 0){
			// 한글자라도 입력했을 때 서버로 보내기
			out.println(msg);
		}
		input.setText("");//청소!!
	}

	private void closed(){
		try {
			if(out != null)
				out.close();
			if(in != null)
				in.close();
			if(s != null)
				s.close();
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
}
```
#### CopyClient클래스 생성하기
```java
public class CopyClient extends Thread{
	Socket s;
	BufferedReader in;
	PrintWriter out;
	ChatServer server;
	String ip;
	
	public CopyClient(Socket s, ChatServer cs){
		this.s = s;
		this.server = cs;
		
		try {
			out = new PrintWriter(s.getOutputStream(), true);
			in = new BufferedReader(
					new InputStreamReader(s.getInputStream()));
			ip = s.getInetAddress().getHostAddress();
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
	
	@Override
	public void run() {
		while(true){
			try {
				String msg = in.readLine();
				if(msg.equals("xx:~X")){
					out.println("xx:~X");
					
					//////////////////////////////////
					server.removeClient(this);
					//////////////////////////////////
					break;
				}

				////////////////////////////////////////
				server.sendMessage(ip+" : "+msg);
				////////////////////////////////////////
			} catch (Exception e) {
				// TODO: handle exception
			}
		}
	}
}
```

