### 메소드 예제 문제 
```java
package day11.basic.메소드;

public class FunctionFactory {
	/* strGugudan()
	 *  인자값 : 정수 1개 
	 *  하는 일 : 해당 구구단 1개의 문자열로 만들기 
	 *  리턴값 : 구구단 문자열 ("2 X 1 = 2 \n2 X 2 = 4 \n2 X 3 = 6\n...")
	 */
	void strGugudan(int dan) {
		for (int j = 1; j < 10; ++j) {
			System.out.println(dan + "X" + j + "=" + dan * j);
		}
	}

//	=======================================================
	/* printGugudan()
	 *  인자값 : 정수 1개 
	 *  하는 일 : 해당 구구단을 sysout
	 *  리턴값 : 없음
	 */
	void printGugudan(int dan) {
		for (int j = 1; j < 10; ++j) {
			System.out.println(dan + "X" + j + "=" + dan * j);

		}
		return;
	}
//	======================================================
	/* getAverage()
	 *  인자값 : 국, 영, 수
	 *  하는 일 : 국, 영, 수 평균 계산
	 *  리턴값 : 평균값
	 */
	double getAverage(int kr, int en, int ma) {
		return (kr+en+ma)/3; 
	}

//==========================================================
	/* getRandomPokemon()
	 *  인자값 : X
	 *  하는 일 : "피카츄", "라이츄", "파이리", "꼬부기" 중 1개의 포켓몬을 랜덤으로 뽑기
	 *  		(Math.random() 사용)
	 *  리턴값 : 뽑힌 포켓몬 이름 
	 */
	String getRandomPokemon() {
		String [] pkname = {"피카츄","라이츄","파이리","꼬북이"};
		for (int i = (int)(Math.random()*3); ; ) {
			return pkname[i];
			
		}
	}
	
//==========================================================	
	/* getMax()
	 *  인자값 : int형 배열 1개 
	 *  하는 일 : 이 배열의 원소 중 가장 큰 수 찾기
	 *  리턴값 : 가장 큰 수
	 */
	int getMax(int [] Maxx) {
		int maxIndex = Integer.MIN_VALUE; //가장 큰 수 찾을 때
		for (int i : Maxx) {
			if (i > maxIndex) {
				maxIndex = i;
			}
		}
		return maxIndex;
		}
	
}
```

