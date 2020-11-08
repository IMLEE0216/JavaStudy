### 배열추가문제 Quiz03 (중)

        "김", "이", "박", "최", "한" 등의 대한민국 성씨를 저장할 배열을 만들고, '성'씨들을 저장하세요.
        "피카츄", "라이츄", "파이리", "꼬부기", "버터풀", "야도란", "피죤투" 를 저장할 배열을 만들고 '이름'들을 저장하세요.
        총 10개의 성+이름 조합을 출력하세요. ( Math.random()을 사용하며, 중복 조합을 허용합니다)
        조합가능한 모든 이름을 출력하세요.
```java
package day08.배열추가문제;

public class Quiz중03 {
	public static void main(String[] args) {
		String [] fn = {"김", "이", "박", "최", "한"}; //성
		String [] pn = {"피카츄", "라이츄","파이리","꼬부기","버터플","야도란","피죤투"}; //이름
		
//		===============================================
		System.out.println("랜덤이름");
		for (int i = 1; i <= 10; ++i) {
			int r1 = (int)(Math.random()*5); //
			int r2 = (int)(Math.random()*7); //
			System.out.println(i+ "."+ fn[r1]+pn[r2]);
		}
//		==============================================
		System.out.println("조합 가능한 모든 이름");
		int No = 0;
		for (int i = 0; i < fn.length; ++i ) {
			for (int j = 0; j < pn.length; ++j) {
				No++;
				System.out.println(No + "." + fn[i] + pn[j]);
			}
		}
		
	} //Main
} //Class
```
