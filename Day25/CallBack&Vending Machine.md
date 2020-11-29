### CallBack











### 자판기

         2. 동기 (synchronized) 사용하여 자판기 구현하기 
	          1) 자판기는 2개가 있다.
          	2) 사람쓰레드는 10개가 있다.
	          3) 자판기에서 음료를 뽑는 시간은 3초다.
	          4) 사람쓰레드는 1번 자판기를 우선적으로 선택하되 
           	    자판기가 사용중이라면 2번 자판기를 사용한다.
              	2번 자판기도 사용중이라면 1번 자판기로 가서 기다린다.
  
          	+ 1, 2 번 자판기 중 먼저 사용가능한 자판기를 선택하여 사용한다.
 
 ```java
package day25.homework;


class waitf {
	String name;
	private int queue;
	private int queueLimit;

public waitf (int num) {
	queue = queueLimit = num;
}
	
public synchronized void waitq() throws InterruptedException{
	while(queue == 0) {
		this.wait();
	}
	
	queue--;
}

public synchronized void waitl() throws InterruptedException {
	if (queue < queueLimit)queue++;
	this.notify();
	}
}

//===================================================================

class Person extends Thread {
	private waitf machine;
	
	public Person (waitf rr, String name) {
	this.setName(name);
	this.machine = rr;
	
	}

	@Override
	public void run() {
		String myname = this.getName();
		boolean ma = true;
		try {
			while (ma) {
				machine.waitq();
				System.out.println(myname+ "이(가) 자판기 앞에 있다.");
				Thread.sleep(3000);
				System.out.println(myname+ "이(가) 음료를 뽑고 갔다");
				machine.waitl();
				ma = false;
			}
		}catch(InterruptedException e) {
			e.printStackTrace();
		}
	}
}	



public class Homework01 {
public static void main(String[] args) {
	waitf machine = new waitf (2); //이것이 자판기 2개? 이름좀....ㅠㅠ

	Person [] arr = new Person[10]; //사람 10명
	for (int i = 0; i < arr.length; ++i) {
		arr[i] = new Person(machine, ("p" + i));
		arr[i].setName("사람" + (i+1));
		arr[i].start();
	}
	}
}
```
