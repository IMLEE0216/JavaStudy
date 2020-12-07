### POS GUI


```java
package day29.homework;

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.FlowLayout;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.LayoutManager;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.text.DecimalFormat;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.HashMap;
import java.util.Locale;
import java.util.Map;
import java.util.Map.Entry;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;
import javax.swing.JTextArea;


class MyButton extends JButton {
	SimpleDateFormat df = new SimpleDateFormat("YYYYMMdd_HHmmss", Locale.KOREA);
	DecimalFormat dcf = new DecimalFormat("#,###");
	private String menuName;
	private int price;
	private JTextArea textArea;
	private JLabel label1;
	private static int total = 0;

	
	
	
	public MyButton(String menuName, int price, JTextArea textArea, JLabel label1) {
		super(menuName); // ??
		this.menuName = menuName;
		this.price = price;
		this.textArea = textArea;
		this.label1 = label1;
		this.addActionListener(listener);
		label1.setText("총액: " + dcf.format(total) + "원");
	
	}

	ActionListener listener = new ActionListener() {
		@Override
		public void actionPerformed(ActionEvent e) {
			total += price;
			label1.setText("총액: " + dcf.format(total) + "원");
			textArea.append(menuName + ":  " + price + "원    " + df.format(new Date()) + "\n");
			
			
			
		}
	};


}
public class Homework01 extends JFrame implements Runnable{
	SimpleDateFormat df = new SimpleDateFormat("YYYY/MM/dd_HH:mm:ss", Locale.KOREA);
	private Map<String, Integer> btn = new HashMap<>();

	private JPanel leftMenuPanel = new JPanel();

	private JPanel upMenuPanel = new JPanel();
	private JButton upbtn1 = new JButton("저장하기"); //
	private JButton upbtn2 = new JButton("불러오기"); //
	private JButton upbtn3 = new JButton("결제하기"); //

	private JPanel centerPanel = new JPanel();
	private JTextArea textArea = new JTextArea();

	private JPanel downPanel = new JPanel();
	private JLabel label1 = new JLabel();
	private JLabel label2 = new JLabel();

	


	@Override
	public void run() {
		label2.setText(df.format(new Date()));
		while(true) {
			
			try {
				Thread.sleep(1000);
				
				
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
		
	}
	
	
	private void menuPrice() {
		btn.put("아메리카노", 3000);
		btn.put("카푸치노", 3500);
		btn.put("카페라떼", 3500);
		btn.put("바닐라라떼", 4000);
		btn.put("카라멜마끼아또", 4000);
	}

	private void initLeftMenuPanel() {
		menuPrice();
		leftMenuPanel.setLayout(new GridLayout(btn.size(), 1));
		for (Entry<String, Integer> e : btn.entrySet()) {
			leftMenuPanel.add(new MyButton(e.getKey(), e.getValue(), textArea, label1));
		}

	}

	private void initCenterPanel() {
		centerPanel.setLayout(null);
		textArea.setBounds(0, 0, 1030, 660);
		textArea.setBackground(Color.WHITE);
		textArea.setFont(new Font("맑은고딕", Font.BOLD, 15));
		textArea.setEditable(false); // edit금지 글을 쓸 수 없음
		centerPanel.add(textArea);

	}

	private void initUpMenuPanel() {
		LayoutManager layout = new FlowLayout(FlowLayout.CENTER, 100, 20);
		upMenuPanel.add(upbtn1);
		upMenuPanel.add(upbtn2);
		upMenuPanel.add(upbtn3);
		upMenuPanel.setBackground(Color.WHITE);
		upMenuPanel.setLayout(layout);

	}

	private void initDownPanel () {
		downPanel.setLayout(new GridLayout(1, 2));
		label1.setHorizontalTextPosition(JLabel.LEFT);
		label2.setHorizontalAlignment(JLabel.RIGHT);
		downPanel.add(label1);
		downPanel.add(label2);

	}

	public Homework01() {
		super("과제");
		setSize(1200, 800);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLocationRelativeTo(null);// 가운데 띄우기

		LayoutManager layout = null;
		layout = new BorderLayout(10, 20);
		setLayout(layout);

		initLeftMenuPanel();
		initUpMenuPanel();
		initCenterPanel();
		initDownPanel();
		
		Thread thread = new Thread();
		thread.start();
		
		
//		==================================================================================
		upbtn1.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				try (FileOutputStream fOut = new FileOutputStream("sell.txt");
						ObjectOutputStream oOut = new ObjectOutputStream(fOut);){
						oOut.writeObject(textArea);
						textArea.setText(null);
				} catch (Exception a) {
					a.printStackTrace();
				}
				
			}
		});
		
		upbtn2.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				try (FileInputStream fIn = new FileInputStream("sell.txt"); 
						ObjectInputStream oIn = new ObjectInputStream(fIn);) { 	
					try {
						textArea = (JTextArea)oIn.readObject();
					} catch (ClassNotFoundException a) {
						a.printStackTrace();
					}
//					textArea.setText(oIn);

				} catch (FileNotFoundException a) {
					a.printStackTrace();
				} catch (IOException a) {
					a.printStackTrace();
				} 
				
			}
		});
		upbtn3.addActionListener(new ActionListener() {
			
			@Override
			public void actionPerformed(ActionEvent e) {
				JOptionPane.showMessageDialog(null, label1);
				try (FileOutputStream fOut = new FileOutputStream("sell.txt");
						ObjectOutputStream oOut = new ObjectOutputStream(fOut);){
						oOut.writeObject(textArea);
						textArea.setText(null);
				} catch (Exception a) {
					a.printStackTrace();
				}
				
			}
		});
		
//		==================================================================================
		
		add(leftMenuPanel, BorderLayout.WEST);
		add(upMenuPanel, BorderLayout.NORTH);
		add(downPanel, BorderLayout.SOUTH);
		add(centerPanel, BorderLayout.CENTER);
		setVisible(true);
	}

	public static void main(String[] args) {
		new Homework01();
	}
}

```
