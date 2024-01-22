---

published: true
title: "[Java] 컬렉션 프레임워크"
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

## 📌컬렉션 프레임워크란?
컬렉션 프레임워크란 데이터 군을 저장하는 클래스들을 표준화한 설계를 뜻한다. <br>
즉객체를 쉽고 편리하게 다룰수 있는 다양한 클래스를 제공한다.

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

### ✅ArrayList란?
* ArrayList는 기존의 Vector를 개선한 것으로 구현 원리와 기능적인 측면에서 동일하다.
* Vector는 자체적으로 동기화 처리가 되어 있으나 ArrayLsit는 그렇지 않다.
* List 인테페이스를 구현하므로, 저장 순서가 유지되고 중복을 허용한다.


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

#### ❗ArrayList 에 저장된 객체의 삭제 과정
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