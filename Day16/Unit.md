### Unit Tank&Sniper


       < Sniper VS Tank >
      - 저격수, 탱크 두 캐릭터 중 아무거나 랜덤하게 2개 생성
         (탱크 vs 탱크, 저 vs 탱, 저 vs 저)
       - 두 객체가 서로 죽을 때까지 서로 공격을 반복
       - 첫번째, 혹은 두번째 플레이어가 이겼는지 마지막 승자 출력! 
       e.g. 플레이어1(탱크)의 승리!
 
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
    //getter & setter
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public int getHp() {
			return hp;
		}
		public void setHp(int hp) {
			this.hp = hp > 0? hp: 0;
			setAlive();
		}
		public int getAtt() {
			return att;
		}
		public void setAtt(int att) {
			this.att = att;
		}
		public boolean isAlive() {
			return alive;
		}
		public void setAlive() {
			alive = hp > 0 ? true : false;
		}
		public String getInfo() {
			return name + "\nhp: " + hp;
		}
		
		public void attack(Unit enemy) {
			
		}
		}
```
      class Sniper extends Unit { // 자식 클래스
      객체 생성되면, 자동으로 name은 "저격수", hp는 400, att는 100
      attack 오버라이드 
      public void attack(Unit enemy) {
       1. 10% 확률로 헤드샷 (상대 즉사)
       2. 나머지 확률로 평타(일반 공격, 상대 hp를 100만큼 깎는다.)
	      }  }
  
```java
class Sniper extends Unit{
	Sniper (){
		super("저격수", 400, 100);
	}
	
	@Override
	public void attack (Unit enemy) {
		boolean attk = Math.random() > 0.1? true :false;  
		if (attk) { 
			System.out.println(getName() +"-----일반공격!");
			enemy.setHp(enemy.getHp() - getAtt());
		} else {
			System.out.println(getName() +"-----헤드샷!");
			enemy.setHp(0);
		}
	}	
}
```

      class Tank extends Unit {
      객체 생성되면, 자동으로 name은 "탱크", hp는 4000, att는 50
      attack 오버라이드 
	        1. 30% 확률로 상대의 hp 30% 감소
	        2. 나머지 확률로 평타(일반 공격, 상대 hp를 50만큼 깎는다.)
```java
class Tank extends Unit {
	Tank (){
		super("탱크" , 4000, 50);
	}
	
	@Override
	public void attack (Unit enemy) {
		boolean attk = Math.random() > 0.3? true :false;  
		if (attk) { 
			System.out.println(getName() + "-----일반공격!");
			enemy.setHp(enemy.getHp() - getAtt());
		} else {
			System.out.println(getName() + "-----특수공격!");
			enemy.setHp((int)(enemy.getHp()*0.7));
		}
	}
}
```
### 죽을때까지 실행시키기
      public class Quiz01 {
	      public static void main(String[] args) {
		     두 타입의 객체를 랜덤하게 2개 생성
		     무한 반복문을 사용하여 둘 중 하나가 죽을 때까지 서로를 공격
		     단, 죽은 객체가 공격하면 안됨
```java
public class Attack {
	public static void main(String[] args) {
		Unit [] units = new Unit [2];//0,1
		
		for (int i = 0; i < units.length; ++i) {
			switch (Math.random() > 0.5? 0 : 1) {
			
			case 0: {
				units[i] = new Tank();
				units[i].setName((i + 1) + "번  Tank");
				System.out.println((i+1)+"번 Player Tank!!");
				break;
			}
			case 1: {
				units[i] = new Sniper();
				units[i].setName((i + 1) + "번  Sniper");
				System.out.println((i+1)+"번 Player Sniper!!");
				break;
			}		
			}
		}
		
		System.out.println("\n+++++게임시작!!+++++\n");
		while (true) {
				if (units[0].getHp() > 0 && units[1].getHp() > 0) {
					units[0].attack(units[1]);
					units[1].attack(units[0]);
					System.out.println("\n======정보======\n" + units[0].getInfo() + "\n" 
                                + units[1].getInfo()+"\n===============\n");
					continue;
				}
				if (units[0].getHp() > 0) {
					System.out.println(units[0].getName() + "승리!!");
					break;
				} 
				if (units[1].getHp() > 0) {
					System.out.println(units[1].getName() + "승리!!");
					break;
				}	
			}
	}//main
}//class
```

### 결과

      1번 Player Tank!!
      2번 Player Sniper!!

      +++++게임시작!!+++++

      1번  Tank-----특수공격!
      2번  Sniper-----일반공격!

      ======정보======
      1번  Tank
      hp: 3900
      2번  Sniper
      hp: 280
      ===============

      1번  Tank-----일반공격!
      2번  Sniper-----일반공격!

      ======정보======
      1번  Tank
      hp: 3800
      2번  Sniper
      hp: 230
      ===============

      1번  Tank-----일반공격!
      2번  Sniper-----헤드샷!

      ======정보======
      1번  Tank
      hp: 0
      2번  Sniper
      hp: 180
      ===============

      2번  Sniper승리!!
