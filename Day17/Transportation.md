### Transportation Interface

```java
public interface Transportation {	
	int getCharge(int age, int km);
}
```
### Transportation Class
```java
package day17.basic.추상화;

import java.util.Scanner;

class Bus implements Transportation{
	@Override
	public int getCharge(int age, int km) {
		int normal = 1000;
		double total = km > 10? (int)(km/10*100) + normal : normal;
		if (age < 20) {
			total = total * 0.8;
		}
		System.out.println("나이: " + age+"살\n"+ "이동거리:" + km + "km\n"+ "총 가격: " + (int)total+ "원");
		return (int)total;
	}
	}
class Taxi implements Transportation{
	@Override
	public int getCharge(int age, int km) {
		int normal = 4000;
		int total = km > 10? (int)(km-10)*100 + normal : normal;
		System.out.println("나이: " + age+"살\n"+ "이동거리:" + km + "km\n"+ "총 가격: " + (int)total+ "원");
		return total;
	}
	}
class Subway implements Transportation{
	@Override
	public int getCharge(int age, int km) {
		int normal = age < 20? 720: 1250;
		int total = age < 20? ((int)km/10)*50 + normal: (int)km/10*100 + normal;
		System.out.println("나이: " + age+"살\n"+ "이동거리:" + km + "km\n"+ "총 가격: " + (int)total+ "원");
		return total;
	}
	}
class Train implements Transportation{
	@Override
	public int getCharge(int age, int km) {
		int normal = 15000;
		double total = km >= 30? (int)(km-30)/30*1000 + normal : normal;
		if (age < 20) {
			total = total * 0.5;
		}
		System.out.println("나이: " + age+"살\n"+ "이동거리:" + km + "km\n"+ "총 가격: " + (int)total+ "원");
		return (int)total;
	}
	}
```
### Transportation Main

      Quiz 클래스 : 메인
	    원하는 교통수단(버스, 전철, 택시, 기차)과 나이, 거리(km)를 입력 받고
	    요금을 출력하세요.
      
```java  
public class Quiz01Transprotation {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		Transportation [] vehicle = new Transportation[4];
		vehicle[0] = new Bus();
		vehicle[1] = new Taxi();
		vehicle[2] = new Subway();
		vehicle[3] = new Train();
		
		System.out.println("이용하실 교통수단의 번호를 입력하세요.\n 1번.버스 \n 2번.택시 \n 3번.지하철 \n 4번.기차");
		int num=sc.nextInt();
		loop: switch (num) {
		case 1:
			System.out.println("버스를 타고갑니다.");
			System.out.println("나이와 이동거리를 입력하세요.");
			vehicle[0].getCharge(sc.nextInt(), sc.nextInt());
			break loop;
			
		case 2:
			System.out.println("택시를 타고 갑니다.");
			System.out.println("나이와 이동거리를 입력하세요.");
			vehicle[1].getCharge(sc.nextInt(), sc.nextInt());
			break loop;
			
		case 3:
			System.out.println("지하철을 타고 갑니다.");
			System.out.println("나이와 이동거리를 입력하세요.");
			vehicle[2].getCharge(sc.nextInt(), sc.nextInt());
			break loop;
			
		case 4:
			System.out.println("기차를 타고 갑니다.");
			System.out.println("나이와 이동거리를 입력하세요.");
			vehicle[3].getCharge(sc.nextInt(), sc.nextInt());
			break loop;
		}
	}
}
```

###결과

       이용하실 교통수단의 번호를 입력하세요.
        1번.버스 
        2번.택시 
        3번.지하철 
        4번.기차
        4
       기차를 타고 갑니다.
       나이와 이동거리를 입력하세요.
       18
       120
       나이: 18살
       이동거리:120km
       총 가격: 9000원


### 문제1

	객체지향 설계원칙 4가지 조사하기 (훑어만 보기)
 	SOLID  -S: 단일 책임 원칙(SRP)
			O: 개방-폐쇄 원칙(OCP)
			L: 리스코프 치환 원칙(LSP)
			I: 인터페이스 분리 원칙(ISP)
			D: 의존 역전 원칙(DIP)
 	YAGNI - You Ain't Gonna Need it  : 정말 필요할 때까지 그 기능을 만들지 말라.  component 갯수를  줄여서 복잡도를 줄이는 전략 
 	KISS - Keep it simple, stupid. : 단순하게 하라.
 	DRY - Don't Repeat Yourself  : 똑같은 일을 두번하지 않는다. 중복되는 함수나 코드는 하나의 공통의 콤포넌트에 넣고 사용한다. 
					큰 시스템을 여러 조각으로 나누고 서로 참조한다.
 					관리 가능한 component를 나눠서 복잡도를 줄이는 전략
									
									
### 문제2
		1. 클래스간의 다중상속
			class B
			class C
			class A extends B, C 

		2. 인터페이스간의 다중상속(extends)
			interface B
			interface C
			interface A extends B, C

		3. 복수의 인터페이스를 구현(implement)
			interface B
			interface C	
			class A implements B, C
			
	2-1.  1은 불가능하지만  2,3은 가능하다. 왜 허용해둔걸까? 개인의 생각을 적어주세요 
	너무 어렵네요.ㅠㅠ
	1번은 같은 이름의 메서드이면 어디 클래스에 적용해야 하는지 몰라서 헷갈린다 라는데...
	2,3 번은 다형성을 위해서 허용한 것 이긴한데...
	구체적인 이유는 모르겠네요...ㅠㅠ단지 추상적 메서드라서 A가 B와 C의 추상적메서드를 모두 구현하기 때문

	2.2 2, 3에서도 특정한 경우 오류가 생긴다. 어떤 경우에 오류가 생길까? 
	A에서 B와 C의 추상 메서드를 모두 override하지 않았을때?!
