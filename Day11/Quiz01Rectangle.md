### Rectangle Quiz 출력

        메인 클래스 : Quiz01
          - Rectangle 객체 1개 생성 
          - JOptionPane을 사용하여 밑변, 높이를 입력 받고, 
        Rectangle 객체에 저장 (setData() 사용)
          - 이 사각형 객체의 넓이와 둘레를 메소드를 사용하여 출력 (getArea(), getCircum())
```java
package day11.quiz.메소드;

import javax.swing.JOptionPane;

public class day11quiz01 {
	public static void main(String[] args) {
		Rectangle cle = new Rectangle();
		int b = Integer.parseInt(JOptionPane.showInputDialog(null, "밑변을 입력하세요."));
		int h = Integer.parseInt(JOptionPane.showInputDialog(null, "높이를 입력하세요."));
		cle.setData(b, h); //setData에 저장
		
		JOptionPane.showMessageDialog(null, "넓이: " +  cle.getArea() 
											+ "\n둘레: " + cle.getCircum());		
	}
}
```
