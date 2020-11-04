### Day08_Quiz03
'A' : 65 , 'Z' : 90

 chArr[i] >= 65 && chArr[i] <= 90 ===> 대문자니? chArr[i] >= 'A' && chArr[i] <= 'Z' ===> 대문자니?

대문자 + 32 == 소문자 소문자 - 32 == 대문자

위 세 단어가 잘 출력되도록 sysout 중간 중간에 for문을 사용하여 코드를 완성하세요.

```java
 

package day08.homework;

public class Homework03 {
	public static void main(String[] args) {
		char[] ch = {'M', 'e', 't', 'h', 'O', 'D'};
		System.out.println(ch);
		
		for (int i = 0; i < ch.length; ++i) {
			if (ch[i] >= 'a' && ch[i] <= 'z') {
				ch[i] -= 32;
			}
		}
		System.out.println(ch);
		
		for (int i = 0; i < ch.length; ++i) {
			if (ch[i] >= 'A' && ch[i] <= 'Z') {
				ch[i] += 32;
			}
		}
		System.out.println(ch);
	}
}
