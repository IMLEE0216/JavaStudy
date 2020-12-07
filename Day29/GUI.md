### POS GUI


```java
package day29.homework;

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.text.DecimalFormat;
import java.text.SimpleDateFormat;
import java.util.Scanner;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextArea;
import javax.swing.SwingConstants;

class MyButton01 extends JButton {
	private String menuName;
	private int price;

	MyButton01(String menuName, int price) {
		super(menuName);
		this.menuName = menuName;
		this.price = price;
	}

	public String getMenuName() {
		return menuName;
	}

	public int getPrice() {
		return price;
	}
	
	public String toString() {
		SimpleDateFormat sdf = new SimpleDateFormat("HH:mm:ss");
		return String.format("%-30s%-10s%s\n", menuName, new DecimalFormat("#,###").format(price), sdf.format(System.currentTimeMillis()));
	}
	
}

public class Homework01 extends JFrame implements Runnable, ActionListener{  

	private static final int NUMBER_MENU = 5;
	
	private static final String[] NAMES_MENU = {"아메리카노", "카페라떼", "카푸치노", "바닐라라떼", "카라멜 마끼아또"};
	private static final int[] PRICES_MENU = {3000, 3500, 3800, 4200, 4500};
	
	
	private JButton saveBtn, loadBtn, payBtn;
	private MyButton01[] coffeeBtns = new MyButton01[NUMBER_MENU];
	private JTextArea textArea;
	private JLabel totalLabel;
	private JLabel timeLabel;
	
	private int totalPrice = 0;
	
	
	@Override
	public void run() {
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		while(true) {
			
			timeLabel.setText(sdf.format(System.currentTimeMillis()));
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
	
	@Override
	public void actionPerformed(ActionEvent e) {
		MyButton01 btn = (MyButton01)e.getSource();
		textArea.setText(textArea.getText() + btn.toString());
		totalPrice += btn.getPrice();
		totalLabel.setText("총 결제액 : " +  new DecimalFormat("#,###").format(totalPrice) +"원");
	}
	
	
	
	private JPanel initNorth() { // 저장하기, 불러오기, 결제하기
		JPanel panel = new JPanel();
		panel.setLayout(new FlowLayout());
		
		saveBtn = new JButton("저장하기");
		loadBtn = new JButton("불러오기");
		payBtn = new JButton("결제하기");
		
		panel.add(saveBtn);
		panel.add(loadBtn);
		panel.add(payBtn);
		
		saveBtn.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				FileWriter fWriter = null;
				try {
					
					fWriter = new FileWriter("sell.txt", true);
					fWriter.append(textArea.getText());
					fWriter.append(new DecimalFormat("#,###").format(totalPrice) +"\n");
					JOptionPane.showMessageDialog(null, "저장완료");
					textArea.setText(null);
					totalPrice = 0;
				} catch (IOException e1) {
					e1.printStackTrace();
				} finally {
					try {
						if(fWriter != null)
							fWriter.close();
					}catch (Exception e1) {
			
						e1.printStackTrace();
					}
					
				}
				
				
			}
		});
		
		loadBtn.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				FileReader fReader = null;
				Scanner sc = null;
				StringBuffer sb = new StringBuffer();
				try {
					fReader = new FileReader("sell.txt");
					sc = new Scanner(fReader);
					while (sc.hasNext()) {
						sb.append(sc.nextLine() + "\n");
					}
					textArea.setText(sb.toString());
					
				}catch (Exception e1) {
					e1.printStackTrace();
				} finally {
					try {
						if (sc != null)
							sc.close();
						if (fReader != null)
							fReader.close();
					} catch (IOException e1) {
						e1.printStackTrace();
					}
				}
			}
		});
		
		payBtn.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				FileWriter fWriter = null;
				try {
					
					fWriter = new FileWriter("sell.txt", true);
					fWriter.append(textArea.getText());
					fWriter.append(new DecimalFormat("#,###").format(totalPrice) +"\n");
					JOptionPane.showMessageDialog(null, totalPrice + "원   저장완료");
					textArea.setText(null);
					totalPrice = 0;
				} catch (IOException e1) {
					e1.printStackTrace();
				} finally {
					try {
						if(fWriter != null)
							fWriter.close();
					}catch (Exception e1) {
						e1.printStackTrace();
					}
					
				}
			}
		});
		return panel;
	}

	private JPanel initWest() { // 메뉴버튼
		JPanel panel = new JPanel();
		panel.setLayout(new GridLayout(NUMBER_MENU, 1));
		for(int i = 0; i < coffeeBtns.length; ++i) {
			coffeeBtns[i] = new MyButton01(NAMES_MENU[i], PRICES_MENU[i]);
			coffeeBtns[i].addActionListener(this);
			panel.add(coffeeBtns[i]);
			
		}
		return panel;
	}

	private JPanel initCenter() { // 주문 내역
		JPanel panel = new JPanel();
		panel.setLayout(new GridLayout(1,1));
		textArea = new JTextArea();
		textArea.setEditable(false);
		panel.add(textArea);
		return panel;
	}

	private JPanel initSouth() { // 총 결제액, 시간
		JPanel panel = new JPanel();
		panel.setLayout(new GridLayout(1, 2));
		
		totalLabel = new JLabel("총 결제액 : 0원");
		totalLabel.setFont(new Font(Font.SANS_SERIF, Font.BOLD, 24));
		
		timeLabel = new JLabel("2020-12-07 13:25:43");
		timeLabel.setFont(new Font(Font.SANS_SERIF, Font.BOLD, 24));
		timeLabel.setHorizontalAlignment(SwingConstants.RIGHT);
		
		panel.add(totalLabel);
		panel.add(timeLabel);
		return panel;
	}

	public Homework01() {
		super("커피 주문 관리 프로그램");
		
		setSize(1200, 800);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setLocationRelativeTo(null);
		
		setLayout(new BorderLayout());
		
		add(initNorth(), BorderLayout.NORTH);
		add(initCenter(), BorderLayout.CENTER);
		add(initSouth(), BorderLayout.SOUTH);
		add(initWest(), BorderLayout.WEST);
		
		
		new Thread(this).start();
		setVisible(true);
	}

	public static void main(String[] args) {
		new Homework01();
	}
}


```
