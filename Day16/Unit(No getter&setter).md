### getter & setter 없이 만들기


```java
package day16.quiz;

public class Unit { // 부모 클래스
		String name;
		int hp, att; // 체력, 공격력
		boolean alive; // true:아직 살아있음 (선택사항)
		
		public Unit() {}
		public Unit(String name) {
			this.name = name;
		}
		public Unit(String name, int hp, int att) {
			this.name = name;
			this.hp = hp;
			this.att = att;
			this.alive = true;
		}
		
		public void isAlive() {
			alive = hp > 0 ? true : false;
		}
		public String getInfo() {
			return name + "\nhp: " + hp;
		}
		
		public void attack(Unit enemy) {
			
		}
		}
//==========================================================
class Sniper extends Unit{
	Sniper (){
		super("저격수", 400, 100);
	}
	
	@Override
	public void attack (Unit enemy) {
		boolean attk = Math.random() > 0.1? true :false;  
		if (attk) { 
			System.out.println("Sniper-----일반공격!");
			enemy.hp -= 100;
		} else {
			System.out.println("Sniper-----헤드샷!");
			enemy.hp = 0;
		}
	}
	
}
//=======================================================
class Tank extends Unit {
	Tank (){
		super("탱크" , 4000, 50);
	}
	
	@Override
	public void attack (Unit enemy) {
		boolean attk = Math.random() > 0.3? true :false;  
		if (attk) { 
			System.out.println("Tank-----일반공격!");
			enemy.hp -= 50;
		} else {
			System.out.println("Tank-----특수공격!");
			enemy.hp -= enemy.hp*0.3;
		}
	}
}
```

### 실행시키기 

```java
package day16.quiz;

public class Attack {
	public static void main(String[] args) {
		Unit [] units = new Unit [2];//0,1
		
		for (int i = 0; i < units.length; ++i) {
			switch (Math.random() > 0.5? 0 : 1) {
			
			case 0: {
				units[i] = new Tank();
				units[i].name = (i+1) + "번 Player Tank";
				System.out.println((i+1)+"번 Player Tank!!");
				break;
			}
			case 1: {
				units[i] = new Sniper();
				units[i].name = (i+1) + "번 Player Sniper";
				System.out.println((i+1)+"번 Player Sniper!!");
				break;
			}		
			}
		}
		
		System.out.println("\n+++++게임시작!!+++++\n");
		while (true) {
				if (units[0].hp > 0 && units[1].hp > 0) {
					units[0].attack(units[1]);
					units[1].attack(units[0]);
					System.out.println("\n======정보======\n" + units[0].getInfo() + "\n" 
										+ units[1].getInfo()+"\n===============\n");
					continue;
				}
				if (units[0].hp > 0) {
					System.out.println(units[0].name + "승리!!");
					break;
				} 
				if (units[1].hp > 0) {
					System.out.println(units[1].name + "승리!!");
					break;
				}	
			}
	}//main
}//class

```

###결과

      1번 Player Tank!!
      2번 Player Sniper!!

      +++++게임시작!!+++++

      Tank-----일반공격!
      Sniper-----일반공격!

      ======정보======
      1번 Player Tank
      hp: 3900
      2번 Player Sniper
      hp: 350
      ===============

      Tank-----일반공격!
      Sniper-----일반공격!

      ======정보======
      1번 Player Tank
      hp: 3800
      2번 Player Sniper
      hp: 300
      ===============

      Tank-----일반공격!
      Sniper-----일반공격!

      ======정보======
      1번 Player Tank
      hp: 3700
      2번 Player Sniper
      hp: 250
      ===============

      Tank-----일반공격!
      Sniper-----헤드샷!

      ======정보======
      1번 Player Tank
      hp: 0
      2번 Player Sniper
      hp: 200
      ===============

      2번 Player Sniper승리!!

