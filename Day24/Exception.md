### throw & throws & Exception

       email, password 문제 리팩토링 
         ==> 조건에 맞는 않는 입력이면 throw 로 예외객체를 생성하여 던질 것 
         ==> 예외클래스 MySignupPolicy를 정의하여 사용할 것 
         ==> setEmail(), setPassword(), confirmPassword() 에 throws 선언을 할 것!
         ==> main()에서 try-catch를 할 것

```java
 class MySingupPolicy extends Throwable{
	public MySingupPolicy(String message) {
		super(message);
	}
 ```
 ```java
  public boolean setEmail(String email) throws MySingupPolicy {
		
		// null comparison
		if(null == email) {
			throw new MySignupPolicyExcepton("이메일이 누락되었습니다.");
		}
		
		
		// email 양 공백 제거
		email = email.trim();
		
		
		// @ 를 포함하여야 한다.
		if(!email.contains("@")) {
			throw new MySingupPolicy("@를 포함하셔야 합니다.");
			//throw new MySingupPolicy("@를 포함하셔야 합니다.");
			
		}
		
		// trim이 되었고 @가 있는 이메일은  
		//  아이디가 없을 경우 무조건 맨 앞글자가 "@"일 것이다.
		if(email.indexOf("@") == 0) {
			throw new MySingupPolicy("아이디를 포함하셔야합니다."); ///////// 요부분
			//throw new MySingupPolicy("아이디를 포함하셔야합니다.");
		}
		
		// com, co.kr, net 중 하나로 끝나야 한다
		String suffix = null;
		for(String s : Whitelist.VALID_MAIL_SUFFIXES) {
			if(email.endsWith(s)) {
				suffix = s;
				break;
			}
		}
		if(null == suffix) {
			throw new MySingupPolicy(java.util.Arrays.toString(Whitelist.VALID_MAIL_SUFFIXES) + "포함해야 합니다");  //////// 이런 부분 
			//throw new MySingupPolicy(Whitelist.VALID_MAIL_SUFFIXES + "포함해야 합니다");
			// java.util.Arrays.toString(Whitelist.VALID_MAIL_SUFFIXES) 이렇게 해야 값이 나온다.
		}
		
		// 메일서버(naver, gmail, hanmail 등) 이름을 포함해야 한다.
		boolean check = false;
		for(String server : Whitelist.VALID_MAIL_SERVER_NAMES) {
			if(email.endsWith("@" + server + "." + suffix)) {
				check = true;
				break;
			}
		}
		if(!check) {
			throw new MySingupPolicy(java.util.Arrays.toString(Whitelist.VALID_MAIL_SERVER_NAMES) +"포함해야 합니다");
			//throw new MySingupPolicy(Whitelist.VALID_MAIL_SERVER_NAMES + "포함해야 합니다"); //해쉬값이 나옴
			//throw new MySingupPolicy(java.util.Arrays.toString(Whitelist.VALID_MAIL_SERVER_NAMES) + "포함해야 합니다"); //이래야 naver 
		}
		this.email = email;
		setId();
		return true;
	}
```
```java
  public boolean setPassword(String password) throws MySingupPolicy { //throws MySingupPolicy
		if (!password.matches(Whitelist.PASSWORD_REGEX)) {
			throw new MySingupPolicy("특수기호, 숫자, 대소문자가 최소 1개씩을 포함하셔야 합니다."); 
			//throw new MySingupPolicy("특수기호, 숫자, 대소문자가 최소 1개씩을 포함하셔야 합니다.");
		}
		if(password.length() < 5 || password.length() > 20) {
			throw new MySingupPolicy("비밀번호는 5~20자여야합니다."); 
			//throw new MySingupPolicy("비밀번호는 5~20자여야합니다.");
		}
		this.password = password;
		return true;
	}
```
```java
public boolean confirmPassword(String password) throws MySingupPolicy {
	if(null == this.password) {
		throw new MySignupPolicyExcepton("두 번째 비밀번호가 누락되었습니다.");
		//throw new MySignupPolicyExcepton("두 번째 비밀번호가 누락되었습니다.");
	}

	return this.password.equals(password);
} 
```
```java
public class homework_Exception {
	public static void main(String[] args) {
		User user = new User();
		Scanner sc = new Scanner(System.in); 
		
		// 이메일 입력 loop 
		while(true) {
			try {
				System.out.print("이메일 : ");
				String email = sc.next();
				if(!user.setEmail(email)) {
					continue;
				}
				break;
			} catch(MySingupPolicy e) { ///////////// 요 부분!
				System.out.println("잘못된 이메일 형식입니다.");
				System.out.println(e.getMessage()); 
			}
			
		}
		
		
		
		while (true) {
			try {
				System.out.print("비밀번호 : ");
				String password = sc.next();
				User01.setPassword(password);
				
				System.out.print("한 번 더 : ");
				String temp = sc.next();
				if (!User01.confirmPassword(temp)) {
					System.out.println("두 비밀번호가 일치하지 않습니다.");
					continue;
				}
				break;
			} catch (MySignupPolicyExcepton e) {
				System.out.println(e.getMessage());
			}
		}
		
				
	
		System.out.println(user);
	}
}

```
  
  
  
