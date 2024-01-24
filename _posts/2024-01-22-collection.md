---

published: true
title: "[Java] 컬렉션 프레임워크 list (1/3)"
excerpt: "수많은 데이터를 효율적으로 관리할수있는 자바 컬렉션 프레임워크에 대해서 알아보기."

categories:
  - Java
tags:
  - [collection, tag2]

permalink: /java/java9/

toc: true
toc_sticky: true


date: 2024-01-22
last_modified_at: 2024-01-22
---

ref -Java의 정석(남궁성) 
{: .notice--info}


### 📌컬렉션 프레임워크란?
* 컬렉션 프레임워크란 데이터 군을 저장하는 클래스들을 표준화한 설계를 뜻한다. <br>
=>즉,객체를 쉽고 편리하게 다룰수 있는 다양한 클래스를 제공한다.

---

### ✅컬렉션 프레임워크의 핵심 인터페이스

![image description](/assets/images/collection.png)<br>

* **List** : 순서가 있고, 데이터의 중복을 허용<br>
ex) 대기자 명단<br>
1.이순신<br>
2.홍길동<br>
3.김길동<br>
4.홍길동<br>

* **Set**: 순서없고 , 데이터 중복 허용하지 않음<br>
ex) 네발동물 -> 개,고양이,사자,호랑이

* **Map**: 키(key)와 값(value)의 쌍으로 이루어진 데이터 집합 <br>
ex) 02 서울 , 031 경기
ex) id pw
순서는 중요하지 않음 누가 먼저 회원가입했는지는 중요하지 않다
단. **키는 중복을 허용하지 않고 , 값은 중복을 허용한다.**

---

### 📌ArrayList


### ✅ArrayList란?
* ArrayList는 기본적으로 배열을 사용한다. 하지만 일반 배열과 차이점이 존재한다.<br>
 ==>일반 배열은 처음에 메모리를 할당할 때 크기를 지정해주어야 하지만,<span style="background-color:#fff5b1"> ArrayList는 크기를 지정하지 않고 동적으로 값을 삽입하고 삭제할 수 있다</span><br>
* ArrayList는 기존의 Vector를 개선한 것으로 구현 원리와 기능적인 측면에서 동일하다.
* Vector는 자체적으로 동기화 처리가 되어 있으나 ArrayLsit는 그렇지 않다.
* List 인테페이스를 구현하므로, 저장 순서가 유지되고 중복을 허용한다.

* <span style="background-color:#fff5b1">ArrayList는 각 데이터의 index를 가지고 있고 무작위 접근이 가능하기 때문에, 해당 index의 데이터를 한번에 가져올 수 있다. </span><br><



```java
package collection;
import java.util.ArrayList;
import java.util.Collection;
import java.util.Collections;

public class ArrayListEx1 {
    public static void main(String[] args) {
        ArrayList list = new ArrayList(10);
        list.add(new Integer(5));
        list.add(new Integer(4));
        list.add(new Integer(2));
        list.add(new Integer(0));
        list.add(new Integer(1));
        list.add(new Integer(3));


        ArrayList list2 = new ArrayList(list.subList(1,4));

        System.out.println(list);
        System.out.println(list2);

        //Collection은  인터페이스 , Collections는 유틸 클래스
        Collections.sort(list); //list를 정렬한다(오름차순으로 정렬함).
        Collections.sort(list2);
        System.out.println(list);
        System.out.println(list2);

        System.out.println("list.containsAll(list2):" + list.containsAll(list2));

        //추가
        list2.add("B");
        list2.add("C");
        list2.add(3,"A");  //추가할 인덱스지정 해주면 , 인덱스 3번에 A추가됨. 기존에있는건 뒤로 밀림(부담이 가는작업)
        System.out.println(list2);

        //변경
        list2.set(3,"AA");
        System.out.println(list2);


        list.add(0,"1");
        // indexOf()는 지정된 객체의 위치(인덱스)를 알려준다.
        System.out.println("index="+list.indexOf("1"));

        //삭제
       // list.remove(1);  //인덱스 1 번을 삭제
         list.remove(new Integer(1)); //인덱스가 아닌 interger 1을 삭제
    }
}

```

---

### ✅ArrayList 에 저장된 객체의 삭제 과정
- ArrayList에 <span style="background-color:#fff5b1"> 저장된 </span> 세 번쨰 데이터를(data[2])를 삭제하는 과정 (1/2).<br>
list.remove(2);를 호출

![image description](/assets/images/collection1.png)<br>

1. 삭제할 데이터 아래의 데이터를 한 칸씩 위로 복사해서 삭제할 데이터를 덮어쓴다.
2. 데이터가 모두 한 칸씩 이동 했으므로 마지막 데이터는 null로 변경한다.
3. 데이터가 삭제 되어 데이터의 개수가 줄었으므로 size값을 감소시킨다.(마지막 데이터를 삭제하는 경우에는 1 번의 배열의 복사 과정은 필요없다.)

---

* ArrayList에 저장된 객체의 삭제과정(2/2).
1. ArrayList에 저장된 <span style="background-color:#fff5b1"> 첫 번쨰 </span> 부터 삭제하는 경우 (배열 복사 발생)

```java
for(int i = 0; i<list.size(); i++){
  list.remove(i);
}
```

![image description](/assets/images/collection2.png)<br>

결과 ==><span style="background-color:#FFE6E6"> 전부삭제가 안된다.</span><br> 

---

2. ArrayList에 저장된 <span style="background-color:#fff5b1"> 마지막</span> 객체 부터 삭제하는 경우(배열 복사 발생 안함)

```java
for(int i= list.size()-1; i>0; i--){
  list.remove(i);
}
```

![image description](/assets/images/collection3.png)<br>
결과 ==><span style="background-color:#FFE6E6"> 전부삭제 완료. </span><br>

---


### 📌LinkedList

### ✅ 배열의 장점과 단점
* 장점<br>
  1. **배열은 구조가 간단하고 데이터를 읽는 데 걸리는 시간(접근시간, access time)이 짧다.**<br>
  <br>

* 단점<br>
1. **배열은 한번 생성하면 크기를 변경할 수 없다.**<br>
  -크기를 변경해야 하는 경우 새로운 배열을 생성 후 데이터를 복사힌 다음, 참조를 변경해야함.<br>
  -크기 변경을 피하기 위해 충분히 큰 배열을 생성하면, 메모리가 낭비됨.<br>
  <br>
 2. **비순차적인 데이터의 추가,삭제에 시간이 많이걸린다.(배열의 중간에 값을 추가 또는 삭제하는경우)**<br>
  -데이터를 추가하거나 삭제하기 위해,다른 데이터를 옮겨야 함.
  -그러나 순차적인 데이터 추가(끝에 추가)와 삭제(끝부터 삭제)는 빠르다.

---


### ✅LinkedList란?

* 배열의 단점을 보완하기 위해 나타난 자료구조가 LinkedList이다.
* 연결 리스트(LinkedList)는 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다.

---

### ✅LinkedList와 배열 비교
* 장점 <br>

1. **데이터의 삭제: 단 한번의 참조 변경만으로 가능**
![image description](/assets/images/collection4.png)<br>


2. **데이터 추가:한 번의 Node 객체 생성과 두 번의 참조 변경만으로 가능**
![image description](/assets/images/collection5.png)<br>


* 단점 <br>

1. LinkedList는 순차적 접근이기 때문에 검색의 속도가 느리다.<br>
(연결 리스트에 5개의 노드가 있다고 가정하면 세번쨰 노드에 접근하려면 첫 번쨰 노드 부터 차례대로 찾아가야 한다. 배열처럼 한 번에 갈 수 없다.)

---

### ✅LinkedList 종류

1. **단일 연결 리스트**<br>
- 단일 연결 리스트는 이동 방향이 단뱡향이기 떄문에 다음 요소에 대해 접근은 쉽지만 이전 요소에 대한 접근은 어렵다.
![image description](/assets/images/collection6.png)<br>

2. **이중 연결 리스트**<br>
- 단일 연결 리스트의 접근성을 향상 시킨 것이 이중 연결 리스트 이다.<br>
- 이중 연결 리스트는 참조 변수를 하나 더 추가하여 다음 요소에 대한 참조 뿐만 아니라 이전 요소에 대한 참조가 가능 하도록 하였다.
- Java의 LinkedList는 이중 연결 리스트로 구현 되어 있다.
![image description](/assets/images/collection7.png)<br>

3. **이중 원형 연결 리스트**<br>
- 이중 연결 리스트의 접근성을 향상 시킨 것이 이중 원형 연결 리스트 이다.<br>
- 이중 연결 리스트의 첫 번쨰 요소와 마지막 요소를 서로 연결 시킨 것이다.
![image description](/assets/images/collection8.png)<br>

---


### ✅ArrayList vs LinkedList 성능 비교
1. 순차적으로 데이터를 추가/삭제 - ArrayList가 빠름
2. 비순차적으로 데이터를 추가/삭제 - LinkedList가 빠름
3. 접근 시간(access time) - ArrayList가 빠름 (여기서 접근시간이란 데이터를 읽는 시간이다)

---
### 📌스택과 큐 Stack & Queue

#### ✅스택 Stack

![image description](/assets/images/stack.png)<br>
LIFO(Last In First Out)
-LIFO구조, 마지막에 저장된 것이 제일 먼저 꺼내게 된다.

#### ✅큐 Queue
![image description](/assets/images/queue.png)<br>
FIFO(First In First Out)
-FIFO구조, 제일 먼저 저장한 것을 제일 먼저 꺼내게 된다.

-Queue는 인터페이스다
그래서 Queue 인터페이스를 구현한 클래스를 사용하면 된다.

---

### 📌Iterator,Enumeration
 컬렉션에 저장된 데이터를 접근하는데 사용되는 **인터페이스**

####  ✅Enumeration이란?
* Enumeration은 Iterator의 구버전이다.<br>
* 이전 버전으로 작성된 소스와의 호완을 위해서 남겨두고 있을뿐 , 가능하면 Iterator를 사용하자.


####  ✅Iterator이란?
* 각 컬렉션마다(list,set,map) 구조가 다르기떄문에  값을 읽어오는 방식 또한 다르다. 그래서 이러한것을 표준하 하기위해 사용되는것이  iterator이다. 
* 컬렉션에 Iterator() 메서드를 호출해서 Iterator를 구현한 객체를 얻어서 사용.
* Iterator는 1회용이므로 다 사용 했다면 다시 얻어 와야 한다.



```java
//iterator 인터페이스의 메서드
boolean has Next() = > 읽어올 요소가 남아있는지 확인한다. 있으면 true, 없으면 false
Object next() => 다음  요소를 읽어온다. 
-next()를 호출하기 전에 hasNext()를 호출해서 읽어 올 요소가 있는지 확인하는 것이 안전하다.
```

```java
//iterator 인터페이스의 메서드 사용 예제
public class Ex11_5 {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");

        Iterator it = list.iterator();
        while (it.hasNext()) {
            System.out.println(it.next()); 
        }
    }

    

}

```
Collection 인터페이스에 Iterator 메서드가 정의 되있으므로, <br>
Collection 인터페이스들의 자손인  list와,set이 모두 가지고 있는 메서드 이기떄문에 list.iterator(); 메서드 호출만하면 iterator 객체를 얻을수있다.


* iterator을 사용을 안한다면?

```java
//iterator을 사용을 안한다면?
public class Ex11_5 {
    public static void main(String[] args) {
       // ArrayList list = new ArrayList(); 
          HashSet list = new HashSet();  
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");

       for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));   //hasSet 객체일경우 get메서드 컴파일오류
        }
    }
}
```

* ArrayList에는 get 메서드가 있지만 , HashSet에는 **get 메서드가 없어서 해당 예제에 for문은 작동하지 않는다**.<br>
이러한 불편함떄문에 iterator 객체를 생성하면 둘다 iterator를 사용해서 값을 가져올수 있기떄문에 iterator를 사용한다.

---

####  ✅Map과 iterator
* Map은 Collection의 자손이 아니므로 iterator()가 없다.

* 그래서 Map은 keySet(), entrySet(),value()를 호출한 다음, Iterator()를 호출해야한다.

```java
Map map = new HashMap();
Iterator it = map.entrySet().iterator();
=> Set eSet = map.entrySet();
=> Iterator it = eSet.iterator();
```

1. map.entrySet() 메서드를 호출해서 Set 객체를 얻고,<br>
2. 그 다음 eSet.iterator set에 iterator 허출해서 iterator 객체를 얻고,<br>
3. 참조변수 it에 저장해서 사용한다.


---

### 📌Arrays 클래스란?
* 배열을 다루기 편리한 static 메서드를 제공한다.

####  ✅일차원 배열의 비교와 출력 toString(),equals()

* 일차원 배열의 비교와 출력(toString(), equals() )
1. ToString()은 배열의 모든 요소를 문자열로 출력한다.(일차원 배열에서만 사용 가능)
2. equals()는 두 배열에 저장된 모든 요소를 비교해서 같으면 true, 다르면 false를 반환한다.(일차원 배열에서만)

* 다차원 배열의 비교와 출력(deepToString(),deepEquals())
1. deepToString은 배열의 모든 요소를 모두 출력한다(다차원 배열에 사용가능)
2. deepEquals()는 두 배열에 저장된 모든 요소를 비교하면서 같으면 true, 다르면 false를 반환한다(다차원 배열에서만 사용가능)

```java

public class ArraysEx {
    public static void main(String[] args) {
 int[] arr = {0, 1, 2, 3, 4,};
 int[][] arr2D = { {11, 12}, {21, 22} };

 System.out.println(Arrays.toString(arr));
 System.out.println(Arrays.deepToString(arr2D));

 String[][] str2D = new String[][]{ {"aaa", "bbb"}, {"AAA", "BBB"} };
 String[][] str2D2 = new String[][]{ {"aaa", "bbb"}, {"AAA", "BBB"} };

System.out.println(Arrays.equals(str2D,str2D2)); // false => 다차원 배열은 배열의 배열의 형태로 구성하기떄문에
//equals()로 비교 하면 문자열을 비교하는게 아닌 배열에 지정된 배열의 주소를 바교하기 떄문에 false가 나온다
System.out.println(Arrays.deepEquals(str2D,str2D2)); //true =>다차원 배열에서의 값을 배교할떄는 deepEquals()메서드를 사용.
    }
}

```

---


####  ✅배열의 복사 copyOf(),copyRange()
1. copyOf()는 배열 전체를 복사해서 새로운 배열을 만들어 반환한다.
2. copyOfRange()는 배열의 일부를 복사해서 새로운 배열을 만든다.

```java
public class ArrayEx_1 {
    public static void main(String[] args) {
    int[] arr = {0, 1, 2, 3, 4};
    int[] arr2 = Arrays.copyOf(arr, arr.length); //arr2= {0,1,2,3,4,}
    int[] arr3 = Arrays.copyOf(arr, 3); //arr3={0,1,2,3}
    int[] arr4 = Arrays.copyOf(arr, 7); //배열 길이 기준arr4={0,1,2,3,4,0,0}
    int[] arr5 = Arrays.copyOfRange(arr, 2, 4); // 인덱스 기준 arr5={2.3}
    int[] arr6 = Arrays.copyOfRange(arr, 0, 7); //arr8= {0,1,2,3,4,0,0}
    }
}

```

---

####  ✅배열 채우기 fill(),setAll()
1. fill()는 배열의 모든 요소를 지정된 값으로 채운다.
2.setAll()는 배열을 채우는데 사용할 함ㄴ수형 인터페이스를 매개변수로 받느다.
(이 메서드를 호출할 떄는 함수형 인터페이스를 구현한 객체를 매개변수로 지정하던가 아니면 람다식을 지정해야한다)

```java
int[] arr =new int[5];
Arrays.fill(arr,9); // arr={9.9.9.9.9}

//람다식은 1~5의 범위에 속한 임의의 정수를 반환한다.
Arrays.setAll(arr,(i) -> (int) (Math.random()*5)+1);
System.out.println("arr=" + Arrays.roStirng(arr));
```

####  ✅배열을 List로 변환 asList(Object)
1. asList()는 배열을 List에 담아서 반환한다.
2. asLsit()가 반환한 List의 크기는 변경할수없다. 즉 추가 또는 삭제가 불가능하다.

```java
List list = Arrays.asList(new Integer[]){1,2,3,4,5});  //list={1,2,3,4,5}
List list = Arrays.asList(1,2,3,4,5); 
list.add(6); //예외 발생 크기를 변경할수없음.
```

---

####  ✅배열의 정렬과 검색 sort(),binarySearch()
1. sort()는 배열을 정렬할 떄 사용하고 binarySearch()는 배열에 저장된 요소를 검색할떄 사용된다.
2. binarySearch()는 배열에 지정된 값이 저장된 위치(index)를 찾아서 반환하는데, **반드시 배열이 정렬된 상태이어야 올바른 결과를 얻는다**


```java
int [] arr = {3,2,0,1,4};
int idx = Array.binarySearch(arr,2); //idx = -5; 잘못된결과를 갖고옴

Arrays.sort(arr); //1)배열 arr을 정렬한다.
System.out.println(Arrays.toString(arr)); //{0,1,2,3,4}
int idx = Array.binarySearch(arr,2); //idx=2 올바른결과 

```

###  📌Comparator와 comparable
* 객체를 정렬 하는데 필요한 메서드를 정의한 인터페이스이다.(정렬 기준 제공)

Comparable : 기본 정렬 기준을 구현하는데 사용.
Comparator : 기본 정렬 기준 외에 다른 기준으로 정렬하고자 할 떄 사용

```java

public interface Comparator{
  int compare(Object o1, Object o2); //두 객체 o1,o2를 비교
  boolean eqauls(Object obj);
}

public interface Comparable{
  public int compareTo(Object o); //주어진 객체 (o)를 자신 this와 비교
}

```
compare()와 compareTo()는 두 객체의 비교 결과를 반환 하도록 구현 해야한다.
비교하는 두 객체가 같으면 0, 왼쪽이 크면 양수 왼쪽이 작으면 음수를 반환
(리턴값이 음수일 떄 자리 교환이 발생함)
