### Day08_Quiz04
김병우님 도움 많이 받았어요!!ㅠㅠ

1. Scanner를 사용하여 6개의 데이터를 입력 받고, 이들을 nums 배열에 저장

2. 입력 받은 값 중, 20 이상 100 이하인 원소만 출력
		
3. 입력 받은 값 중, 최댓값과 최솟값을 출력
  	int max = nums[0];
		int min = nums[0];
  	(for문 사용)
		System.out.println("최댓값 : " + max);
		System.out.println("최댓값 : " + min);
		
4. 오름차순(작은->큰)으로 정렬하여 모든 원소를 출력  ==> 버블 정렬 알고리즘 검색해서 ... 

```java
package day08.homework;

import java.util.Scanner;

public class as {
public static void main(String[] args) {
	Scanner sc = new Scanner(System.in);
	int [] nums = new int [6];
	System.out.println("6개의 데이터 입력: ");
	for (int i = 0; i < nums.length; ++i) {
	nums [i] = sc.nextInt();
		
	}
	System.out.println("20이상 100이하의 수: ");
	for (int i : nums) {
		if (i >= 20 && i <= 100) { 
	System.out.println(i);
	}
		
	}
	
	int max = nums[0];
	int min = nums[0];
	for (int i = 0; i < nums.length; ++i) {
	if (max < nums[i]) {
		max = nums[i];
	}
	if (min >nums[i]) {
		min = nums[i];
	}
  }
	System.out.println("최대값: " + max);
	System.out.println("최소값: " + min);
	
	//버블 정렬 알고리즘...역시 인터넷...
	 System.out.println("\n 정렬: ");
     
     for(int i=0;i<nums.length-1;i++)
     {
         for(int j=0;j<nums.length-1-i;j++)
         {
             if(nums[j]>nums[j+1])
             {
                 int temp=nums[j];
                 nums[j]=nums[j+1];
                 nums[j+1]=temp;
             }
         }
     }
     for(int i:nums)
     {
         System.out.print(i+" ");

	
}
}
}

