---

published: true
title: "[Java] 컬렉션 프레임워크 Set (2/3)"
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

ref -Java의 정석(남궁성) 
{: .notice--info}


## 📌HashSet


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

## 📌TreeSet


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