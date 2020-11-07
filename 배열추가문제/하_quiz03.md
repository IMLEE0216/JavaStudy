### 배열추가Quiz03 (하)
        
하-3 : 사용자에게 배열의 칸 개수를 입력 받고, 해당 정수의 크기만큼 정수형 배열을 생성하세요.

입력 : 3  ===> 결과 : [ 0, 0, 0 ] 

입력 : 5  ===> 결과 : [ 0, 0, 0, 0, 0 ] 

```java
package day08.배열추가문제;

import java.util.Scanner;

public class Quiz하03 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("칸 개수 입력: ");
		int aa = sc.nextInt();
		
		int [] arr = new int [aa];
		
		for (int i = 0; i < arr.length; ++i) {
			
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
		
	}
	}
  ```
