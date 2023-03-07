### 프레임 : JFrame

#### JFrame의 생성자
|생성자|설명|
|---|---|
|JFrame()|보이지 않는 JFrame을 생성한다.|
|JFrame(String title)|타이틀을 지정한 보이지 않는 JFrame을 생성한다.|
- 프레임을 생성했을때는 기본적으로 화면에 보이지 않는다.
- 화면에 프레임을 표시하고자 할 때는 위치와크기, 화면에 표시할 것인지에 대한 여부를 지정해줘야 한다.
- setSize(int width, int height) : 프레임의 크기 지정
- setLocation(int x, int y) : 프레임이 보일 좌표설정
- setVisible(boolean value) : 화면 표시 여부 설정

#### JFrame의 주요 메서드
|메서드|설명|
|---|---|
|void add(Component c)|지정된 컴포넌트를 패널에 추가한다.|
|JMenuBar getJMenuBar()|지정된 JMenuBar를 구한다.|
|void pack()|프레임에 부속된 컴포넌트들의 크기에 맞게 프레임의 크기를 조절한다.|
|void remove(Component c)|프레임에 지정된 컴포넌트를 제거한다.|
|void setDefaultCloseOperation(int operation)|사용자가 JFrame을 닫을 때 기본적으로 어떤 작업을 할지 정한다. operation은 하기 표 참조|
|void setIconImage(Icon image)|프레임이 최소화 되었을 떄의 아이콘을 지정한다.|
|void setLayout(LayoutManager layout)|배치관리자를 지정한다(디폴트는 BoarderLayout 배치관리자이다.)|
|void setLocation(int x, int y)|프레임의 x좌표, y좌표를 지정한다.|
|void setResizable(boolean value)|프레임의 크기 변경 허용 여부를 지정한다.|
|void setSize(int width, int height)|프레임의 크기를 설정한다.|
|void setJMenuBar(JMenubar menubar)|	현재 프레임에 메뉴바를 붙인다.|

#### setDefaultCloseOperation(int operation) 메서드의 operation 값
|상수값|설명|
|---|---|
|EXIT_ON_CLOSE|닫기 단추를 누르면 창을 화면에서 사라지게 하고, 메모리에도 제거된다.|
|DO_NOTHING_ON_CLOSE|닫기 단추를 비활성화 시킨다. 이 상수는 JFrame에서 제공하는 적업을 하지 않고 등록된 WindowListener의 windowClosing()메서드에서 원하는 작업을 하고 싶을 때 사용한다.|
|HIDE_ON_CLOSE|등록된 WindowListener의 메서드를 호출하기 전에 자동적으로 JFrame을 닫는다. 화면에서 창을 숨겨준다.|
|DISPOSE_ON_CLOSE|닫기 단추를 누르면 창을 화면에서 사라지게 하고, 메모리에는 제거되지 않는다.|




ex1_JFrame 패키지 생성

#### Ex1_JFrame 클래스 생성
```java
package test;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.URL;

import javax.swing.JFrame;

public class JFrameTest extends JFrame {
	
	public JFrameTest() {
		super("제목");
		setBounds(300,300,300,200);
		setVisible(true);
	}
	
	
	
	public static void main(String[] args) {
		JFrameTest f = new JFrameTest();
		f.setDefaultCloseOperation(EXIT_ON_CLOSE);
	}
}
```


### 패널 : JPanel
- JPanel은 JFrame에 붙히는 중간 컨테이너 역할을 한다.
- 화면이 복잡한 형태인 경우 요소를 그룹별로 묶어서 표현할 수 있는데, 이러한 경우 JPanel에다 묶어서 Frame에다 붙힐 수 있다.

#### JPanel의 생성자
|생성자|설명|
|---|---|
|JPanel()|레이아웃 매니저가 FlowLayout인 JPanel을 생성한다|
|JPanel(LayoutManger layout)|레이아웃 매니저가 layout인 JPanel을 생성한다.|

#### 배치관리자
- FlowLayout : 왼쪽에서 오른쪽으로 배치, 오른쪽 공간이 없으면 아래로 배치
- BorderLayout : 동,서,남,북,중앙 5개의 영역으로 나눠준다.
- GridLayout : 2차원 표 모양으로서 n X n으로 설정해주며 왼쪽에서 오른쪽, 위에서 아래 순으로 배치
- CardLayout : 컴포넌트를 포개어 배치
- Null : 레이아웃을 쓰지 않고 각 컴포넌트마다 수동으로 위치를 설정

#### JPanel의 주요 메서드
|메서드|설명|
|---|---|
|void add(Component c)|지정된 컴포넌트를 패널에 추가한다.|
|void remove(Component c)|패널에 지정된 컴포넌트를 제거한다.|
|void setLayout(LayoutManager layout)|배치관리자를 지정한다(디폴트는 FlowLayout 배치관리자이다.)|
|void setLocation(int x, int y)|패널의 x좌표, y좌표를 지정한다.|
|void setSize(int width, int height)|패널의 크기를 설정한다.|
|void setToolTipText(String text)|패널의 빈곳에 마우스를 올려놓으면 툴팁을 표시한다.|

#### Ex2_JPanel 클래스 생성

```java
package test;

import java.awt.Color;
import java.awt.FlowLayout;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;

public class Test extends JFrame {
	
	public Test() {
        super("FlowLayout 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        JPanel p1 = new JPanel();
        p1.setBackground(Color.YELLOW);
        p1.setLayout(new FlowLayout());
        //p1.setLayout(new GridLayout(3,2));
	//p1.setLayout(new BorderLayout());
        p1.add(new JButton("1"));
        p1.add(new JButton("2"));
        p1.add(new JButton("3"));
        p1.add(new JButton("4"));
        p1.add(new JButton("5"));
        
        this.add(p1);
        setSize(300, 200);
        setVisible(true);
    }
    
    public static void main(String[] args) {
    	Test frame = new Test();
    	
    }
}

```












### Image 넣기

ex2_img 패키지 생성

src에서 폴더생성 images 구글에서 심슨 이미지 검색<br>
웹개발 폴더에 저장 복사해서 images 폴더에 저장 작은크기의 이미지도 같은 방법으로<br>
버튼을 눌렀을 때 바뀔 이미지를 한 장 더 구한다.<br>

#### ImgText 클래스 생성
```java
public class ImgText {
	static boolean change = true;

	public static void main(String[] args) {
		Frame f = new Frame(“이미지”);
		f.setBounds(500,300,500,500);
		f.setLayout(null);
		이미지는 프레임에 맞게 늘릴수 없고 꽉 채우고 싶으면 맞는 사진을 구해야 함

		스윙이라고 해서 좀 더 발전된 클래스에서 제공하는 기능

		ImageIcon back = new ImageIcon(“src/images/s.png”);
		JLabel jl_back = new JLabel(back);
		jl_back.setBounds(0,0,500,500);

		ImageIcon btnIcon = new ImageIcon(“src/images/ic.png”);
		JButton jb = new JButton(btnIcon);
		jb.setBounds(20,40,106,106);

		ImageIcon back2 = new ImageIcon(“src/images/s2.jpg”);
		
		jb.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				if(change == true){
					//배경으로 사용중인 JLabel의 아이콘을 back2로 변경
					jl_back.setIcon(back2);
					f.repaint();//현재 프레임의 내용을 갱신
				} else if(change == false){
					//배경으로 사용중인 JLabel의 아이콘을 backㅎ로 변경
					jl_back.setIcon(back);
					f.repaint();//현재 프레임의 내용을 갱신
				}
				
			}
		});

		//버튼객체인 jb를 먼저 add해줘야 배경보다 위쪽에 보여진다.
		f.add(jb);
		f.add(jl_back);
		

		frame.setVisible(true);

		f.addWindowListener(new WindowAdapter() {
			@Override
			public void windowClosing(WindowEvent e) {
				System.exit(0);
			}
		});
		
	}
}
```
