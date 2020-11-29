### 학생 관리 프로그램

          < 학생 관리 프로그램 >
           step 1. 다음 학생들의 정보를 Map 에 저장하세요. (TreeMap<Integer,HashMap<String,Object>>)
            key 는 학번(Integer)입니다.
            주의) Student 클래스를 사용하지 않고 학생 정보도 Map을 사용합니다. 	

		        101 : {"name":"홍길동", "average":88, "grade":"B", "contact":"010-2222-1231"},
		        102 : {"name":"김길동", "average":92, "grade":"A", "contact":"010-2231-1256"},
		        103 : {"name":"김장미", "average":47, "grade":"F", "contact":"010-2512-7754"},
		        ...

            코딩으로 그냥 넣고 
            학번		     이름      평균     등급          연락처
            101         홍길동      88       B        010-2222-1231
            102         김길동      92       A        010-2231-1256
            103         김장미      47       F        010-2512-7754
            201         장아름      85       B        010-9966-3512
            202        	최영수      74       C        010-1111-3864			
    
    
           step 2. (1)의 딕셔너리에 학생 3명의 정보를 입력 받아 추가 저장합니다. (+3명더)
               - 학생의 이름, 국, 영, 수, 학년, 연락처를 입력 받습니다.

               - 학년은 학번의 가장 앞자리에 해당합니다.
                  예를 들어 딕셔너리에 저장된 2학년 학생이 4명이라면, 다음 2학년 학생의 학번은 205가 되어야 합니다.
	          (1 <= 학년 <= 6)	
	           (0 <= 학년 당 학생의 수 < 100)

                - 평균은 국,영,수 의 평균을 계산하여 저장합니다.
                    *사용자에게 입력 받지 않습니다.

                - 등급은 평균에 따른 A, B, C, D, F 중 하나로 저장합니다.
                   *사용자에게 입력 받지 않습니다.
                   90 점 이상 : A
                   80점 이상 ~ 90점 미만 : B
                   70점 이상 ~ 80점 미만 : C
                   60점 이상 ~ 70점 미만 : D
                   60점 미만 : F
    
    
           step 3. 사용자 메뉴를 출력합니다. (선택문제)
                1. 학번으로 검색
                2. 연락처 뒷번호로 검색
                3. 1등 학생 보기 - for 최대값
                4. 모든 학생 보기 - for문
                 0. 종료

               1. 학번으로 검색
                    학번을 입력 받고 해당 학생의 모든 정보를 출력합니다.
                    미등록 학번인 경우 '미등록 학번'을 출력합니다.

               2. 연락처 뒷번호로 검색
                    연락처 뒷번호 4자리를 입력 받아 연락처가 일치하는
                    '모든' 학생들의 이름, 학년, 연락처를 출력합니다.

                3. 1등 학생 보기
                   평균을 가지고 1등 학생을 찾아 해당 학생의 학번, 이름, 평균 점수를 출력합니다.
                    공동 1등인 경우 학년이 가장 높은 학생을,
                   그 중 같은 학년에 공동 1등이 있다면 그 학생들 모두를 출력하세요.

               4. 모든 학생 보기
                   현재 등록되어있는 모든 학생들의 모든 정보를 출력하세요.

 
 
```java
package day23.testhome;

import java.util.HashMap;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.TreeMap;
import javax.swing.JOptionPane;

public class Homework01JOp {

TreeMap<Integer, HashMap<String, Object>> students = new TreeMap<Integer, HashMap<String, Object>>();
Scanner sc = new Scanner(System.in);

	
private void oldStudents() {
		students.put(101, new HashMap<>());
		students.get(101).put("name", "홍길동");
		students.get(101).put("average", 88);
		students.get(101).put("grade", "B");
		students.get(101).put("contact", "010-2222-1231");
		
		students.put(102, new HashMap<>());
		students.get(102).put("name", "김길동");
		students.get(102).put("average", 92);
		students.get(102).put("grade", "A");
		students.get(102).put("contact", "010-2231-1256");
		
		students.put(103, new HashMap<>());
		students.get(103).put("name", "김장미");
		students.get(103).put("average", 47);
		students.get(103).put("grade", "F");
		students.get(103).put("contact", "010-2512-7754");
		
		students.put(201, new HashMap<>());
		students.get(201).put("name", "장아름");
		students.get(201).put("average", 85);
		students.get(201).put("grade", "B");
		students.get(201).put("contact", "010-9966-3512");
		
		students.put(202, new HashMap<>());
		students.get(202).put("name", "최영수");
		students.get(202).put("average", 74);
		students.get(202).put("grade", "C");
		students.get(202).put("contact", "010-1111-3864");	
	}
	
private void newStudents() {
		while(true) {
			loop: for (int i = 0; i < 3; ++i) {
				JOptionPane.showMessageDialog(null, (i+1)+"번째 학생의 정보를 입력하세요.");
				String s = JOptionPane.showInputDialog("학년");
				if (Integer.parseInt(s) <= 0 || Integer.parseInt(s) >= 7) {
					JOptionPane.showMessageDialog(null, "다시 입력하세요.");
					break loop;
				}
			for (int a = 1 ; ; ++a) {	
				int num = Integer.parseInt(s)*100 + a;
				if (students.containsKey(num)) {
					continue;
				} else {
					students.put(num, new HashMap<>());
				}

				String name = JOptionPane.showInputDialog("이름");

				int kr, en, ma;
				kr = Integer.parseInt(JOptionPane.showInputDialog("국어"));
				en = Integer.parseInt(JOptionPane.showInputDialog("영어"));
				ma = Integer.parseInt(JOptionPane.showInputDialog("수학"));

				int avg = (kr + en + ma) / 3;
				String grade;
				if (avg >= 90) {
					grade = "A";
				} else if (avg >= 80) {
					grade = "B";
				} else if (avg >= 70) {
					grade = "C";
				} else if (avg >= 60) {
					grade = "D";
				} else {
					grade = "F";
				}
				
				String contactnum = JOptionPane.showInputDialog("전화번호").trim();
//==============================================================================================
				students.get(num).put("name", name);
				students.get(num).put("average", avg);
				students.get(num).put("grade", grade);
				students.get(num).put("contact", contactnum);
				JOptionPane.showMessageDialog(null, students.get(num));
				JOptionPane.showMessageDialog(null, students.keySet());
				break;
			}
		}
		return;
	}
		
	}
	
private void menu01() { //학번 검색
	String snum;
	snum = JOptionPane.showInputDialog("학번");
		
		if (snum == null) {
			JOptionPane.showMessageDialog(null, "메뉴로 돌아갑니다.");
		}
		JOptionPane.showMessageDialog(null, students.containsKey(Integer.parseInt(snum))? students.get(Integer.parseInt(snum)) : "미등록 학번");
}


private void menu02() { // 연락처 뒷 번호 검색
	String num = JOptionPane.showInputDialog("전화번호 뒷자리").trim();
	String last = null;
	for (Entry<Integer, HashMap<String, Object>> st : students.entrySet()) {
		last = st.getValue().get("contact").toString().substring(9);
		if (num.equals(last)) {
			JOptionPane.showMessageDialog(null, Info(st.getKey())); //getkey = 왼 //get value = 오	
			return;	
		}
		}
	if (!last.equals(num)) {
		JOptionPane.showMessageDialog(null, "없는 번호");
	}
} 


private void menu03() { //1등 보기
	TreeMap<Integer, HashMap<String, Object>> zero = new TreeMap<Integer, HashMap<String, Object>>();
	zero.put(0, new HashMap<String, Object>());
	zero.get(0).put("average", 0);
	for (Entry<Integer, HashMap<String, Object>> s : zero.entrySet()) {
	for (Entry<Integer, HashMap<String, Object>> st : students.entrySet()) {
		if(((Integer) st.getValue().get("average")) > ((Integer)s.getValue().get("average"))){
				s = st;
				continue;	
		}
			JOptionPane.showMessageDialog(null, Info(s.getKey()));
			break;
		}	
	}
	
}


private void menu04() { //전체 학생 
	StringBuffer message = new StringBuffer("=========== 모든 학생 정보 ===========\n");
	for (Entry<Integer, HashMap<String, Object>> st : students.entrySet()) {
		message.append("[" + st.getKey() + "] : " + st.getValue() + "\n");
	}
	JOptionPane.showMessageDialog(null, message);
}


public Homework01JOp() {
	oldStudents();
	newStudents();
	
	String menu = "1. 학번 검색 \n" + "2. 연락처 뒷번호 검색 \n" + "3. 1등 학생 \n" + "4. 모든학생  \n" + "0. 종료";
	menu: while (true) {
		 String select = JOptionPane.showInputDialog(menu);
		switch (select) {
		case "0":
			JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
			break menu;
		case "1":
			menu01();
			break;
		case "2":
			menu02();
			break;
		case "3":
			menu03();
			break;
		case "4":
			menu04();
			break;

		default:
			JOptionPane.showMessageDialog(null, "다시 입력하세요.");
			break;
		}
	}
}

	public static void main(String[] args) {
		new Homework01JOp();
		
	}
}
