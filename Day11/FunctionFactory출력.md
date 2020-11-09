### 메소드 예제 출력
```java
package day11.basic.메서드;

import java.util.Scanner;

public class FunctionTest01 {
	public static void main(String[] args) {
		FunctionFactory go = new FunctionFactory();
		Scanner sc = new Scanner(System.in);
		
		go.strGugudan(4);
//		============================================
		go.printGugudan(sc.nextInt());
//		============================================
		double Average = go.getAverage(80, 70, 75);
		System.out.println(Average);
//		============================================
		System.out.println(go.getRandomPokemon());
//		============================================
		System.out.println(go.getMax(new int[] {10, 2, 4, 150, 2, 100, 15}));
		
	}
}
```
