### JOp pokemon homework


```java
package day36.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import javax.swing.JOptionPane;

public class Test01 {
	private static final String URL = "jdbc:mysql://127.0.0.1/testdb?useUnicode=true&characterEncoding=utf8";
	private static final String ID = "testdba";
	private static final String PASSWORD = "test1234";
	private Connection connection;
	private PreparedStatement preparedStatement;
	private ResultSet resultSet;
	String sql;

	public Test01() {
		String menu = "1. 포켓몬 추가 \n" 
                + "2. 번호로 검색 \n" 
                + "3. 이름으로 검색 \n" 
                + "4. 포켓몬 삭제 \n" // 이름으로 삭제
		+ "5. 레벨업 \n" // 이름으로 레벨업
		+ "6. 모두 레벨업 \n" 
                + "7. 모든 포켓몬 보기\n" 
                + "0. 종료";

		menu: while (true) {
			String select = JOptionPane.showInputDialog(menu);
			switch (select) {
			case "0":
				JOptionPane.showMessageDialog(null, "프로그램을 종료합니다.");
				break menu;
			case "1":
				menu01();
				break;
			case "2":
				menu02();
				break;
			case "3":
				menu03();
				break;
			case "4":
				menu04();
				break;
			case "5":
				menu05();
				break;
			case "6":
				menu06();
				break;
			case "7":
				getCurrentPokemons();
				break;
			default:
				JOptionPane.showMessageDialog(null, "다시 입력하세요.");
				break;
			}
		}
	}

	private void menu01() { // 포켓몬 추가
		String url = "jdbc:mysql://127.0.0.1/testdb";
		preparedStatement = null;
		connection = null;

		while (true) {
			try {
				String pkname = JOptionPane.showInputDialog("포켓몬 이름").trim();
				if (pkname.isEmpty()) {
					JOptionPane.showMessageDialog(null, "포켓몬 이름을 입력하세요.");
					break;
				}

				int level = Integer.parseInt(JOptionPane.showInputDialog("레벨"));
				if (level <= 0) {
					JOptionPane.showMessageDialog(null, "정수 값의 레벨을  입력하세요.");
					break;
				}

				int hp = level * 100;
				double ap = level * 0.5;
				sql = "INSERT INTO pokemon(no, name, level, hp, ap, regdate) VALUES(?, ?, ?, ?, ?, DEFAULT)";

				Class.forName("com.mysql.cj.jdbc.Driver");

				connection = DriverManager.getConnection(url, ID, PASSWORD);

				preparedStatement = connection.prepareStatement(sql);
				preparedStatement.setInt(1, 0);
				preparedStatement.setString(2, pkname);
				preparedStatement.setInt(3, level);
				preparedStatement.setInt(4, hp);
				preparedStatement.setDouble(5, ap);

				preparedStatement.executeUpdate();

				JOptionPane.showMessageDialog(null, pkname + "  저장완료");
				break;
			} catch (SQLException e) {
				JOptionPane.showMessageDialog(null, "중복된 포켓몬");
				e.printStackTrace();
			} catch (NullPointerException e) {
				e.printStackTrace();
			} catch (NumberFormatException e) {
				JOptionPane.showMessageDialog(null, "정수 값의 레벨 입력");
				break;
//				e.printStackTrace();
			} catch (ClassNotFoundException e) {
				e.printStackTrace();
			} finally {
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
	} // menu01

private void menu02() { // 번호로 검색
	try {
		connection = DriverManager.getConnection(URL, ID, PASSWORD);

		while (true) {
			int num = Integer.parseInt(JOptionPane.showInputDialog("검색 포켓몬의 번호를 입력하세요."));
			sql = "SELECT * FROM pokemon WHERE no = " + num;
			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery();

			if (resultSet.next()) {
				String name = resultSet.getString(2);
				int level = resultSet.getInt(3);
				int hp = resultSet.getInt(4);
				double ap = resultSet.getDouble(5);
				String regdate = resultSet.getString(6);

				String message = name + "\n레벨: " + level + "\n체력: " 
						+ hp + "\n공격력: " + ap + "\n등록일 : " + regdate;

				JOptionPane.showMessageDialog(null, message);
				break;

			} else {
				JOptionPane.showMessageDialog(null, "없는 포켓몬 번호");
				break;
			}
		}
	} catch (SQLException e) {
		e.printStackTrace();
	} catch (NumberFormatException e) {
		JOptionPane.showMessageDialog(null, "메뉴로 돌아갑니다.");
		return;
//		e.printStackTrace();
	}
} // menu02

private void menu03() { // 이름으로 검색
	try {
		connection = DriverManager.getConnection(URL, ID, PASSWORD);
		while (true) {
			String sName = JOptionPane.showInputDialog("검색 포켓몬의 이름을 입력하세요.").trim();
			sql = "SELECT * FROM pokemon WHERE name = " + "'" + sName + "'";
			preparedStatement = connection.prepareStatement(sql);
			resultSet = preparedStatement.executeQuery();

			if (resultSet.next()) {
				int no = resultSet.getInt(1);
				String name = resultSet.getString(2);
				int level = resultSet.getInt(3);
				int hp = resultSet.getInt(4);
				double ap = resultSet.getDouble(5);
				String regdate = resultSet.getString(6);

				String message = no + ".  " + name + "\n레벨: " + level + "\n체력: " 
						+ hp + "\n공격력: " + ap + "\n등록일 : "
						+ regdate;

				JOptionPane.showMessageDialog(null, message);
				break;

			} else if (sName.isEmpty()) {
				JOptionPane.showMessageDialog(null, "다시 입력하세요.");
				break;

			} else {
				JOptionPane.showMessageDialog(null, "없는 포켓몬 번호");
				break;
			}
		}
	} catch (SQLException e) {
		e.printStackTrace();
	} catch (NullPointerException e) {
		e.printStackTrace();
	}
} // menu03

private void menu04() { // 포켓몬 삭제
	try {
		connection = DriverManager.getConnection(URL, ID, PASSWORD);
		String sName = JOptionPane.showInputDialog("삭제 포켓몬의 이름을 입력하세요.").trim();
		String sql1 = "SELECT * FROM pokemon WHERE name = " + "'" + sName + "'";
		preparedStatement = connection.prepareStatement(sql1);
		resultSet = preparedStatement.executeQuery();
			
		resultSet.next();
		if (sName.isEmpty()) {
			JOptionPane.showMessageDialog(null, "다시 입력하세요.");
			return;
		}
			
		if (resultSet.getString(2).equals(sName)) {
			sql = "DELETE FROM pokemon WHERE name = " + "'" + sName + "'";
			preparedStatement = connection.prepareStatement(sql);
			int n = preparedStatement.executeUpdate();
			JOptionPane.showMessageDialog(null, sName + " 정보 삭제 완료");
		} 
			
		getCurrentPokemons();

	} catch (SQLException e) {
		JOptionPane.showMessageDialog(null, "미등록 포켓몬 입니다.");
		return;
	} catch (NullPointerException e) {
		e.printStackTrace();
	}
} // menu04

private void menu05() { // 레벨업 이름으로
	try {
		connection = DriverManager.getConnection(URL, ID, PASSWORD);
			
		String sName = JOptionPane.showInputDialog("삭제 포켓몬의 이름을 입력하세요.").trim();
		String sql1 = "SELECT * FROM pokemon WHERE name = " + "'" + sName + "'";
		preparedStatement = connection.prepareStatement(sql1);
		resultSet = preparedStatement.executeQuery();
			
		resultSet.next();
		if (sName.isEmpty()) {
			JOptionPane.showMessageDialog(null, "다시 입력하세요.");
			return;
		}
			
		if (resultSet.getString(2).equals(sName)) {
			sql = "UPDATE pokemon SET LEVEL = LEVEL + 1 WHERE NAME = " + "'" + sName + "'";
			preparedStatement = connection.prepareStatement(sql);
			int n = preparedStatement.executeUpdate();
			JOptionPane.showMessageDialog(null, sName + " 레벨업 완료");
		} 

			
	} catch (SQLException e) {
		JOptionPane.showMessageDialog(null, "미등록 포켓몬 입니다.");
		return;
	}
}// menu05

private void menu06() { // 모두 레벨업
	try {
		connection = DriverManager.getConnection(URL, ID, PASSWORD);
		sql = "UPDATE pokemon SET LEVEL = LEVEL + 1 WHERE LEVEL > 0";
		preparedStatement = connection.prepareStatement(sql);
		int n = preparedStatement.executeUpdate();
		JOptionPane.showMessageDialog(null, "모든 포켓몬 레벨업 완료");
		getCurrentPokemons();
	} catch (SQLException e) {
		e.printStackTrace();
	}
}// menu06

private String getCurrentPokemons() { //포켓몬 현황
		
	StringBuilder message = new StringBuilder("==== < 포켓몬 현황 > ====\n");
	String sql = "SELECT * FROM pokemon";
	try {
		connection = DriverManager.getConnection(URL, ID, PASSWORD);
		preparedStatement = connection.prepareStatement(sql);
		resultSet = preparedStatement.executeQuery();
		while(resultSet.next()) {
			message.append(resultSet.getString(2))
					.append(" LV.").append(resultSet.getInt(3))
					.append(" HP/AP. ").append(resultSet.getInt(4))
					.append("/").append(resultSet.getInt(5))
					.append("[").append(resultSet.getString(6)).append("]\n");
		}
		JOptionPane.showMessageDialog(null, message.toString());
	} catch(Exception e) {
		e.printStackTrace();
	}
	
	return message.toString();
}
public static void main(String[] args) {
	new Test01();
}
}
```
