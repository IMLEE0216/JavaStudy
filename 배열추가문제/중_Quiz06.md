### 배열추가문제 Quiz06 (중)

        로또생성기 만들기 
        step1) 사용자에게 1 ~ 45 중 6개의 숫자를 입력 받습니다.
        step2) 컴퓨터는 로또 번호 6개를 생성합니다. 배열의 크기는 6이고 int형입니다.
        step3) 1 ~ 45 중 6개의 숫자를 배열에 담습니다. 중복된 원소가 있으면 안됩니다.
        step4) (구현 가능하다면) 오름차순 정렬을 합니다.
        step5) 배열 결과를 출력합니다.
        step6) 사용자가 몇 개의 번호를 맞췄는지 출력하세요.
```java
package day08.배열추가문제;

import java.util.Scanner;


public class Quiz중06 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int [] Plotto = new int [6];
		int [] Clotto = new int [6];
//s1==============================================================		
		for (int i = 0; i <Plotto.length; ++i) {
			System.out.println((i+1) +  "번쨰 Lotto 번호를 입력하세요.");
			Plotto[i] = sc.nextInt();
			
			for (int j = 0; j < i ; ++j ) {
				if (Plotto[j] ==Plotto[i]) {
					System.out.println("중복된 수 입니다.");
					i--;
				} 
				if (Plotto[i] > 45) {
					i--;
					System.out.println("1~45번 까지 입니다.");
				}
			}
		}
//s2=============================================================		
		for (int i = 0; i<Clotto.length; i++) {
			Clotto[i] = (int)(Math.random()*45)+1;
			for (int j = 0; j<i; ++j){
				if (Clotto[i] == Clotto[j]) {
					i--;
				}
			}
		}
//s4-1===============================================================
		int i, j, temp;
		  for (i = 0; i < Plotto.length; i++) {
	            for (j = i + 1; j < Plotto.length; j++) {
	                if (Plotto[i] > Plotto[j]) {
	                    int tmep = Plotto[i];
	                    Plotto[i] = Plotto[j];
	                    Plotto[j] = tmep;
	                }
	            }
	       }
//s4-2===============================================================		  
		  for (i = 0; i < Clotto.length; i++) {
	            for (j = i + 1; j < Clotto.length; j++) {
	                if (Clotto[i] > Clotto[j]) {
	                    int tmep = Clotto[i];
	                    Clotto[i] = Clotto[j];
	                    Clotto[j] = tmep;
	                }
	            }
	      }
//s5-1===============================================================
		  System.out.println("사용자 번호: ");
		  for (i = 0; i< Plotto.length; i++) {
			  if (i <Plotto.length-1) { 
			  System.out.print(Plotto[i] + ",");
			  continue;
		  	} else {
			  System.out.println(Plotto[i] + " ");
		  	}
		  }
		  
//s5-2==================================================================	
		  System.out.println("컴퓨터 번호: ");
		  for (i = 0; i< Clotto.length; i++) {
			  if (i <Clotto.length-1) { 
			  System.out.print(Clotto[i] + ",");
			  continue;
		  	} else {
			  System.out.println(Clotto[i] + " ");
		  	}
		  }
		  
		  
//s6==================================================================			  
		  int count = 0;
		  for (i = 0; i<Plotto.length && i<Clotto.length; i++) {
			  if (Plotto[i] == Clotto[i]) {
				  count++;
			  }
		  }
		  System.out.println(count + "개 맞췃습니다.");	
	
  }//Main
}//Class
```
