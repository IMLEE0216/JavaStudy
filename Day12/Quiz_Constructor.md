### Student_Quiz_Constructor

```java
public class Student { //클래스 Student 생성
	
	//create field
	String name;
	int kr;
	int en;
	int ma;
	double avg;
	char grade; 
	
	
	//Constructor
	Student (String name) {
		this.name = name;
	}
	Student (int k, int e, int m){
		kr = k;
		en = e;
		ma = m;
		avg = setMean(); //(kr+en+ma)/3.0
		grade = setGrade();
		}

	Student (String name, int k, int e, int m){
		this.name = name;
		kr=k;
		en=e;
		ma=m;
		avg = setMean(); //(kr+en+ma)/3.0
		grade = setGrade();
	}
	
	
	//create method
	void setData(String n, int k, int e, int m) {
		name = n;
		kr = k;
		en = e;
		ma = m; //해당필드에 저장
		return;
	}
	double setMean() {
		return avg = (kr+en+ma)/3.0;
	}
	char setGrade() {
		if (avg >= 90.0) {
			grade = 'A';
		} else if (avg >= 80) {
			grade ='B';
		} else if (avg >= 70) {
			grade = 'C';
		} else if (avg >= 60) {
			grade = 'D';
		} else {
			grade = 'F';
		} return grade;
	}
	
	void printData() {
		System.out.println("이름: " + name);
		System.out.println("국어: " + kr);
		System.out.println("영어: " + en);
		System.out.println("수학: " + ma);
		System.out.println("평균: " + avg);
		System.out.println("등급: " + grade);
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


### Pokemon 클래스 필드 생성자 메서드
 ```java
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
		this.name =name;
		this.level = level;
		hp = level*1000;
		if ((int)(Math.random()*10) > 2) {
			ap = level*1.5;
		} else {
			ap = level*2;
		}
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
		name = n;
		level = lv;
		hp = lv*1000;
		ap = Math.random() > 0.2? ap*1.5 : ap*2;
		}
//		if ((int)(Math.random()*10) > 2) {
//			ap = lv*1.5;
//		} else {
//			ap = lv*2;
//		}
	
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
		return level++;
	}
		/* 4. isAlive()
			인자값 : X
			하는 일 : 객체의 생사여부 확인( 체력이 0 이하면 죽음 )
			리턴값 : 살아있으면 true, 아니면 false
		*/
	boolean isAlive() {
		return alive = hp > 0? true : false;
		
	}
		/*5. attack()
			인자값 : 적 포켓몬 객체 (Pokemon형)
			하는 일 : 상대 포켓몬의 체력을 이 객체의 공격력만큼 감소
				10% 확률로 치명타 (공격력 X 1.5배)
			리턴값 : 없음
		 */
	void attack(Pokemon enemy) {
		ap = Math.random() < 0.1? ap*1.5 : ap;
		enemy.hp -= ap;	
	}
}

