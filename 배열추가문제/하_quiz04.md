  ### 배열추가문제 Quiz04 (하)
        하-4 : (3)번에서 생성된 배열에 다음 기능을 추가하세요.
        ㄱ. 0 ~ n-1 까지의 숫자를 배열에 순서대로 저장하세요.
        입력 : 3  ===> 결과 : [0, 1, 2]
        입력 : 5  ===> 결과 : [0, 1, 2, 3, 4]
        ㄴ. 배열의 가장 마지막 원소부터 0번 원소까지 역순으로 출력하세요.
        ㄷ. for문을 사용하여 배열에 저장된 실제 원소들을 역순으로 재배치 하세요. (난이도 중)
        sysout(배열[0]); // 3
        sysout(배열[1]); // 2
        sysout(배열[2]); // 1
        sysout(배열[3]); // 0
        (for문을 쓰되 for문의 실행 횟수가 n/2이 되도록하세요. 
        (5칸 배열이면 2회만에, 10칸 배열이면 5회만에 for문이 종료되도록)
```java
package day08.배열추가문제;

import java.util.Scanner;

public class Quiz하04 {
	public static void main(String[] args) {
		
		Scanner sc = new Scanner(System.in);
		
		System.out.println("칸 개수 입력: ");
		int aa = sc.nextInt();
		
		int [] arr = new int [aa];
		
		for (int i = 0; i < arr.length; ++i) {
		  arr[i] =i;  //입력 : 5  ===> 결과 : [0, 1, 2, 3, 4]
		}
			   
		System.out.print("결과 : [ ");
		for (int i = 0; i < arr.length; ++i) {
			if(i<(arr.length-1)) {
				System.out.print(arr[i] + ", "); //마지막에 {0, 0, 0,} ,가 출력되기 때문에  arr.length-1로함
													// 그래야 마지막에 , 가 없음
				continue;
			} 
			
			System.out.println(arr[i]+" ]");
		}
		System.out.print("역순 : [ "); 
		for (int i = arr.length - 1; i >= 0; --i) {
			if (i > 0) {
				System.out.print(arr[i] + ", ");
				continue;
			}
			System.out.println(arr[i] + " ]");
			}
		
		for (int i = 0; i < (arr.length)/2 ; i++) {
	         int max = arr.length- i -1; 
	         int temp = 0;
	         temp = arr[i];
	         arr[i] = arr[max];
	         arr[max] = temp;
	     }
	     for (int i = 0; i < arr.length; i++) {
	         System.out.print("역순: " + arr[i]);
	     }
	}
	        	        
	}
  ```
