### Day08_Quiz1 

```java
  JOp 활용하여 국단 게임 만들기 (제어문 최종 문제)
  규칙 : 1. 사용자에게 원하는 판 수를 입력 받는다.
         2. 입력 받은 판 수 만큼 구구단 문제를 낸다. 
         3. 정답 시 100점, 오답일 경우 -10점. 
         4. 모든 횟수가 종료되면 총점을 출력한다. 
         5. 정답률을 퍼센티지로 출력한다.(소숫점은 생략한다.)
         6. 정답률이 80% 이상이면 "win"을, 그렇지 않으면 "lose"를 출력한다.

package day08.homework;

import java.util.Scanner;

import javax.swing.JOptionPane;


public class Homework01 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int problem;
		int score = 0;
				
		String pro = JOptionPane.showInputDialog(null, "몇 판? : ");
		problem = Integer.parseInt(pro); // 판수 입력 ***** 매우 중요 
		
		for (int i = 1; i <= problem; ++i) {
			int n1 = (int)(Math.random()*8)+2 ;
			int n2 = (int)(Math.random()*9)+1 ;
			int answer = n1*n2;
		String ans = JOptionPane.showInputDialog(null, n1 +"X" + n2 + "= ? ");
		answer = Integer.parseInt(ans); //*****
		
		if (answer == n1*n2) {
			score += 100;
		} else 
			score -= 10;
		
		}
		int avg = score/problem;
		JOptionPane.showMessageDialog(null, "총: " + score);
		JOptionPane.showMessageDialog(null, "정답률" + (int) avg + "%");
		JOptionPane.showMessageDialog(null, avg > 80? "WIN!!" : "LOSE");
		
	}
}

```
