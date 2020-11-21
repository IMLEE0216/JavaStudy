### D-day 계산기

        1. 디데이 계산기를 만드세요.
          시작년월일 입력 --> 목표 년월일 입력 ---> D-Day XX!!! 
          
```java
package day20.homework;

import java.time.LocalDate;
import java.time.temporal.ChronoUnit;
import java.util.Scanner;

public class TimeD_day {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		LocalDate temp;
		LocalDate target;
		while (true) {
			System.out.println("시작 년  월  일을 입력하세요: ");
			temp = LocalDate.of((sc.nextInt()), sc.nextInt(), sc.nextInt());
			System.out.println("목표 년  월  일을 입력하세요:");
			target = LocalDate.of(sc.nextInt(), sc.nextInt(), sc.nextInt());
			System.out.println("시작 날짜: " + temp);
			System.out.println("목표 날짜: " + target);
			
			// temp가 target보다 이후이다.
			if(temp.isAfter(target)) {
				System.out.println("시작이 목표보다 이후입니다.");
				System.out.println("다시 입력하세요");
				continue;
			}else {
				System.out.println("남은 일 : " + ChronoUnit.DAYS.between(temp, target));
			}// temp가 target보다 이전이다.
			break;
		} 
//		System.out.println("남은 년 : " + ChronoUnit.YEARS.between(temp, target));
//		System.out.println("남은 월 : " + ChronoUnit.MONTHS.between(temp, target));
	}
}
```
        시작 년  월  일을 입력하세요: 
        2020
        5
        9
        목표 년  월  일을 입력하세요:
        2022
        9
        29
        시작 날짜: 2020-05-09
        목표 날짜: 2022-09-29
        남은 일 : 873

### 달 출력

        2. 년, 월을 입력 받고 해당 월을 달력형태로 출력하세요. (토요일마다 줄바꿈이 일어나도록)  

```java
package day20.homework;

import java.util.Arrays;
import java.util.Calendar;
import java.util.Scanner;

public class Test02 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		Calendar cal = Calendar.getInstance();
		String[] days = {" 일", "월", "화", "수", "목", "금", "토"};
		
		System.out.println("년도를 입력하세요 : "); 
		int year = sc.nextInt(); //년도 
		System.out.println("월을 입력하세요 : "); 
		int month = sc.nextInt(); //월 
		cal.set(Calendar.YEAR, year); //입력받은 년도로 세팅 
		cal.set(Calendar.MONTH, month); //입력받은 월로 세팅

		System.out.println("---------["+year+"년 "+month+"월]---------");
		System.out.println(Arrays.toString(days).replaceAll("," , "     ")); //Arrays는 java.util
		
		cal.set(year,month-1,1); //입력받은 월의 1일로 세팅 //month는 0이 1월이므로 -1을 해준다
		int end = cal.getActualMaximum(Calendar.DATE); //해당 월 마지막 날짜
		int dayOfWeek = cal.get(Calendar.DAY_OF_WEEK); //해당 날짜의 요일
		
		for(int i=1; i<=end; i++) {
			if(i==1) {
				for(int j=1; j<dayOfWeek; j++) {
					System.out.print("    ");
				}
			}
			if(i<10) { //한자릿수일 경우 공백을 추가해서 줄맞추기
				System.out.print(" ");
			}
			System.out.print(" "+i+" ");
			if(dayOfWeek%7==0) { //한줄에 7일씩 출력
				System.out.println();
			}
			dayOfWeek++;
		}
	}
}
```

        년도를 입력하세요 : 
        2002
        월을 입력하세요 : 
        8
       ---------[2002년 8월]---------
       [ 일  월  화  수  목  금  토]
                         1   2   3 
         4   5   6   7   8   9  10 
        11  12  13  14  15  16  17 
        18  19  20  21  22  23  24 
        25  26  27  28  29  30  31

