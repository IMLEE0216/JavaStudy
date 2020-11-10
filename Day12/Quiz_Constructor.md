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
    
    
