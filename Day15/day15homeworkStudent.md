### Student 부모클래스 & 자식 클래스 생성



    부모 클래스 : Student 
     1) 필드 : 학생이름, 나이, 학교명
     2) 메소드 :
       	ㄱ. 생성자 
      		- 디폴트 생성자(기본생성자)
      		- 학생이름, 나이, 학교명 3개 넣고 생성되도록 
       	ㄴ. getters
      	ㄷ. setters
 ```java
package day15.homework;

//=====================어머니클래스=======================
public class Student {
	//field
	private String stname;
	private int age;
	private String scname;

	//constructor
	Student () {
		
	}
	Student (String stname, int age, String scname) {
		this.stname = stname; this.age = age; this.scname = scname;
	}

	//getter setter
	public String getStname() {
		return stname;
	}
	public void setStname(String stname) {
		this.stname = stname;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getScname() {
		return scname;
	}
	public void setScname(String scname) {
		this.scname = scname;
	}
}

```
    자식 클래스1 : ElementaryStudent
      1) 추가할 필드 : 국어점수, 영어점수, 학부모 연락처
      2) 메소드 : 
      	ㄱ. 생성자 
   	    	- 학생이름, 나이, 학교명
      		- 학생이름, 나이, 학교명, 학부모 연락처
       		- 학생이름, 나이, 학교명, 국어점수, 영어점수
    		ㄴ. getters
	    	ㄷ. setters
```java    
 //=====================애기들 클래스======================	
class ElementaryStudent extends Student{
		int kr;
		int en;
		String momnum;
		
		//constructor	
		ElementaryStudent(String stname, int age, String scname) {
			super(stname, age, scname);
		}
		
		ElementaryStudent(String stname, int age, String scname, String momnum) {
			super(stname, age, scname);
			this.momnum = momnum;
		}
		
		ElementaryStudent(String stname, int age, String scname, int kr, int en) {
			super(stname, age, scname);	this.kr = kr;	this.en = en;
		}
		
		// getter & setter
		public int getKr() {
			return kr;
		}
		public void setKr(int kr) {
			this.kr = kr;
		}
		public int getEn() {
			return en;
		}
		public void setEn(int en) {
			this.en = en;
		}
		public String getMomnum() {
			return momnum;
		}
		public void setMomnum(String momnum) {
			this.momnum = momnum;
		}
		public String toString() {
			return "============" +"\n이름: " + getStname() + "\n나이: " + getAge() + "\n학교명: " + getScname() 
					+ "\n국어 점수: " + getKr() + "\n영어 점수: " + getEn() + "\n부모님 번호: " + getMomnum(); 
			}
	}
```

      자식 클래스2 : MiddleSchoolStudent
      1) 추가할 필드 : 국어점수, 영어점수, 수학점수, 평균점수		
      2) 메소드 : 
 	      ㄱ. 생성자 
 		      - 학생이름, 나이, 학교명, 국어점수, 영어점수, 수학점수
 		        (평균 자동 계산)
      	ㄴ. getters
      	ㄷ. setters 

```java
	class MiddleSchoolStudent extends Student {
		int kr;
		int en;
		int ma;
		double avg;
		
		//constructor
		MiddleSchoolStudent (String stname, int age, String scname, int kr, int en, int ma){
			super(stname, age, scname); this.kr = kr;	this.en = en; this.ma = ma;
			avg = getAvg();
		}
		
		//getter & setter
		public int getKr() {
			return kr;
		}
		public void setKr(int kr) {
			this.kr = kr;
		}
		public int getEn() {
			return en;
		}
		public void setEn(int en) {
			this.en = en;
		}
		public int getMa() {
			return ma;
		}
		public void setMa(int ma) {
			this.ma = ma;
		}
		public double getAvg() {
			return avg = (kr + en + ma)/3.0;
		}
		public void setAvg(double avg) {
			this.avg = avg;	
		}
		public String toString() {
			return "============" +"\n이름: " + getStname() + "\n나이: " + getAge() + "\n학교명: " + getScname() 
					+ "\n국어 점수: " + getKr() + "\n영어 점수: " + getEn() + "\n수학 점수: " + getMa() 
					+ "\n평균: " + getAvg();
		}
	}
```

 
     자식 클래스3 : HighSchoolStudent
      1) 추가할 필드 : 국어점수, 영어점수, 수학점수, 평균점수, 내신등급	
      2) 메소드 : 
  	    ㄱ. 생성자 
  		   - 학생이름, 나이, 학교명, 국어점수, 영어점수, 수학점수
  		     (평균 자동 계산)
  	    ㄴ. getters
  	    ㄷ. setters
```java
  class HighSchoolStudent extends Student{
	  //field 
	  int kr;
	  int en;
	  int ma;
	  double avg;
	  String grade = "F";
	
	  //constructor
	HighSchoolStudent(String stname, int age, String scname, int kr, int en, int ma) {
		super(stname, age, scname); this.kr = kr;	this.en = en; this.ma = ma;
		avg = getAvg();
	}
	 
	  
	//getter & setter  
	public int getKr() {
		return kr;
	}
	public void setKr(int kr) {
		this.kr = kr;
	}
	public int getEn() {
		return en;
	}
	public void setEn(int en) {
		this.en = en;
	}
	public int getMa() {
		return ma;
	}
	public void setMa(int ma) {
		this.ma = ma;
	}
	public double getAvg() {
		getGrade();
		return avg = (kr + en + ma)/3.0;
		
	}
	public void setAvg(double avg) {
		this.avg = avg;
		
	}
	public String getGrade() {
		if (avg >= 90.0) {
			grade = "A";
		} else if (avg >= 80) {
			grade ="B";
		} else if (avg >= 70) {
			grade = "C";
		} else if (avg >= 60) {
			grade = "D";
		} else {	
		} 
		return grade;
	}
	
	public void setGrade(String grade) {
		this.grade = grade;
	}
	public String toString() {
		return "============" +"\n이름: " + getStname() + "\n나이: " + getAge() + "\n학교명: " + getScname() 
				+ "\n국어 점수: " + getKr() + "\n영어 점수: " + getEn() + "\n수학 점수: " + getMa() 
				+ "\n평균: " + getAvg() + "\n등급: " + getGrade();
	}
  }
```

### Mian

      메인 클래스 : Quiz02
      - 이름과 나이를 입력 받음
      - 나이에 따른 객체 생성 (예. 13 -> new ElementaryStudent())
      - 각 객체의 필드를 입력 받아서 저장 
        예. 중학생이면
     	     학교명, 국어점수, 영어점수, 수학점수 입력 받음
      - 결과 출력
```java
package day15.homework;

import java.util.Scanner;

public class homework01 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		Student s = new Student (); 

				System.out.println("학생의 이름: ");
				s.setStname(sc.next());
				
			while (true) {
				System.out.println("학생의 나이: ");
				s.setAge(sc.nextInt());
				
				if (s.getAge() < 8 || s.getAge() > 20) {
					System.out.println("나이를 다시 입력해주세요.");
					} 
			
				if (s.getAge()>=8 && s.getAge() <= 13) {
					ElementaryStudent e = new ElementaryStudent(s.getStname(),s.getAge(),null);
					System.out.println("초등학생입니다.");
					System.out.println("학생의 학교명: ");
					e.setScname(sc.next());
					System.out.println("부모님 전화번호 입력: ");
					e.setMomnum(sc.next());
					System.out.println("국어 점수 입력: ");
					e.setKr(sc.nextInt());
					System.out.println("영어 점수 입력: ");
					e.setEn(sc.nextInt());
					System.out.println(e);		
					break;
					}
							
				if (s.getAge()>=14 && s.getAge() <= 16) {
					MiddleSchoolStudent m = new MiddleSchoolStudent(s.getStname(),s.getAge(),null,0,0,0);
					System.out.println("중학생입니다.");
					System.out.println("학생의 학교명: ");
					m.setScname(sc.next());
					System.out.println("국어점수: ");
					m.setKr(sc.nextInt());
					System.out.println("영어점수: ");
					m.setEn(sc.nextInt());
					System.out.println("수학점수: ");
					m.setMa(sc.nextInt());
					System.out.println(m.getAvg());
					System.out.println(m);	
					break;
					}
				
				if (s.getAge()>=17 && s.getAge() <= 19) {
					HighSchoolStudent h = new HighSchoolStudent(s.getStname(),s.getAge(),null,0,0,0);
					System.out.println("고등학생입니다.");
					System.out.println("학생의 학교명: ");
					h.setScname(sc.next());
					System.out.println("국어점수: ");
					h.setKr(sc.nextInt());
					System.out.println("영어점수: ");
					h.setEn(sc.nextInt());
					System.out.println("수학점수: ");
					h.setMa(sc.nextInt());
					System.out.println(h.getAvg());
					System.out.println(h.getGrade());
					System.out.println(h);
					break;
					}
			}
	} //main
} //class
```
    학생의 이름: 
    이이
    학생의 나이: 
    17
    고등학생입니다.
    학생의 학교명: 
    고랭
    국어점수: 
    70
    영어점수: 
    80
    수학점수: 
    90
    80.0
    B
    ============
    이름: 이이
    나이: 17
    학교명: 고랭
    국어 점수: 70
    영어 점수: 80
    수학 점수: 90
    평균: 80.0
    등급: B


