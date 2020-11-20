### 문제1 입력 받은 단어들...

  
        1. 사용자가 -1을 입력할 때까지 문자열을 입력 받고
          1) 입력된 문자열 중 소문자 'a'의 개수를 출력하세요.
          2) 비출력문자(공백,엔터 등)을 제외한 문자의 총 개수를 출력하세요.
          3) 단어의 개수를 출력하세요.
```java
package day19.homework;

import java.util.Scanner;
import java.util.StringTokenizer;

public class Homework01 {
	public static void main(String[] args) {
		Scanner sc =new Scanner(System.in);
		String words;
		int count = 0;
		int total = 0;
		int wtotal = 0;
		System.out.println("단어를 입력하세요.\n종료는 -1");
		
	while (true) {
		  words = sc.next();
			if (words.equals("-1")) {
				System.out.println("종료");
				break;
			}
      
			for (int i = 0; i < words.length(); ++i) {
				if (words.charAt(i) == 'a') { //a개수 만큼 증가
					++count;
				} 
     			if(words.charAt(i) == ',' || words.charAt(i) == '.') { //특수문자 다 넣어야하나...
					continue;
				}
//			if (words.charAt(i) == ' ' || words.charAt(i) == '\n'){ //이거없어도 문자의 개수는 잘 입력된다. 왜지?
//			continue;
//      }
					++total;
				} //for
			
				StringTokenizer st = new StringTokenizer(words," ") ;//이걸로 해결했지만 뭔지 모르겠다ㅋㅋ
				++wtotal;
				}//while

		System.out.println("a의 개수: " + count);
		System.out.println("문자의 총 개수: " + total);
		System.out.println("단어 개수: " + wtotal);
	}
}
```
      단어를 입력하세요.
      종료는 -1
      happy,
      cat.
      sleep
      -1
      종료
      a의 개수: 2
      문자의 총 개수: 13
      단어 개수: 3
      
### ID&PW

         2. 회원가입과정은 다음과 같습니다.
	        1) 이메일을 입력 받는다.
	        2) 비밀번호를 2번 입력받는다.
	
           이때 다음 조건에 충족하면 저장, 그렇지 않으면 해당 항목을 재입력 받으세요
        	1) 이메일 조건
	        	- @ 를 포함하여야 한다.
		        - com, co.kr, net 중 하나로 끝나야 한다
	        	- 메일서버(naver, gmail, hanmail 등) 이름을 포함해야 한다.
	        	- 아이디가 있어야 한다.
	        	- 공백이 있다면 제거한다.
		
	        2) 비밀번호 조건
		        - 4자 이상 20자 이하여야 한다.
		        - (선택사항) 특수기호, 숫자, 대소문자가 최소 1개씩 모두 있어야 한다. (String 클래스의 matches()사용)
	        	- 두 비밀번호가 동일해야 한다.

          모두 정상적인 입력을 받았다면 사용자의 id, 패스워드, 이메일을 출력하세요.
	        1) id 는 이메일의 @ 앞 부분을 추출합니다.
        	2) 비밀번호는 앞 두 글자만 출력하고 나머지는 '*'로 대체합니다.
	        	예) pika1234 ==> pi******
        	3) 이메일은 모두 출력합니다.

```java
public class Homework02 {
	
	public static boolean settingId(String Id) {
		if (Id.indexOf('@') < 1) {
			return false;
		}
		if (!Id.endsWith("com") && !Id.endsWith("co.kr") && !Id.endsWith("net")) { 
			return false; //끝나야한다. //충족안하면 빠꾸
		}
		if (!Id.contains("naver") && !Id.contains("gmail") && !Id.contains("hanmail") && !Id.contains("hotmail")) {
			return false; //서버포함 	//충족안하면 빠꾸
		}
		return true; 
		}
	
	
	public static boolean settingPw(String pw) {
		if (pw.matches("^(?=.*\\d)(?=.*[~`!@#$%\\^&*()-])(?=.*[a-z])(?=.*[A-Z]).{4,20}$")) {
//			              -------  ---------------------  ---------  ----------  -----
//			              뭔지모름      특수문자 포함	      소문자     대문자  최소4자 최대20자     $는 뭘까?
			return true; //이것들 충족하면 true
		}
		return false; 
	}
	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		String id = null; //null이 없으면 밑에서 막힘...
		String pw = null;
		String pw2;
		boolean a = true, b =true; //while문에서 나올려면 마지막에 false여야함...
		
		
		while (a) { //처음부터 false를 넣으면안되니깐  boolean써서 마지막에 탈출 할 수 있게 false 입력해주기
			System.out.println("e-mail을 입력하세요: ");
			id = sc.nextLine().trim(); //trim 공백 삭제
			if (!settingId(id)) {
				System.out.println("잘못된 아이디 형식입니다.\n예)abcd@gmail.com");
				continue;
				} 	
			 a = false; //false여야지 다음 while로 이동.
			}//while id
		
		while (b) {
			System.out.println("비밀번호 입력하세요: ");
			pw=sc.nextLine().trim();
			if (!settingPw(pw)) {
				System.out.println("잘못된 비밀번호 형식입니다.\n4~20자리\n특수문자, 대소문자, 숫자 최소 한개씩은 포함");
				continue;
				}
			
			System.out.println("비밀번호 재확인: ");
			while (b) {
				pw2 = sc.nextLine().trim();
				if (!pw.equals(pw2)) {
					System.out.println("비밀번호가 동일하지 않습니다.\n비밀번호 재확인: ");
					continue;
					} 
				b = false;
			}//while 작은 
			b = false;
			}//while 큰
	
	System.out.println("ID: " + id.substring(0, id.indexOf('@') ));
	System.out.println("Password: " + pw.substring(0, 2)+pw.substring(2).replaceAll("[a-z]|[A-Z]|[$@#!%*?&]|[0-9]", "*"));
//		                                                                        ------------reg-------------- , 요걸로
	System.out.println("email: " + id);
	} //main
}//class
```
      e-mail을 입력하세요: 
      java12@naver.com
      비밀번호 입력하세요: 
      Java12
      잘못된 비밀번호 형식입니다.
      4~20자리
      특수문자, 대소문자, 숫자 최소 한개씩은 포함
      비밀번호 입력하세요: 
      Java12!
      비밀번호 재확인: 
      Jaca12!
      비밀번호가 동일하지 않습니다.
      비밀번호 재확인: 
      Java12!
      ID: java12
      Password: Ja*****
      E-mail: java12@naver.com
