---

published: true
title: "[Java] 컬렉션 프레임워크 Set (2/3)"
excerpt: "자바 컬렉션 프레임워크 Set 컬렉션 알아보기."

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


### 📒HashSet과TreeSet 상속관계



![image description](/assets/images/hash.png)<br>


### 📋HashSet이란?
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

### 📋HashSet의 add() 메서드
* **HashSet은 객체를 저장 하기 전에 기존에 같은 객체가 있는지 확인한다**. <br>
같은 객체가 없으면 저장하고, 있으면 저장하지 않는다.

* HashSet의 add()는 새로운 객체를 추가 하기 전에 기존에 저장된 객체와 같은 것인지 확인하기위해 저장할 객체의 **equals()와 hashCode()**를 호출한다.
그래서 equlas()와 hashCode()가 **오버라이딩 되있어야 한다**.
1. equals()는 인스턴스 변수(iv)를 비교 하도록 오버라이딩 한다.
2. hashCode()는 Object클래스의 hash()를 이용하여 오버라이딩 한다.


```java
public class EX11_11 {
    public static void main(String[] args) {
        HashSet set = new HashSet();

        set.add("abc");
        set.add("abc"); //중복이라 저장안됨
        set.add(new Person("David", 10));
        set.add(new Person("David", 10));

        System.out.println(set);
    }
}

//equals () 와 hashCode()를 오버라이딩해야 HasSet이 바르게 동작.
class Person{
    String name;
    int age;

    Person(String name , int age) {
        this.name = name;
        this.age = age;
    }

    public String toString() {
        return  name + ":" + age;
    }

    @Override
    public boolean equals(Object obj) {
       if(!(obj instanceof Person)) return false;

       Person p = (Person) obj;
        // 나자신(this)의 이름과 나이를  p와 비교
       return  this.name.equals(p.name) && this.age == p.age;
    }

    @Override
    public int hashCode() {
        // int hash(Object.. values); //....>은 가변인자
        return Objects.hash(name, age);
    }
}


```