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
