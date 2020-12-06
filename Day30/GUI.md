### 길찾기

```java
package day30.homework;

import java.awt.Color;
import java.awt.Graphics;
import java.awt.GridLayout;
import java.awt.Image;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.lang.Thread.State;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class Homework01 extends JFrame{
	
	static class MyButton extends JButton {
		private int stat;
		
		public MyButton(int stat) {
			this.stat = stat;
		}
		int getStat() {
			return stat;
		}
	}
	
	private static final int ROAD = 0;
	private static final int WALL = 1;
	private static final int START = 2;
	private static final int END = 3;
	private static final int CURRENT = 4;
	
	private static final int ROW = 8;
	private static final int COL = 8;
	
	private int x = 0;
	private int y = 0;
	
	private static final Color[] COLOR = {
			new Color(250, 237, 239),
			new Color(33, 32, 32),
			new Color(235, 52, 82),
			new Color(74, 52, 237),
			new Color(207, 52, 235)
	};
	
	private static final int[][] MAP = {
			{ START, ROAD, WALL, WALL, WALL, ROAD, WALL, ROAD },
			{ ROAD, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD },
			{ WALL, WALL, WALL, ROAD, ROAD, ROAD, ROAD, ROAD },
			{ WALL, ROAD, ROAD, ROAD, WALL, ROAD, WALL, ROAD },
			{ WALL, WALL, WALL, ROAD, WALL, WALL, WALL, ROAD }, 
			{ ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, WALL, END },
			{ ROAD, WALL, WALL, WALL, WALL, WALL, WALL, ROAD }, 
			{ ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD, ROAD },
	};
	
	
	private MyButton[][] btnMap;
	private void initMap() {
		btnMap = new MyButton[ROW][COL];
		for(int i = 0; i < ROW; ++i) {
			for(int j = 0; j < COL; ++j) {
				MyButton btn = new MyButton(MAP[i][j]);
				btn.setBackground(COLOR[MAP[i][j]]);
				btn.setEnabled(false);
				btnMap[i][j] = btn;
			}
		}
	}
	
	public Homework01() {
		initMap();
		setSize(500,500);
		setLocationRelativeTo(null);
		setLayout(new GridLayout(ROW, COL));
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		
		for(MyButton[] btns : btnMap) {
			for(MyButton btn : btns) {
				add(btn);
			}
		}
		
		
		addKeyListener(new KeyListener() {
			
			@Override
			public void keyTyped(KeyEvent e) {
			}
			
			@Override
			public void keyReleased(KeyEvent e) {
			}
			
			@Override
			public void keyPressed(KeyEvent e) {
				switch (e.getKeyCode()) {
				case KeyEvent.VK_UP:
					System.out.println("UP");
					y = y-1;
					if(btnMap[y][x].stat==0) {
						btnMap[y][x].stat = 2;
						btnMap[y][x].setBackground(COLOR[START]);
						btnMap[y+1][x].stat = 0;
						btnMap[y+1][x].setBackground(COLOR[ROAD]);
					} else if (btnMap[y][x].stat == 1){
						y = y+1;
						System.out.println("벽");
					} else if (btnMap[y][x].stat == 3) {
						JOptionPane.showMessageDialog(null, "축축");
						System.exit(0);
					}
					break;
				case KeyEvent.VK_DOWN:
					System.out.println("DOWN");
					y = y+1;
					if(btnMap[y][x].stat==0) {
						btnMap[y][x].stat = 2;
						btnMap[y][x].setBackground(COLOR[START]);
						btnMap[y-1][x].stat = 0;
						btnMap[y-1][x].setBackground(COLOR[ROAD]);
					} else if (btnMap[y][x].stat == 1){
						y = y-1;
						System.out.println("벽");
					} else if (btnMap[y][x].stat == 3) {
						JOptionPane.showMessageDialog(null, "축축");
						System.exit(0);
					}
					break;
				case KeyEvent.VK_LEFT:
					System.out.println("LEFT");
					x = x-1;
					if(btnMap[y][x].stat==0) {
						btnMap[y][x].stat = 2;
						btnMap[y][x].setBackground(COLOR[START]);
						btnMap[y][x+1].stat = 0;
						btnMap[y][x+1].setBackground(COLOR[ROAD]);
					} else if (btnMap[y][x].stat == 1){
						x = x+1;
						System.out.println("벽");
					} else if (btnMap[y][x].stat == 3) {
						JOptionPane.showMessageDialog(null, "축축");
						System.exit(0);
					}
					break;
				case KeyEvent.VK_RIGHT:
					System.out.println("RIGHT");
					x = x+1;
					if(btnMap[y][x].stat==0) {
						btnMap[y][x].stat = 2;
						btnMap[y][x].setBackground(COLOR[START]);
						btnMap[y][x-1].stat = 0;
						btnMap[y][x-1].setBackground(COLOR[ROAD]);
					} else if (btnMap[y][x].stat == 1){
						x = x-1;
						System.out.println("벽");
					} else if (btnMap[y][x].stat == 3) {
						JOptionPane.showMessageDialog(null, "축축");
						System.exit(0);
					}
					break;

				default:
					break;
				}
				
			}
			
		});
		
		setVisible(true);
	}
	
	
	
	public static void main(String[] args) {
		new Homework01();
	}
}

```
