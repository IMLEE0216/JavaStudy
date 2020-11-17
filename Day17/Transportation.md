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
