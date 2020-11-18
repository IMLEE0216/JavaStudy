### Person Clone & Copy 얕은 복사와 깊은 복사


       1. 깊은 복사와 얕은 복사 조사하기
         <얕은복사>
          - 얕은 복사는 복사 객체의 내용을 바꾸면 원본까지 복사 객체 내용 처럼 변화. 원본도 수정되어 버림.
          - 한 쪽에서 수정이 발생되면 다른쪽에도 영향을 끼쳐 같아지게 된다.
          - 가능한 이유는 얕은 복사가 주소값을 복사하기 때문에 주소로 값을 참조하여 값이 변경되면 해당 값을 참조하고 있는 배열들의 값이 변경된다.
  	-        즉, 복사된 배열이나 원본 배열이 변경될 때, 함께 변경된다. = 연산자는 얕은 복사를 수행한다.//인터넷~
  
          <깊은복사>
          - 깊은복사는 원본은 그대로 유지하고 복사만 변함. 원본 내용은 그대로 유지.
          - 깊은 복사는 주소값을 참조하는 것이 아닌, 새로운 메모리 공간에 값을 복사하는 것이기 때문에 원본 배열이 변경되어도 복사된 배열에 전혀 상관이 없다.
          - 따라서 배열을 복사한 후에 한쪽 값을 수정해도 다른 배열에 영향을 끼치지 않는다.//인터넷~
          
```java
class Person implements Cloneable{
	
	String name;
	int age;
	Person father;
	Person mother;
	
	Person (String name, int age) {
		this.name = name;
		this.age = age;
	}
	
	
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public Person getFather() {
		return father;
	}

	public void setFather(Person father) {
		this.father = father;
	}

	public Person getMother() {
		return mother;
	}

	public void setMother(Person mother) {
		this.mother = mother;
	}

	//clone() //요것은 clone
	@Override 
	protected Object clone() throws CloneNotSupportedException {
		// TODO Auto-generated method stub
		return super.clone();
	}
	//copy() // 요것은 copy
	public void copy (Person child) {
		child.setFather(getFather());
		child.setMother(getMother()); 
		//setName 넣어버리면 son의 이름까지 복사하는.....
	}
	
}
public class Test01 {
	public static void main(String[] args) {
		//할아버지 : 홍길동 70세 
		//할머니 : 김피카츄 65세 
		Person grandfather= new Person("홍길동", 70);
		Person grandmother = new Person("김피카츄", 65);
		//어머니 : 김피츄 35세
		//아버지 : 홍또도가스 40세 
		Person father= new Person("홍또도가스", 40);
		Person mother = new Person("김피츄", 35);
		//아들 : 홍뚜벅초 10세
		Person son = new Person("홍뚜벅초", 10);
		son.setFather(father);
		son.setMother(mother);
		//딸 : 홍푸린 5세 
		Person daughter = new Person("홍푸린", 5);
		//푸린객체는 뚜벅초 객체를 복사하여 구현하세요. (아버지, 어머니가 뚜벅초와 같아야 함 )
		//daughter.setFather(father);
		//daughter.setMother(mother);  //이거 쓰지말고
		son.copy(daughter); 
		//동일한 어머니, 아버지를 둔      뚜벅초, 푸린 생성 할 때
		System.out.println(son.getName()); //뚜벅초
		System.out.println(son.getAge()); // 10
		System.out.println(son.getFather().getName()); //홍뚜벅초
		System.out.println(son.getMother().getName()); //김피츄
		//푸린객체는 뚜벅초 객체를 복사하여 구현하세요. (아버지, 어머니가 뚜벅초와 같아야 함 )
		System.out.println(daughter.getName()); //홍푸린
		System.out.println(daughter.getAge()); //5
		System.out.println(daughter.getFather().getName()); //홍뚜벅초
		System.out.println(daughter.getMother().getName()); //김피츄
		
		//푸린(동생) 객체를 생성할 때 깊은 복사를 해야하는지 얕은 복사를 해야하는지 생각해보고
//			깊은복사를 해야한다. 얕은복사하면 이름과 나이까지 뚜벅초 & 10인 같은 값이 나온다.
		
	}
}
```
