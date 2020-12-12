### pokemon homework01


          1. Scanner(Jop) 를 사용하여 새 포켓몬의 이름, 레벨을 입력 받는다.
          공격력은 레벨의 0.5 배
          체력은 레벨의 100 배
          로 세팅하여 이를 DB에 저장 (INSERT)

```java
package day35.homework;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.text.SimpleDateFormat;

import javax.swing.JOptionPane;

public class Pokemon01 {

	String pkname = null;
	int level;
	int hp;
	double ap;

	public Pokemon01() {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		String date = sdf.format(System.currentTimeMillis());
		String url = "jdbc:mysql://127.0.0.1/testdb";
		String id = "testdba";
		String password = "test1234";
		PreparedStatement preparedStatement = null;
		Connection connection = null;

		String sql = "INSERT INTO pokemon(no, name, level, hp, ap, regdate) VALUES(?, ?, ?, ?, ?, ?)";
		try {

			Class.forName("com.mysql.cj.jdbc.Driver");

			connection = DriverManager.getConnection(url, id, password);

			// 쿼리문 준비
			preparedStatement = connection.prepareStatement(sql);

			pkname = JOptionPane.showInputDialog("포켓몬 이름");
			level = Integer.parseInt(JOptionPane.showInputDialog("레벨"));
			hp = level * 100;
			ap = level * 0.5;
			preparedStatement.setInt(1, 0);
			preparedStatement.setString(2, pkname);
			preparedStatement.setInt(3, level);
			preparedStatement.setInt(4, hp);
			preparedStatement.setDouble(5, ap);
			preparedStatement.setString(6, date);

			// 쿼리 실행
			preparedStatement.executeUpdate();

			JOptionPane.showMessageDialog(null, pkname + "  저장완료");

		} catch (SQLException e) {
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (NullPointerException e) {
			e.printStackTrace();
		} catch (NumberFormatException e) {
			e.printStackTrace();
		} finally {
			// 접속 종료
			try {
				if (preparedStatement != null)
					preparedStatement.close();
				if (connection != null)
					connection.close();
			} catch (SQLException e) {
				e.printStackTrace();
			}
		}

	}

	public static void main(String[] args) {
		new Pokemon01();

	}
}

```

### pokemon homework02


         2. 사용자에게 조회할 포켓몬의 이름을 입력 받고 해당 포켓몬의 정보를 DB에 조회한 뒤 출력
            없으면 '미등록 포켓몬'
          
```java
package day35.homework;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.swing.JOptionPane;

public class Pokemon02 {
   private static final String URL = "jdbc:mysql://127.0.0.1/testdb?useUnicode=true&characterEncoding=utf8";
   private static final String ID = "testdba";
   private static final String PASSWORD = "test1234";
   private Connection connection;
   private PreparedStatement preparedStatement;
   private ResultSet resultSet;

   public Pokemon02() throws SQLException {
	connection = DriverManager.getConnection(URL, ID, PASSWORD);
	String pkname = null;
	boolean b1 = true;
	while (b1) {
		pkname = JOptionPane.showInputDialog("포켓몬 검색");
		preparedStatement = connection.prepareStatement("SELECT * FROM pokemon WHERE NAME = " + "'" + pkname + "'");
		resultSet = preparedStatement.executeQuery(); // select 쓸 때
		loop: if (resultSet.next()) {
			int no = resultSet.getInt(1);
			String name = resultSet.getString(2);
			int level = resultSet.getInt(3);
			int hp = resultSet.getInt(4);
			double ap = resultSet.getDouble(5);
			String regdate = resultSet.getString(6);
				String message = no + ".  " + name + "\n레벨: " 
						    + level + "\n체력: " + hp
						    + "\n공격력: " + ap + "\n등록일 : "
					+ regdate;
			JOptionPane.showMessageDialog(null, message);
			break;
			} else if (pkname.equals(null)) {
			b1 = false;
		} else {
			JOptionPane.showMessageDialog(null, "미등록포켓몬");
			break loop;
		}
		}
	}

public static void main(String[] args) {
   try {
	new Pokemon02();
   } catch (SQLException e) {
		e.printStackTrace();
	}
   }
}

```

### pokemon homework03


           3. [선택문제] GUI 를 사용하여 
        	    (1)번문제를 Panel 형식으로 구현해보기 
                이름 : __________
                레벨 : __________  [계산] <--- '계산' 버튼 클릭되면 체력, 공격력이 자동으로 하단 label에 출력
 		            체력 : 
 		            공격력 : 	

```java
package day35.homework;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.sql.SQLIntegrityConstraintViolationException;
import java.text.SimpleDateFormat;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.JTextField;

import com.mysql.cj.exceptions.CJException;

public class Pokemon03GUI extends JFrame {
	private JButton btn1 = new JButton("계산");
	private JButton btn2 = new JButton("저장");
	private JLabel nameLabel = new JLabel("포켓몬 이름");
	private JLabel levelLabel = new JLabel("레벨");
	private JLabel hpLabel = new JLabel("체력");
	private JLabel apLabel = new JLabel("공격력");
	private JTextField nameField = new JTextField();
	private JTextField levelField = new JTextField();
	private JTextArea hpArea = new JTextArea();
	private JTextArea apArea = new JTextArea();
	private JPanel centerPanel = new JPanel();
	private JPanel southPanel = new JPanel();

	private void initCenterPanel() {
		centerPanel.setLayout(new GridLayout(4, 2));
		centerPanel.add(nameLabel);
		centerPanel.add(nameField);
		centerPanel.add(levelLabel);
		centerPanel.add(levelField);
		centerPanel.add(hpLabel);
		centerPanel.add(hpArea);
		centerPanel.add(apLabel);
		centerPanel.add(apArea);
		hpArea.setEditable(false);
		apArea.setEditable(false);
	}

private void initSouthPanel() {
	southPanel.setLayout(new FlowLayout());
	southPanel.add(btn1);
	southPanel.add(btn2);
	
	btn1.addActionListener(new ActionListener() {
		String name;
		int level;
			
		@Override
		public void actionPerformed(ActionEvent e) {
			try {
				name = nameField.getText();
				level = Integer.parseInt(levelField.getText());
				int hp = level * 100;
				double ap = level * 0.5;
				if (name.equals("")) {
					JOptionPane.showMessageDialog(null, "포켓몬 이름 입력하세요.");
				} 
				
				if (level <= 0) {
					JOptionPane.showMessageDialog(null, "레벨은 0 보다 위!");
				} else {
					hpArea.setText(Integer.toString(hp));
					apArea.setText(Double.toString(ap));
				}
			} catch (Exception e1) {
				e1.printStackTrace();
				JOptionPane.showMessageDialog(null, "레벨을 입력하세요.");
			}
			
		}
	});

	btn2.addActionListener(new ActionListener() {

		@Override
		public void actionPerformed(ActionEvent e) {
			if (nameField.getText().equals("") || levelField.getText().equals(Integer.toString(0)) || levelField.getText().equals("")) {
				JOptionPane.showMessageDialog(null, "저장 할 수 없음");
			} else if (Integer.parseInt(levelField.getText())*100 != Integer.parseInt(hpArea.getText())){
				JOptionPane.showMessageDialog(null, "계산 후 저장");
			} else {
				SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
				String date = sdf.format(System.currentTimeMillis());
				String url = "jdbc:mysql://127.0.0.1/testdb";
				String id = "testdba";
				String password = "test1234";
				PreparedStatement preparedStatement = null;
				Connection connection = null;
				
				String sql = "INSERT INTO pokemon(no, name, level, hp, ap, regdate) VALUES(?, ?, ?, ?, ?, ?)";
				
				try {
				Class.forName("com.mysql.cj.jdbc.Driver");
				
				connection = DriverManager.getConnection(url, id, password);
					
					preparedStatement = connection.prepareStatement(sql);
					preparedStatement.setInt(1, 0);
					preparedStatement.setString(2, nameField.getText());
					preparedStatement.setInt(3, Integer.parseInt(levelField.getText()));
					preparedStatement.setInt(4, Integer.parseInt(hpArea.getText()));
					preparedStatement.setDouble(5, Double.parseDouble(apArea.getText()));
					preparedStatement.setString(6, date);
					
					preparedStatement.executeUpdate();
					JOptionPane.showMessageDialog(null, nameField.getText() + "  저장완료");
				} catch (SQLException e1) {
					e1.printStackTrace();
					JOptionPane.showMessageDialog(null, "중복된 포켓몬");
				} catch (ClassNotFoundException e1) {
					e1.printStackTrace();
				} catch (NullPointerException e1) {
					e1.printStackTrace();
				} catch (NumberFormatException e1) {
					e1.printStackTrace();
					JOptionPane.showMessageDialog(null, "레벨 입력 후 계산을 누르세요.");
				} 
				finally {
					// 접속 종료
					try {
						if (preparedStatement != null)
							preparedStatement.close();
						if (connection != null)
							connection.close();
					} catch (SQLException e1) {
						e1.printStackTrace();
					}
				}
			}
			
		}
	});
}

	public Pokemon03GUI() {
		super("pokemonGUI");
		setSize(300, 200);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLocationRelativeTo(null);
		initCenterPanel();
		initSouthPanel();
		add(centerPanel, BorderLayout.CENTER);
		add(southPanel, BorderLayout.SOUTH);
		setVisible(true);
	}

	public static void main(String[] args) {
		new Pokemon03GUI();

	}
}
```
