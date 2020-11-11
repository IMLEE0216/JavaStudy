### Student_Quiz_Constructor

 	클래스 : Student
	 필드 : 이름, 국, 영, 수, 평균, 등급
 	메소드 : 
  	 0) 생성자:
   		student(String name) : name 만 저장
   		student(int k, int e, int m) : name은 "없음", 국여수는 k,e,m 값을 저장. 평균, 등급도 계산되어 저장
   		Student(String name, int k, int e, int m) : 이름,국영수는 name, k, e, m 값을 저장. 평균, 등급도 계산되어 저장
  	 1) setData() : 이름, 국, 영, 수를 인자값으로 받아, 해당 필드에 모두 저장
 	  2) setMean() : 객체가 가지고 있는 국, 영, 수를 가지고 평균을 계산하여 평균 필드에 저장
  	 3) setGrade() : 객체가 가지고 있는 평균을 가지고 등급을 저장 
     		 90이상 : A
		80이상 ~ 90미만 : B
      		70이상 ~ 80미만 : C
      		60이상 ~ 70미만 : D
     		 60미만 : F
	  4) printData() : 객체의 모든 정보(이름, 국, 영, 수, 평균, 등급)를 sysout
```java
package day11.quiz.메소드;

public class Student { //클래스 Student 생성
	
	//create field
	String name;
	int kr;
	int en;
	int ma;
	double avg;
	String grade = "F"; //String형으로 바꿔라 나중에 A+이라는게 나올수 있으니깐  //F를 기본값으로 
	
	
	//Constructor
	Student() {
		
	}
	Student (String name) {
		this.name = name;
	}
	Student (int k, int e, int m){
		this(null, k , e, m); //밑에 생성자한테 일을 떠맡김
		}

	Student (String name, int k, int e, int m){
		setData(name, k, e, m);
//		this.name = name;
//		kr=k;
//		en=e;
//		ma=m;
//		setMean(); //(kr+en+ma)/3.0
//		grade = setGrade();
		
	}
	
	
	//Method
	void setData(String n, int k, int e, int m) { //데이터에 다 넣어주면 생성자에서 편함
		name = n;
		kr = k;
		en = e;
		ma = m; //해당필드에 저장
		setMean(); //(kr+en+ma)/3.0 
//		grade = setGrade();
		return;
	}
	void setMean() {
		avg = (kr+en+ma)/3.0;
		setGrade(); //여기에 넣으면 자동으로 학점도 계산
	}
	String setGrade() {  //switch문을 써도 된다. 더 쉬움 return이 더 나음(밑에 명령이 없으면)
		if (avg >= 90.0) {
			grade = "A";
		} else if (avg >= 80) {
			grade ="B";
		} else if (avg >= 70) {
			grade = "C";
		} else if (avg >= 60) {
			grade = "D";
		} else {
			grade = "F";
		} return grade;
	}
	
	String getData() {
		return "이름: " + name + "\n국영수: " + kr + "," + en + "," + ma + "\n평균: " + avg + "\n등급: " + grade;
	}
	
	void printData() {
		System.out.println(getData());
//		System.out.println("이름: " + name);
//		System.out.println("국어: " + kr);
//		System.out.println("영어: " + en);
//		System.out.println("수학: " + ma);
//		System.out.println("평균: " + avg);
//		System.out.println("등급: " + grade);
		}
	
}

```


```java
public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		Student s1 = new Student("Lee");
		System.out.println(s1.name);
				s1.printData();
		
		Student s2 = new Student(65, 75, 80);
				s2.printData();
		
		Student s3 = new Student("Kim", 95, 85,70);
				s3.printData();
```
    Lee
    이름: Lee
    국어: 0
    영어: 0
    수학: 0
    평균: 0.0
    등급:
    이름: null
    국어: 65
    영어: 75
    수학: 80
    평균: 73.33333333333333
    등급: C
    이름: Kim
    국어: 95
    영어: 85
    수학: 70
    평균: 83.33333333333333
    등급: B


### Pokemon Cla Fie Con Meth
 ```java
package day12.quiz.메소드;

import java.util.Scanner;

//Pokemon 클래스 
//멤버변수 : name, level, hp(체력), ap(공격력)

public class Pokemon {
	//field
	String name;
	int level;
	int hp; //체
	double ap; //공
	boolean alive;
	
	
	//생성자
	//0. Pokemon(name)
	//name을 등록 
	//Pokemon(name, level)
//		name, level 등록
//		체력은 레벨의 1000배
//		공격력은 레벨의 1.5배 (20% 확률로 2배)
	Pokemon (String name){
		this.name = name;
	}
	
	Pokemon (String name, int level){
		setInfo(name, level);
	}
	
//===================================================================================	
	//method
	
	 	/*1. setInfo()
			인자값 : 이름, 레벨
			하는 일 : 인자로 들어온 값들을 멤버변수 name, level 에 모두 저장 
				체력은 레벨의 1000배
				공격력은 레벨의 1.5배 (20% 확률로 2배)
		 	리턴값 : X
		 */
	void setInfo(String n, int lv){
		this.name = n;
		this.level = lv;
		reset(); //추가한거임
//		setHp();
//		setAp();
		}
//	void setHp() {
//		hp = level*1000;
//	}
//	void setAp() {
//		ap = Math.random() > 0.2? level*1.5 : level*2;
//	}
		
	
		/*2. getInfo()
			인자값 : X
			하는 일 : "XXX / Lv. @@ / HP. ####" 형태로 name, level, hp 의 값들을 하나의 문자열로 표현
		 	리턴값 : "XXX / Lv. @@ / HP. ####" 형태의 문자열
		 */
	
	String getInfo() {
		return "Name: " + name + "\nLv: " + level + "\nHP: " + hp + "\nAtt: " + ap;
		}
		/* 3. levelUp()
			인자값 : X
			하는 일 : level을 1증가
			리턴값 : 증가된 level
		 */
	int levelUp() {
		++level;
		reset();
		return level;
	}
	
	//추가메서드: 레벨기반으로 hp,ap리셋
	void reset() {
		hp = level*1000;
		ap = Math.random() > 0.2? level*1.5 : level*2;
	}
	
		/* 4. isAlive()
			인자값 : X
			하는 일 : 객체의 생사여부 확인( 체력이 0 이하면 죽음 )
			리턴값 : 살아있으면 true, 아니면 false
		*/
	boolean isAlive() {
		return hp > 0;
		
	}
		/*5. attack()
			인자값 : 적 포켓몬 객체 (Pokemon형)
			하는 일 : 상대 포켓몬의 체력을 이 객체의 공격력만큼 감소
				10% 확률로 치명타 (공격력 X 1.5배)
			리턴값 : 없음
		 */
	void attack(Pokemon enemy) {
		enemy.hp -=  Math.random() < 0.1? ap*1.5 : ap;
	}
	
	public static void main(String[] args) {
		Pokemon p1 = new Pokemon("피");
		Pokemon p2 = new Pokemon("꼬",6);
		System.out.println(p1.getInfo());
		System.out.println(p1.isAlive());
		
		Scanner sc= new Scanner(System.in);
		System.out.println("이름,레벨");
		String name = sc.next();
		int level = sc.nextInt();
		p1.setInfo(name, level);
		
//		p1.name = sc.next(); //hp랑 ap다시 설정해야함
		
		p1.levelUp();
		p1.levelUp();
		System.out.println(p1.getInfo());
		
		p1.attack(p2);
		p2.attack(p1);
		System.out.println(p1.getInfo());
		System.out.println(p2.hp);
	}
}
```

