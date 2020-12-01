### Writer


         Quiz01 
          -> 2단.txt ~ 9단.txt 구구단 텍스트 파일 생성  
  
  ```java
  public class Quiz01 {
	public static void main(String[] args) {
		FileWriter danWriter = null;
		try {
			for (int i = 2; i<10; ++i ) {
				danWriter = new FileWriter(i + "단.txt");
				for (int j = 1; j<10; ++j) {
					danWriter.write(i + "X" + j + "=" + i*j + "\n");	
				}
				danWriter.close();
				System.out.println("파일 저장 완료");
			}
		
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if (null!=danWriter) {
					danWriter.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}	
	}
}
```

### Writer w/ Thread


       Quiz01 
        -> 2단.txt ~ 9단.txt 구구단 텍스트 파일 생성  
 
        추가 문제 
 
        class GugudanOutThread extends Thread {
	        private int dan;
	      public GugudanOutThread(int dan) {
	        // TODO Auto-generated constructor stub
	      }
	        @Override
	      public void run() {
 		      // 파일 열기
 		      // 파일 쓰기
 		      // 파일 닫기 *	}
        }
        public class Quiz01 {
  	    public static void main(String[] args) {
 		    GugudanOutThread[] threads = new GugudanOutThread[8];
 	      }
        }
       
```java
//요게 맞는지 모르겠네요 ㅋㅋㅋ
class GugudanOutThread extends Thread {
	private int dan;
	public GugudanOutThread (int dan) {
		this.dan = dan;
	}
	
	public void run() {
		FileWriter danWriter = null;
		try {
			danWriter = new FileWriter(dan + "단.txt");
				for (int j = 1; j<10; ++j) {
					danWriter.write(dan + "X" + j + "=" + dan*j + "\n");	
				}
				System.out.println("파일 저장 완료");
				
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if (null!=danWriter) {
					danWriter.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	};
	}


public class Test01 {
	public static void main(String[] args) {
		GugudanOutThread[] threads = new GugudanOutThread[8];
			for (int i = 0; i < threads.length; ++i) {
				threads[i] = new GugudanOutThread(i+2);
				threads[i].start();
			}	
  }	
}
  
```


### Reader 

       Quiz02
  	    ->사용자에게 '단'을 입력 받아 해당 구구단 txt 파일을 열고,
  		    그 내용을  JOp 으로 출력
          
```java

package day27.quiz.java.io;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.io.Reader;
import java.util.Scanner;

import javax.swing.JOptionPane;

  

 
public class Quiz02 {
	public static void main(String[] args) {
		
		FileReader danReader = null;
		
		String dan = JOptionPane.showInputDialog("원하시는 단을 입력하세요");
		
		try {
			danReader = new FileReader(dan + "단.txt");
			
			
			StringBuffer sb = new StringBuffer();
			Scanner sc = new Scanner(danReader);
			while (sc.hasNext()) {
				sb.append(sc.nextLine() + "\n");
				
				
			}
			JOptionPane.showMessageDialog(null, sb);
			
			
		} catch (FileNotFoundException e) {
			JOptionPane.showMessageDialog(null, "파일을 찾을수 없습니다.");
			
	    } catch (IOException e) {
			e.printStackTrace();
			
		} finally {
			try {
				if (null != danReader) {
					danReader.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
}
```

### Log file


         Quiz03 
          -> 사용자에게 exit를 입력 받을때까지 모든 문자열을 JOp으로 입력받고 
  		      exit를 입력하면 YYYYMMdd_HHmmss.txt 형식으로 log파일을 생성하여 
  	      	사용자가 입력한 모든 문자열 저장
              
 ```java
 package day27.quiz.java.io;

import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

import javax.swing.JOptionPane;


public class Quiz03 {
	public static void main(String[] args) {
		SimpleDateFormat dateFormat = new SimpleDateFormat("YYYYMMdd_HHmmss", Locale.KOREA);;
		FileWriter writer = null;
		try { 
			writer = new FileWriter(dateFormat.format(new Date()) + ".txt" , true);
			while (true) {
				try {
					String rand = JOptionPane.showInputDialog("아무거나 기입\n");
					
					
					if (rand.contains("exit")) {
						JOptionPane.showMessageDialog(null, "프로그램 종료");
						return;
					
					} else {
						writer.write(rand + "\n");
					}
				
				} catch (NullPointerException e) {
					JOptionPane.showMessageDialog(null, "취소하셨습니다");
					return;
				}
			}
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				if (null != writer) {
					writer.close();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}	
	}
}
```

  
  
  
