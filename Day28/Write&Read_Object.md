### Write & Read Object

          22 일 차 homework (영단어) 
             추가기능1) 프로그램이 종료 되면 map 객체를 words.w 에 저장 
   			                writeObject(Map)
             추가기능2) 프로그램이 실행 될때 words.w 에 저장된 map 객체를 꺼냄 
   		                 없는 경우 파일을 읽지 말고 map 객체 생성하여 프로그램 실행
   			                map = readObject() 1회
 	
  
 
```java
package day28.homework;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;

import java.util.ArrayList;
import java.util.List;
import java.util.Map.Entry;
import java.util.Set;
import java.util.TreeMap;

import javax.swing.JOptionPane;




public class Homework01 {

	private TreeMap<String, String> map = new TreeMap<>();
	
	private void save() {
	//현재 map을 word.w에 덮어씀
		try (FileOutputStream out = new FileOutputStream("word.w");
			ObjectOutputStream oOut = new ObjectOutputStream(out);) { //닫기까지 함
		
				
			
				oOut.writeObject(map);
				System.out.println("단어장 저장 완료");
			
		} catch (NullPointerException e) {
				return;
			} catch (IOException e) {
				e.printStackTrace();
			} 
			
	}
	
	
	@SuppressWarnings("unchecked")
	private void load() {
	//word.w에 readObject하여 그 객체를 map에 저장
	// FileNotFound 익셉션이 발생했다면 new TreeMap() 하여 map에 저장
		
		
		
		try (FileInputStream fIn = new FileInputStream("word.w"); 
				ObjectInputStream oIn = new ObjectInputStream(fIn);){ //닫기까지 함
			map = (TreeMap<String, String>)oIn.readObject();
			
			}catch (FileNotFoundException e) {
				map = new TreeMap<>();
			} catch (IOException e) {
				e.printStackTrace();
			} catch (ClassNotFoundException e) {
				e.printStackTrace();
			}
		} 
			

	
	private void menu1() { // 단어 추가
		
		String w, m;
		w = JOptionPane.showInputDialog("새 단어");
		m = JOptionPane.showInputDialog("[" + w + "]의 뜻");
		if (w == null || m == null) {
			JOptionPane.showMessageDialog(null, "메뉴로 돌아갑니다.");
		} else {
			w = w.trim();
			m = m.trim();
			map.put(w, m);
			JOptionPane.showMessageDialog(null, "저장 완료!");
		}		
	}

//====================================================================================================


	public Homework01() {
		String select;
		load();
		try {
			while (true) {
			select = JOptionPane.showInputDialog("1. 단어 추가 \n" 
							   + "2. 단어 검색 \n"
							   + "3. 모든 단어 보기 \n"
							   + "4. 퀴즈 \n"
							   + "0. 종료");
			if (select == null) {
				JOptionPane.showMessageDialog(null, "취소하셨습니다.");
				return;
			} else {
				 switch (select) {
				case "0": //영단어 저장이 됩니다.
					JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
					save();
					return;
				case "1":
					menu1();
					break;
				case "2":
					menu2();
					break;
				case "3":
					menu3();
					break;
				case "4":
					menu4();
					break;

				default:
					JOptionPane.showMessageDialog(null, "다시 입력하세요.");
					break;
				}
			}		
		}
		} catch (NullPointerException e) {
			e.printStackTrace();
		} 
		
		
	}

	public static void main(String[] args) {
		new Homework01();
	}
}
```
