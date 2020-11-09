### 메소드 Quiz01 (Rectangle)


        클래스 : Rectangle
        - 필드(멤버변수) : base, height
        - 메소드 
        1) setData() : 두 정수를 인자값으로 받아, 객체의 base, height에 각각 저장
        2) getArea() : 넓이를 리턴
        3) getCircum() : 둘레를 리턴
```java	
package day11.quiz.메서드;

public class Rectangle {
	int base;
	int height;
	
	void setData(int b, int h) { //밑변, 높이
		base = b;
		height = h;	
	} 
	
	double getArea() {
		return base*height;
	}
	double getCircum() {
		return (base+height)*2;
	}
	
}
```
