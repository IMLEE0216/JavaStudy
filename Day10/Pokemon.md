### Pokemon
      메인메서드 : Pokemon 객체 5개짜리 배열 1개 만들기 
			메뉴 (무한 while문 사용) 1. 포켓몬 등록
				                 2. 모든 포켓몬 보기
				                 3. 레벨업
				                 0. 종료
			
			loop:while(true){
				switch(select){
				case "0":
					break loop;
				}
			} 
	  1. 포켓몬 등록 - 포켓몬 이름, 레벨을 입력 받고 
		           체력은 레벨의 1000배, 공격은 레벨의 2배 (20% 확률로 3배) 
			    ==> 5마리 한꺼번에 진행  혹은 1마리씩 진행 
		2. 모든 포켓몬 보기
			배열에 담겨있는 모든 포켓몬의 모든 정보 출력
		3. 레벨업
			방법1. 배열에 담겨있는 모든 포켓몬의 레벨을 1 증가
			방법2. 인덱스 입력 받고 해당 포켓몬의 레벨을 1 증가
			방법3. 이름을 입력 받고 해당 포켓몬의 레벨을 1 증가
			      (없는 이름인 경우 '미등록 포켓몬') 
```java
package day10.homework;

import java.util.Scanner;
import javax.swing.JOptionPane;

public class Homework01 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		Pokemon [] pk;
		pk = new Pokemon [5]; // 배열 1개 만들기 - 5객체
		for (int i = 0; i < pk.length; ++i) {
			pk[i] = new Pokemon();
		}
		
		System.out.println("Pokemon 등록 먼저 해야 합니다.");
		
		while (true) {
			System.out.println( "Menu:\n 1: Poketmon 등록 \n 2: 모든포켓몬 보기 \n 3: 레벨업\n 
						     4: 개인 레벨업\n 5: 이름 레벨업\n 0:종료");   
			int num = sc.nextInt(); 
			
			switch(num) {
			//============================종료===============================
				case 0 : {
				System.out.println("종료");
				return;
				}
			//==========================정보입력하기============================
				case 1 : { 
				 for (int i = 0; i < pk.length; ++i) {
					 System.out.println ((i+1) + "번 포켓몬 이름 등록: ");
					 pk[i].pkname = sc.next();
					 System.out.println("포켓몬 레벨 입력: ");
					 pk[i].level = sc.nextInt();
					 pk[i].hp = pk[i].level*1000;
					 int p = (int)(Math.random()*10)+1;
					 if (p < 8) {
						 pk[i].power = pk[i].level*2; 
					 } else {
						 pk[i].power = pk[i].level*3;
					 }				
				 	 }
				 		break; 
				 	 }   
			//==========================정보 보기===============================
				 case 2: { //
				 for (int i =0; i <pk.length; ++i) {
					System.out.println("======" + (i+1)+ "번 포켓몬" + "=====" + "\n"
							+ "이름: " + pk[i].pkname + "\n" 
						 	+ "레벨: " + pk[i].level + "\n" 
							+ "체력: " + pk[i].hp + "\n" 
							+ "공격력: " + pk[i].power + "\n");
					} 
				 		break;
				 	} 
			//=============================레벨업=================================
				 case 3: {
				 
				 for (int i = 0; i < pk.length; ++i) {
				  pk[i].level ++;
				  
				  pk[i].hp = pk[i].level*1000;
					 int p = (int)(Math.random()*10)+1;
					 if (p < 8) {
						 pk[i].power = pk[i].level*2; 
					 } else {
						 pk[i].power = pk[i].level*3;
					 }	
					 
				  System.out.println(pk[i].pkname + " 레벨업!");
					}
				 break;
				 }
			//===========================번호레벨업===========================
				 case 4: {
					 System.out.println("레벨업 할 포켓몬 번호를 입력하세요");
					for (int i= sc.nextInt(); ;) {
					pk[i-1].level ++;
					
					pk[i-1].hp = pk[i-1].level*1000;
					int p = (int)(Math.random()*10)+1;
					if (p < 8) {
						 pk[i-1].power = pk[i-1].level*2; 
					} else {
						pk[i-1].power = pk[i-1].level*3;
					}	
					System.out.println((i)+"번 포켓몬 :" + pk[i-1].pkname + " 레벨업!");
					break;
					}
					
					}
			//===========================이름레벨업==========================
				  case 5: {
					 System.out.println("레벨업 할 포켓몬 이름을 입력하세요");
						String upname = sc.next();
						boolean find = false;
					 for (Pokemon e: pk) {
						if (e.pkname.equals(upname)) { //String 일때 ==은 안된다.
							++e.level;
							e.hp = e.level*1000;
							
							int p = (int)(Math.random()*10)+1;
							if (p < 8) {
								 e.power = e.level*2; 
							} else {
								e.power = e.level*3;
							}	
							System.out.println(e.pkname + " 레벨업!");
							find = true;
							break;
							
							
						} 
						}
					 if (!find) { //find==false
							System.out.println("미등록포켓몬");
							
						} 
					 break;
				 
					 
			}
		 } //switch
	}//while
	}// main
}//Class
```
