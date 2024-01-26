---

published: true
title: "[Java] 컬렉션 프레임워크 Set (2/2)"
excerpt: "자바 컬렉션 프레임워크 Set 컬렉션  HashSet,TreeSet 알아보기."

categories:
  - Java
tags:
  - [collection, tag2]

permalink: /java/java10/

toc: true
toc_sticky: true


date: 2024-01-25
last_modified_at: 2024-01-25
---




## 🔥set -HashSet


### ✅HashSet과TreeSet 상속관계


![image description](/assets/images/hash.png)<br>


### ✅HashSet이란?
* HashSet은 Set인터페이스를 구현한 가장 대표적인 컬렉션이며,Set인터페이스의 특징대로<span style="background-color:#fff5b1"> **중복된 요소를 저장하지않고 순서를 중요시 하지않는다.**</span><br>
* Set은 저장순서를 유지 하지 않으므로 저장순서를 유지하고 한다면 LinkedHashSet을 사용해여한다.


```java
//HashSet 실습
public class Ex11_9 {
    public static void main(String[] args) {
        Object[] objArr = {"1", new Integer(1), "2", "2", "3", "3", "4", "4", "4"};
        Set set = new HashSet();

        for (int i = 0; i < objArr.length; i++) {
            set.add(objArr[i]); //HashSet에 objArr의 요소들을 저장한다
        }
        System.out.println(set); //{1,1,2,3,4} 중복 제거 하고 출력, 여기서 1은 문자열과,인터저 타입1이므로 서로 다르므로 같은 1이 두개 출력

        Iterator it = set.iterator();  //iterator객체 생성 

        while (it.hasNext()) {
            System.out.println(it.next());
        }
    }
}
/*출력
[1, 1, 2, 3, 4]
1
1
2
3
4
*/

```

---


### ✅HashSet의 add() 메서드
* **HashSet은 객체를 저장 하기 전에 기존에 같은 객체가 있는지 확인한다**. <br>
같은 객체가 없으면 저장하고, 있으면 저장하지 않는다.

* HashSet의 add()는 새로운 객체를 추가 하기 전에 기존에 저장된 객체와 같은 것인지 확인하기위해 저장할 객체의 **equals()와 hashCode()**를 호출한다.
그래서 equlas()와 hashCode()가 **오버라이딩 되있어야 한다**.
1. equals()는 인스턴스 변수(iv)를 비교 하도록 오버라이딩 한다.
2. hashCode()는 Object클래스의 hash()를 이용하여 오버라이딩 한다.

==> 자세한 예제로 equals 메서드를 오버라이딩 해야되는 경우로 포스팅 참고.

---

## 🔥set-TreeSet


### ✅TreeSet이란?
* TreeSet은 **이진 탐색 트리라는 자료 구조의 형태로 데이터를 저장하는 컬랙션 클래스이다**.
* 내부적으로 TreeMap을 이용해서 만들어졌으며 범위 검색과 정렬에 유리하다.
* 이진 트리는 모든 노드가 최대 두 개의 자식 노드를 갖는다.

### ✅이진 탐색 트리

* **모든 노드가 최대 두 개의 자식 노드를 갖는다.**
* **부모 보다 작은 값을 왼쪽, 큰 값을 오른쪽에 저장한다.**
* **중복된 값을 저장하지 못한다.**
* 범위 검색과 정렬에 유리하다.
* 데이터가 많아질 수록 데이터 **추가,삭제에 시간이 더걸린다**.(부모 보다 큰지 작은지를 비교하는 획수가 증가하기 떄문에)

 실제 이진 탐색 트리의 구조<br> 

![image description](/assets/images/treeset.png)<br>


* TreeSet은 compare()를 호출해서 비교하여 기존에 같은 객체가 있는지 확인한다.

```java
HashSet equals(), hasCode()로 비교
TreeSet은 compare()를 호출해서 비교
```

![image description](/assets/images/treeset1.png)<br>
TreeSet 트리 순회(전위,중위,후위)
* 이진 트리의 모든 노드를 한번씩 읽는 것을 트리 순회라고 한다.
* 전위,중위,후위 순회법이 있으며,중위 순회하면 오름차순으로 정렬된다.

---

## 🔥Map-HashMap

### ✅HashMap이란?
* HashMap' 은 키(Key)와 값(value)쌍을 저장하는 자료 구조이다.<br>
각 키는 고유하며, 키를 사용하여 해당하는 값을 빠르게 검색할 수 있다

* 해싱 (Hashing) :
'HashMap'의 핵심 원리이다.
'해싱 함수(Hashing Functoin)'는 키(key)를 받아서
정수값인 '해시코드(Hashcode)'를 반환하고,
반환된 해시코드는 Hash 배열의 각 요소인 '버킷(Bucket)'의 인덱스가 된다.

![image description](/assets/images/hashmap.png)<br>

이 예시에서도 보이듯이 배열의 각 요소를 **'버킷'**이라고 한다.

요약하면,
키(key)를 주면 해싱 함수에 의해 해시코드로 변환되고, 해당 해시코드는 배열의 각 요소인. 버킷의 인덱스 역할을 한다. 해당 버킷을 찾아가면 값을 삽입 및 조회할 수 있다.



### ✅HashMap 사용해서 예제코드 만들어보기1

```java
package collection;

import javax.sound.midi.SysexMessage;
import java.util.HashMap;
import java.util.Scanner;

public class Ex_16 {
    public static void main(String[] args) {
        HashMap map = new HashMap();
        map.put("admin", "1234");
        map.put("min", "123");
        map.put("admin", "12345");

        Scanner sc = new Scanner(System.in);

        while (true) {
            System.out.println("아이디와 비밀번호를 입력해주세요");
            System.out.print("id:");
            String id = sc.nextLine();

            System.out.print("password:");
            String password = sc.nextLine().trim();

            if (!(map.containsKey(id))) {
                System.out.println("등록되지 않은 아이디 입니다 다시입력해주세요.");
                continue;
            }
            if (!(map.get(id)).equals(password)) {
                System.out.println("비밀번호가 일치하지 않습니다 다시 입력해주세요");
            }else{
                System.out.println("id와 비밀번호가 일치합니다");
                break;
            }
        }
    }
}

```
* map을 생성해서 put()메서드를 사용해서 값을 넣는다.
* 여기서 admin 의 값은 12345 로 값을 초기화 시킨다.
* ContainsKey(Object Key) 메서드를 통해 map에 등록한 id값이랑 매개변수로 들어온 id 값을 비교 
* map.get(id) 매개변수로 입력받은 id값을 넘기면 지정된 키의 값을 반환 받는다 => ex) admin입력할경우 12345가 들어오면서 eqauls 문자비교

---

### ✅HashMap 사용해서 예제코드 만들어보기2

```java
package collection;

import java.util.*;

public class Ex11_17 {
    public static void main(String[] args) {
        HashMap map = new HashMap();
        map.put("김자바", new Integer(90));
        map.put("김자바", new Integer(100)); //key값이 일치하기떄문에 새로운값으로 바뀜 ==100
        map.put("이자바", new Integer(100));sasa
        map.put("강자바", new Integer(80));
        map.put("안자바", new Integer(90));

        Set set = map.entrySet(); // HashMap에 저장된 키와 값을 엔트리 형태로 set에 저장해서 반환 
        Iterator it = set.iterator();

        while (it.hasNext()) {
          // Iterator 조상타입 -> Map.Entry 자손 타입의 형변환 ( 다운 캐스팅 )
            Map.Entry e = (Map.Entry) it.next();
            System.out.println("이름:" + e.getKey() + ", 점수:"+ e.getValue());
        }

        set = map.keySet();
        System.out.println("참가자 명단:" + set);

        Collection values = map.values();
        it = values.iterator();

        int total = 0;

        while (it.hasNext()) {
            int i = (int) it.next();
            total += i;

        }

        
            System.out.println(" 총점:" + total);
            System.out.println(" 평균:" + (float)total/set.size());
            System.out.println(" 최고점수:" + Collections.max(values));
            System.out.println(" 최저점수:" + Collections.min(values));
    }
}

```

* entrySet()=> map에 저장된 키와 값을 엔트리의 형태로 set에 저장해서 반환
* entrySet은 Map.Entry로 받아야한다. 
* // Iterator 조상타입 -> Map.Entry 자손 타입의 형변환 ( 다운 캐스팅 )


--





<br>


참고

* Java의 정석(남궁성) ,
* https://velog.io/@cchoijjinyoung/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-5-HashMap%ED%95%B4%EC%8B%9C%EB%A7%B5%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90
* https://kevinntech.tistory.com/16<br>
* https://babgeuleus.tistory.com/entry/Map%EC%9D%98-EntrySet%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9E%90%EC%84%B8%ED%95%9C-%EC%84%A4%EB%AA%85%EB%A7%B5%EC%9D%84-%ED%83%90%EC%83%89%ED%95%98%EB%8A%94-4%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95
