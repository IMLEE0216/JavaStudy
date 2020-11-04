### Day08_Quiz02 

```java
// double형 4칸짜리 배열을 생성하고 
// Scanner를 사용하여 각 원소를 입력 받음
// 입력 후 모든 원소를 출력
// a[0] = sc.nextDouble();

package day08.homework;

import java.util.Scanner;

public class Homework02 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		double [] dArr = new double [4];
		System.out.println("정수 입력: ");
		dArr[0] = sc.nextDouble();
		dArr[1] = sc.nextDouble();
		dArr[2] = sc.nextDouble();
		dArr[3] = sc.nextDouble();
		
			for (int i = 0; i < dArr.length; ++i) {
				System.out.println(dArr[i]);
	  }		
	}
}
```
