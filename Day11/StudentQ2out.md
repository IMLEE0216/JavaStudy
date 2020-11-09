### Quiz02 Student 출력

       메인 클래스 : Quiz03
       4명의 학생 객체를 배열로 선언하고 
       반복문을 사용하여 학생들의 이름, 국, 영, 수를 입력 받음
       입력이 끝나면 모든 학생의 정보를 출력
```java
package day11.quiz.메서드;

import java.util.Scanner;


public class day11quiz02 {
	public static void main(String[] args) {
		Student [] st = new Student [4]; //0,1,2,3
		Scanner sc = new Scanner(System.in);
		
		for (int i = 0; i < st.length; i++) {
			st[i] = new Student();
			System.out.println("이름을 입력하세요.");
			String n = sc.next();
			System.out.println("국어 점수: ");
			int k = sc.nextInt();
			System.out.println("영어 점수: ");
			int e = sc.nextInt();
			System.out.println("수학 점수: ");
			int m = sc.nextInt();
			
			st[i].setData(n, k, e, m);
			st[i].setMean();
			st[i].setGrade();
			
			}
			 for (int i = 0; i <st.length; i++) {
				 System.out.println("=================");
				 st[i].printData();
				 
			 }
	}
}
```
