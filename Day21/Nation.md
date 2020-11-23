### 국가 관리 프로그램

        0. Nation 클래스 
	      필드 : 국가명(nation)  수도명(capital)  인구수(population) ==> 모두 private 
	      메서드 : 	
		      Nation()  생성자
		      Nation(국가, 수도)  생성자
		      Nation(국가, 수도, 인구수)  생성자
		      getter, setter 
		      toString() 오버라이드 


```java
package day21.homework;


import java.text.DecimalFormat;
import java.util.ArrayList;
import javax.swing.JOptionPane;


class Nation{
	private String nation;
	private String capital;
	private long population;
	
	DecimalFormat df = new DecimalFormat("#,###");
	
	Nation(){	
		this(null, null, 0);
	}
	
	Nation(String nation, String capital){
		this(null, null , 0);
	}
	Nation(String nation, String capital, long poppulation){
		this.nation = nation;
		this.capital = capital;
		this.population = poppulation;
	}
	public String getNation() {
		return nation;
	}
	public void setNation(String nation) {
		this.nation = nation;
	}
	public String getCapital() {
		return capital;
	}
	public void setCapital(String capital) {
		this.capital = capital;
	}
	public long getPopulation() {
		return population;
	}
	public void setPopulation(long population) {
		this.population = population;
	}
	@Override
	public String toString() {
		return "===============\n" + "Nation: " + getNation() + 
					"\nCapital: " + getCapital() + 
					"\nPopulation: " + df.format(getPopulation());
	}
	public String showInfo() {
		return "===============\n" + "Capital: " + getCapital() + 
					"\nPopulation: " + df.format(getPopulation());
	}

}
```

        1. ArrayList 객체 생성 (Nation 객체들을 저장할 창고 객체) 
        2. 메뉴 띄우기
	        1) 국가 추가   ==> 국가명, 수도명, 인구수 입력 받아 Nation 객체 생성 후 ArrayList에 add()
	        2) 모든 국가 보기	==> 현재 등록된 국가들을 모두 출력 (for문과 Nation.toString() 활용)
	        3) 국가 검색 	==> 국가명을 입력 받고, 해당 국가가 있으면 수도, 인구수 출력
			                      없으면 "미등록 국가"
		                        인구수는 ',' 추가 ( 예) 100,000,000 명 ) 
	        0) 종료 
          
```java
public class homework01 {
	public static void main(String[] args) {
		ArrayList<Nation> nations = new ArrayList<Nation>();
		String menu;
		String select;
		int a = -1;
		menu = "=====MENU=====" + "\n1. Add Nation" + "\n2.Show All Info" + "\n3. Search" + "\n0. Exit";
		
		while (true) {
			select = JOptionPane.showInputDialog(menu);
			switch (select) {
			case "0": {
				JOptionPane.showMessageDialog(null, "Program Exit");
				return;
			}//case 0
			case "1": {			
				nations.add(new Nation(JOptionPane.showInputDialog("Nation: "),
							JOptionPane.showInputDialog("Capital: "),
							Integer.parseInt(JOptionPane.showInputDialog("Population: "))));
				break;
			} //case 1
			case "2":{
				for (Nation n : nations) {
					JOptionPane.showMessageDialog(null, n.toString());
					a++;
					break;
				}
				if (a == -1) {
						JOptionPane.showMessageDialog(null, "등록된 정보 없음");
					}
				break;
			} //case 2
			case "3":{
				for (int i = 0; i < nations.size(); i++) {
					String s = JOptionPane.showInputDialog("Name of Nation: ");
					if (nations.get(i).equals(s)) {
						JOptionPane.showMessageDialog(null, "미등록 국가");
						break;
					} else {
						JOptionPane.showMessageDialog(null, nations.get(i).showInfo());
					}
					}
						break;
					}//case 3
			}//Switch
		}//While
	}//Main
}//Class
```
