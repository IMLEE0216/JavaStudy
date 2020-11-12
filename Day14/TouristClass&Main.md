### Tourist 클래스 필드 메서드

        Tourist 클래스
        필드 : name, budget(예산), destination(목적지) private
        메서드 : 생성자 여러개 ... 맘대로 생성자 안함
        getter, setter, ...
        public String toString()
 
```java
package day14.quiz;


public class Tourist {
//field
	private String name;
	private int budget;
	private static String destination;

//===========================================	
//getter setter method 
	public void setName (String name){
		this.name = name;
		}
	public String getName() {
		return name;
		}
	
	public void setBudget (int budget){
		this.budget = budget;
		}
	public int getBudget (){
		return budget;
		}

	public void setDestination (String destination){
		this.destination = destination;
		}
	public String getDestination (){
		return destination;
		}
	
	public String toString() {
		return "\n이름: " + name + "\n목적지: "
				+ destination + ","
				+ "\n예산: " + budget;
	}

}
```

### Tourist Main 작성

	 Quiz01 클래스 - main()
 		메뉴) 
 		1. 목적지 설정 //만약 제주도면 모두 제주도
 		2. 여행객 추가  '한명씩 추가'
 		3. 모든 여행객 정보 보기
 		4. 전체 예산 보기
 		5. VIP 조회 
 		0. 종료 
	메뉴 메서드를 따로 하나하나 만들어도된다.(어후 머리 아프다...pass)
 
  	여행객은 최대 5명까지 받는다. 	배열쓰셈 
  	모든 여행객의 목적지는 동일하다.  static
  	예산이 가장 많은 여행객이 VIP다.  돈을 많이 가지고 있는 사람이 VIP다.

```java  
package day14.quiz;

import java.util.Scanner;
import day14.quiz.Tourist;
import javax.swing.JOptionPane;

import day10.homework.Pokemon;

public class quiz01 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		Tourist[] tour = new Tourist [5];
		int lastIdx = -1;
				
		String menu = "======메뉴======" + "\n1.목적지 설정\n"+ "2.여행객 추가\n"+ 
				"3.모든 여행객 정보 보기\n" +"4.전체 예산 보기\n" +"5.VIP 조회\n" + "0. 종료";
		String select;
		
		while (true) {
			select = JOptionPane.showInputDialog(menu);
			switch(select) {
			
			case "0": {
				JOptionPane.showMessageDialog(null, "프로그램 종료");
				return;
			} //case1
			
			case "1": {
				Tourist des = new Tourist();
				des.setDestination(JOptionPane.showInputDialog("목적지를 입력해 주세요. \n*단, 한 곳을 정하면 모두 같은 배 타는겁니다."));
				break;	
			}//case1
				
			
			case "2": {
				if(lastIdx +1  == tour.length) {
						JOptionPane.showMessageDialog(null, "추가 불가");
						continue;
					}
					Tourist t = new Tourist(); //한명씩 추가
					t.setName(JOptionPane.showInputDialog("이름"));
					t.setBudget(Integer.parseInt(JOptionPane.showInputDialog(t.getName() + "의 예산")));
					tour[++lastIdx] = t;
					break;
				}//case2
			
			case "3": {
				if( lastIdx == -1 ) {
					JOptionPane.showMessageDialog(null, "여행객 정보 없음");
					break;
				}
				String message = "======= 여행객 정보 =======\n";
				for(Tourist t : tour) {
					if(null == t) {
						break;
					}
					message += "\n=========정보=========="+ t;

				}
				JOptionPane.showMessageDialog(null, message);
				break;
			}//case3
			
			case "4" : {
				if( lastIdx == -1 ) {
					JOptionPane.showMessageDialog(null, "여행객 정보 없음");
					break;
				}
				int sum = 0;
				for(int i=0; i<=lastIdx; ++i) {
					sum += tour[i].getBudget();
				}
				JOptionPane.showMessageDialog(null,"전체 예산 : " + sum);
				break;
			} //case4
			
			case "5": {
				if( lastIdx == -1 ) {
					JOptionPane.showMessageDialog(null, "여행객 정보 없음");
					break;
				}
				int vip =0;
				for (int i =0; i< lastIdx+1; ++i) {
					if (tour[vip].getBudget() < tour[i].getBudget()) {
						vip = i;
					}
				}
				JOptionPane.showMessageDialog(null, "VIP: " + tour[vip].getName()); 
				break;
			}
			default:
				JOptionPane.showMessageDialog(null, "다시 입력하세요.");
				break;
			
			}//Switch
		}//While 
	}//Main
}//Class

```
