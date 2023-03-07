### Image 넣기

ex3_img 패키지 생성

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
