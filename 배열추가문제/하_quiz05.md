### 배열추가문제 Quiz05 (하)

하-5 : 사용자에게 배열의 칸 개수를 입력 받고, 해당 정수의 크기만큼 String형 배열을 생성하고

입력 : 3  ===> 결과 : [ null, null, null ] 

입력 : 5  ===> 결과 : [ null, null, null, null, null ]

사용자에게 입력받은 단어들을 순차적으로 배열에 저장하세요.  

```java
package day08.배열추가문제;

import java.util.Scanner;

public class Quiz하05 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		System.out.println("칸 개수 입력: ");
		int abc = sc.nextInt();
		
		
		String [] arr = new String [abc];
		
		for (int i = 0; i < arr.length; ++i) {
			System.out.println((i+1)+ "번째 단어를 입력하세요.");
			arr[i] = sc.next();
		}
		
		System.out.print("결과 : [ ");
		for (int i = 0; i < arr.length; ++i) {
			if(i<(arr.length-1)) {
				System.out.print(arr[i] + ", ");
				continue;
			} 
			
			System.out.println(arr[i]+" ]");
		}
		
	}
}

```
