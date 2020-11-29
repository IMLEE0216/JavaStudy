### CallBack

	1. 콜백 함수란?
	보통 호출자(caller)가 피호출자(callee)를 불러 함수의 기능을 수행하게 된다.
	하지만 이름대로 callback이란 피호출자(callee)가 호출자(caller)를 부르는 것을 의미한다.
	즉 사용자가 시스템에게 처리 요청을 하면 call이고 시스템이 사용자에게 처리 요청을 하면 callback이다. 
	
	호출자가 call한 기능을 수행하다가 어떠한 조건을 만족시키면 피호출자님께서 callback을 발생시키게 된다.

	예를들면... 1~11가지 더한다고 했을때 Max는 50인데 50을 넘으면 exceed 값을 콜백하는거 
	eg) Console에서 1~ 11까지 더하면서 나가다가 50이 넘으면 콜백한다 "더한 값은 66 초과 값은 16" 이런식으로?ㅋㅋ인터넷에서 예제 몇 개 봤습니다.ㅋㅋ





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
