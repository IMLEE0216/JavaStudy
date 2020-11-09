### Student Class 생성

        클래스 : Student
         필드 : 이름, 국, 영, 수, 평균, 등급
        메소드 : 
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
public class Student { //클래스 Student 생성
	
	//create field
	String name;
	int kr;
	int en;
	int ma;
	double avg;
	char grade; 
	
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
	void setGrade() {
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
		}
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
