### Words_HashMap

        String menu = "1. 단어 추가\n" 
		    + "2. 단어 검색\n" 
		    + "3. 모든 단어 보기\n"
		    + "4. 퀴즈 풀기 \n"
		    + "0. 종료\n입력 : ";


        1 : 영단어, 그의 뜻(한글) 을 입력 받고 단어장(Map)에 저장
        2 : 영단어 입력 받고 그의 뜻을 출력. 없으면 "미등록 단어" 출력  (containsKey("apple")) 
        3 : for문 사용 
        4 : (선택문제) 
                      문제 : 뜻   / 답 : 영단어  
		        예) 사과(은)는 영어로? ==> 'home' 입력 ==> 땡!
		        문제는 랜덤하게 나와야 함. Map --> List 나 array 로 변경해야 함


```java
package day22.homework01;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map.Entry;
import javax.swing.JOptionPane;

public class Homework02 {
	public static void main(String[] args) {
		HashMap<String, String> words = new HashMap<>();
		String menu;
		String select;
		String w ;
		String k ;
		
		menu = "1. 단어 추가\n2. 단어 검색\n3. 모든 단어 보기\n4. 퀴즈 풀기\n0. 종료";
		loop: while(true) {
			select = JOptionPane.showInputDialog(menu);
			switch (select) {
			case "0":
				break loop;
			case "1": {
				if (null == words) {
				return;
				}
				w = JOptionPane.showInputDialog("영단어");
				k = JOptionPane.showInputDialog("단어 뜻");
				if (w.isEmpty() || k.isEmpty()) {
				JOptionPane.showMessageDialog(null, "등록 불가");
				break;
				} 
				words.put(w, k);
				JOptionPane.showMessageDialog(null, "등록 완료");
				break;
			}
			case "2": {
				String s = JOptionPane.showInputDialog("단어 검색");
				if (null == s) {
				JOptionPane.showMessageDialog(null, "취소하셨습니다.");
				break;
				}
				JOptionPane.showMessageDialog(null, words.containsKey(s)? words.get(s) : "미등록 단어");
				break;
				}
			case "3": {
				if (words.isEmpty()) {
					JOptionPane.showMessageDialog(null, "등록된 단어 없음");
					break;
				}
				StringBuffer message = new StringBuffer("단어 리스트\n");
				for(Entry<String, String> entry : words.entrySet()){
				String key = entry.getKey();
				String value = entry.getValue();
				message.append((key+ ":  " +value)  + "\n");
				}
				JOptionPane.showMessageDialog(null, message);
				break;
				}
			case "4": {
				List<String> list = new ArrayList<>(words.values());
				//https://surhommejk.tistory.com/222
				String q = list.get((int)(Math.random()*list.size()));
				String ans = JOptionPane.showInputDialog(q +"(은)는 영어로?");
				JOptionPane.showMessageDialog(null, q.equals(words.get(ans))? "정답!" : "오답!");
				break;
			}
			default:
				JOptionPane.showMessageDialog(null,"잘못된 입력입니다.\n다시 입력하세요.");
			}
		}//while
		JOptionPane.showMessageDialog(null, "프로그램 종료");
	}//main
}//class
```
