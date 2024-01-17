---
title: "[Java] 자바 입출력 Scanner vs Bufferedreader 차이"
excerpt: " 자바 입출력 Scanner와 Bufferedreader 차이 구별하기"

categories:
  - Java
tags:
  - [tag1, tag2]

permalink: /java/java7/

toc: true
toc_sticky: true
published: true

date: 2024-01-17
last_modified_at: 2024-01-17
---

## 📌Scanner vs Bufferedreader 차이
자바에서 입력 방식은 scanner와 bufferedreader 가있다. 각자의 장점 단점을 알아보자.

### ✅Scanner 란?
Scanner 클래스는 입력받은 데이터를 다양한 타입으로 변환하여 반환하는 클래스이다.
간단하게 기본형과 String 타입을 정규표현식을 사용해 파싱할수있다.

### ✅Scanner 특징
* java.util 패키지에 속한다. (java.util.Scanner)
* 공백(띄어쓰기)및 개행(줄 바꿈)을 기준으로 읽는다.('', '\t', '\r', '\n' 등)
* 원하는 타입으로 읽을 수 있다.
* 버퍼의 사이즈가 1024byte(1KB) 이다.
* Unchecked(Runtime)Exception 으로 별도의 예외 처리를 명시할 필요가 없다.
* 데이터를 입력받을 경우 즉시 사용자에게 전송되며 입력받을 떄마다 전송되게 하기에 많은 시간이 소요된다.

### ✅BufferedReader 란?
데이터를 한번에 읽어와 버퍼에 보관한 후 버퍼에서 데이터를 읽어오는 방식으로 동작하는 클래스이다.
즉 사용자가 입력한 문자 스트림을 읽는 것이 라고한다.<br>

* 여기서 버퍼(buffer)란 ? <br>
데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 해당 데이터를 보관하는 임시 메모리 영역이다.
주로 입출력 속도 향상을 위해 버퍼를 사용한다.
