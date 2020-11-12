### Pokemon 은닉과 캡슐 getter & setter

```java
package day12.quiz.메소드;

import java.util.Scanner;

	//class
public class Pokemon2 {
	//field
	private String name;
	private int level;
	private int hp; 
	private double ap; 
//==================================================================================
//Constructor
	public Pokemon2 () {
		
	}
	public Pokemon2 (String name, int level){
		setName(name);
		setLevel(level);
	}

//===================================================================================	
	//method getter & setter
	
	public void setName(String name){
		this.name = name;
	}
	public String getName() {
		return name;
	}
	public void setLevel(int level) {
		this.level = level;
		setHp();
		setAp();
	}
	public int getLevel() {
		return level;
	}
	private void setHp() {
		this.hp = level*1000;
	}
	public int getHp() {
		return hp;
	}
	private void setAp() {
		this.ap = Math.random() > 0.2? level*1.5 : level*2;
	}
	public double getAp() {
		return ap;
	}

}
```
### 호출

```java
package day12.quiz.메소드;

public class PokemonTest01 {
	public static void main(String[] args) {

		Pokemon2 p = new Pokemon2();
		p.setName("피카");
		p.setLevel(10);
		System.out.println(p.getName());
		System.out.println(p.getLevel());
		System.out.println(p.getHp());
		System.out.println(p.getAp());
		
		p.setLevel(20);
		System.out.println(p.getHp());
		System.out.println(p.getAp());
		
		Pokemon p1 = new Pokemon("이상해씨",50);
		System.out.println(p1.getInfo());
		
		
	}
}
```
      피카
      10
      10000
      15.0
      20000
      40.0
      Name: 이상해씨
      Lv: 50
      HP: 50000
      Att: 100.0
      
### import & 호출

```java
package day13.test;
import day12.quiz.메소드.Pokemon2;
public class PokemonTest01 {
	public static void main(String[] args) {
		Pokemon2 p1 = new Pokemon2();
		p1.setName ("라이츄");
		p1.setLevel(30);
		System.out.println(p1.getHp());
		System.out.println(p1.getAp());
		
		p1.setLevel(50);
		System.out.println(p1.getName());
		System.out.println(p1.getHp());
		System.out.println(p1.getAp());
	}
}
```
      30000
      60.0
      라이츄
      50000
      100.0
      
### Student 은닉과 캡슐 getter & setter

```java
package day11.quiz.메소드;

public class Student02 { //클래스 Student 생성
	
	//create field
	private String name;
	private int kr;
	private int en;
	private int ma;
	private double avg;
	private String grade = "F"; 
//==================================================================	
	//Constructor
	public Student02 (){
	}
	
	public Student02 (String name) {
		this(name,0,0,0);
	}
	
	Student02 (String name, int k, int e, int m){
		setName(name);
		setKr(k);
		setEn(e);
		setMa(m);
		setMean(); 
	}
//==================================================================		
	//Method getter & setter
	public void setName(String name) {
		this.name = name;
	}
	public String getName() {
		return name;
	}
	public void setKr(int kr) {
		this.kr = kr;
		setMean ();
		setGrade();
	}
	public int getKr () {
		return kr;
	}
	public void setEn(int en) {
		this.en = en;
		setMean ();
		setGrade();
	}
	public int getEr () {
		return en;
	}
	public void setMa(int ma) {
		this.ma = ma;
		setMean ();
		setGrade();
	}
	public int getMa () {
		return ma;
	}
	private void setMean () {
		this.avg = (kr+en+ma)/3.0;
		setGrade();
	}
	public double getMean() {
		return avg;
	}
	private void setGrade() {
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
		} 
	}
	public String getGrade() {
		return grade;
	}
}
```
### import & 호출

```java
package day13.test;
import day11.quiz.메소드.Student02;
public class StudentTest01 {
	public static void main(String[] args) {
		
		Student02 s1 = new Student02();
		s1.setName("파라오");
		s1.setKr(70);
		s1.setEn(80);
		s1.setMa(65);
		
	
		System.out.println(s1.getMean());
		System.out.println(s1.getGrade());
		
		s1.setKr(95);
		s1.setEn(85);
    		System.out.println(s1.getName());
		System.out.println(s1.getMean());
		System.out.println(s1.getGrade());
		
//		System.out.println(s1.setMean()); //볼수없다고 뜸.
	}
}
``` 

      71.66666666666667
      C
      파라오
      81.66666666666667
      B
