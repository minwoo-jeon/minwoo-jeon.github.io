---
title: "[Java] 입출력 Scanner vs Bufferedreader 차이"
excerpt: " 자바 입출력 Scanner와 Bufferedreader 차이 구별하기"

categories:
  - Java
tags:
  - [tag1, tag2]

permalink: /java/java7/

toc: true
toc_sticky: true


date: 2024-01-17
last_modified_at: 2024-01-17
---

## 📌Scanner vs Bufferedreader 차이

### ✅Scanner 

Scanner는 입력 받을 떄 정수 값,소수 갑스,문자 데이터도 구분지어 읽어들일 수있다.

즉 직관적이고 사용하기 편리하다는 장점이있다.

그렇치만 키보드의 입력이 키를 누르는 즉시 바로 전달되기 떄문에 버퍼를 사용하는 BufferReader 보다
속도 면에서 불리하다는 큰 단점이 존재한다.

---

### ✅BufferedReader

버퍼리더는 입력 받은 값을 기본적으로 8192 char (16384 byte) 크기의 버퍼에 담아두었다가 한번에 프로그램에 전송을한다.

어쩌면 입력받은 즉시 전송하는 Scanner가 더 효율적이라고 생각될 수 있겠지만 버퍼링 없이 전송하는 것은  CPU와의 성능 차이 떄문에 버퍼를 사용하는 방식보다 속도에서 비효율적이라고 할 수 있다.

과일을 수확할떄 , 하나의 과일을 딸 떄마다 창고로 옮겨주는 것과
수확한 과일을 한 수레에 모아 한번에 창고로 옮겨주는 것의 효율 차이를 예를 들수 있다.


![image description](/assets/images/scanner.png)<br>


---

### ✅BufferedReader 사용법

Scanner는 띄어쓰기와 개행문자를 기준으로 입력 값을 인식하기 떄문에 따로 가공할 필요가 없지만
버퍼리더는 개행문자(엔터)만 경계로 인식하고 입력된 데이터의 형식이 String으로 고정되기 떄문에 데이트를 따로 가공해주어야 한다.

BufferedReader와 StringTokenizeer를 사용하기 위해 import를 해준다.

BufferedReader를 사용하기 위해선 예외처리가 필수적이기 떄문에 try,cathc문을 이용하던가
메인문 중괄호 시작전 thrwos IOException 으로 처리해야만 한다.

입력을 받기 위해선 ReadLine() 메소드를 사용하고 , 데이터가 문자 값으로 들어오기 떄문에 숫자 값을 받아올떈 꼭 형변환이 필요하다.

---

### ✅다량의 데이터 입력받기

단일 입력을 받을 떄는 상관 없지만 다량의 데이터를 입력 받을떄는 split 아니면 StringTokenizer를 사용해준다.

split은 입력 받는 동시에 별다른 처리 없이 배열로 데이터를 받아올 수 있다.

그에 반해 StringTokenizer의 경우 토큰화 된 문자열을 다시 처리해주어야 한다.

StringTokenzier의 생성자에서 추가적인 구분자를 명시하지 않을 경우 default 값은 띄어쓰기로 데이타기 구분되기 떄문에 필요 시 다른 구분자를 사용할 경우 StringTokenzier st = new StringTokenize(문자열,구분자); 를 사용한다.

배열을 생성하여 크기를 정해줄떈 countTokens() 메서드를 이용해 총 토큰의 수를 리턴받는다.

그 다음 hasMoreTokent() 메소드가 토큰이 더이상 없을떄는 false를 리턴 한다는 것을 이용해 while문을 돌리며 데이터를 저정한다. 

성능면에선 split은 정규식을 기반으로 문자열을 자르는 로직으로 동작하기 떄문에
단순히 공백 자리를 당겨서 채우는 StringTokenizer가 더빠르다.


```java
import java.io.*; //BufferedReader 사용
import java.util.*; //StringTokenizer 사용

public class BufferEx {
	public static void main(String[] args) throws IOException { // 예외처리 필수
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); // 선언
		
		String s = br.readLine(); 
		System.out.println("String : " + s);
		
		int i = Integer.parseInt(br.readLine()); // readLine()으로 받은 String 값을 int로 형변환
		System.out.println("Int : " + i);
		
       	 	//여러 개의 데이터 입력받기
        	String s2[] = br.readLine().split(" "); //split을 이용해 다량의 데이터 입력 받기
        
		StringTokenizer st = new StringTokenizer(br.readLine());
		int arr[] = new int[st.countTokens()];
		int count=0;
		while(st.hasMoreTokens()) {
			arr[count] = Integer.parseInt(st.nextToken());
			System.out.println(arr[count++]);
       		//countTokens() : 총 토큰의 개수를 리턴
		//hasMoreTokens() : 토큰이 남아있다면 true, 없으면 false 리턴
		}
	}
}

```


