# CollectionFramework & Stream

발표자 : 윤요섭

발표일 : 2023-02-26

# Collection Framework

컬렉션 프레임 워크 : '데이터 군을 다루고 표현하기 위한 단일화된 구조'

## Collection Framework 종류

 **✔️ public interface Iterable<T>**

![image](https://user-images.githubusercontent.com/81727895/221247582-ed182109-76a3-4812-a020-643faa9935ab.png)

**✔️ public interface Collection<E> extends Iterable**

![image](https://user-images.githubusercontent.com/81727895/221247069-7ab3329b-8279-416d-8ecd-9019d52558fb.png)

**✔️ public interface List<E> extends Collection<E>**

![image](https://user-images.githubusercontent.com/81727895/221247265-48e4d49d-61f4-4913-a5e3-5bd407513820.png)

**✔️ public interface Set<E> extends Collection<E>**

![image](https://user-images.githubusercontent.com/81727895/221247450-36740afd-9619-47e8-8946-2164f9846baf.png)

**🤔 Map은 어디 있을까?**

**✔️ public interface Map<K, V>**

![image](https://user-images.githubusercontent.com/81727895/221248261-d2ea6455-a8ba-4be9-806b-2a67419213d4.png)

## Collection

Collection 인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고 삭제하는 등 컬렉션을 다루는데 가장 기본적인 메서드 들을 정의하고 있다.

```java
package collectionFramework;

import java.util.*;

public class CollectionTest {
    public void basicCollection(){
        Collection listCol=new ArrayList();

        // add(Object o), addAll(Collection c) : 지정된 객체(Object) 
        // 또는 Collection(c)의 객체들을 Collection에 추가한다.
        listCol.add("1");
        listCol.add("2");
        listCol.add("3");

        Collection setCol = new HashSet();

        setCol.add("4");
        setCol.add("5");
        setCol.add("6");

        Collection collection = new ArrayList();

        collection.addAll(listCol);
        collection.addAll(setCol);

        collection.forEach(x -> System.out.print(x+", ")); // 1, 2, 3, 4, 5, 6,

        collection.clear();


        System.out.println("collection.isEmpty() : "+collection.isEmpty()); 
        // collection.isEmpty() : true
    }

    public void changeType(){
        Collection setCol = new HashSet();

        setCol.add("4");
        setCol.add("5");
        setCol.add("6");

        List<Object> objList = new ArrayList(setCol);

        for(Object obj : objList){
            System.out.print(obj.toString()+", "); // 4, 5, 6,
        }
    }

    public static void main(String args[]){
        CollectionTest collectionTest = new CollectionTest();
        collectionTest.basicCollection();
        collectionTest.changeType();
    }
}
```

## List

List는 기존의 Vector를 개선 한 것으로, 데이터의 저장순서가 유지되고 중복을 허용한다는 특징을 갖는다.

## ArrayList

ArrayList의 경우, Object 배열을 이용해서 데이터를 순차적으로 저장한다.

배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장한다.

```java
package collectionFramework;

import java.util.ArrayList;
import java.util.Collection;
import java.util.List;

public class ListTest {
    public void basicList(){
        List list = new ArrayList();

        // 0부터 100까지 숫자를 list에 담는다.
        for(int idx=0; idx<101; idx++){
            list.add(idx);
        }
        list.add("A");

        System.out.println("1. firstValue : "+Integer.valueOf(list.get(0).toString())); // 0
        System.out.println(list.indexOf(0)); // 0
        System.out.println(list.lastIndexOf("A")); // 101

        // 0번째 index를 제거
        list.remove(0);
        // "A"라는 Object를 제거
        list.remove("A");

        System.out.println("2. firstValue : "+Integer.valueOf(list.get(0).toString())); // 1
        System.out.println(list.indexOf(0)); // -1
        System.out.println(list.lastIndexOf("A")); // -1

        // 1부터 100까지 20개씩 끊어서 5개의 리스트로
        List subList1 = list.subList(0, 20);
        List subList2 = list.subList(20, 40);
        List subList3 = list.subList(40, 60);
        List subList4 = list.subList(60, 80);
        List subList5 = list.subList(80, 100);

        Collection collection= new ArrayList();
        collection.addAll(subList1);
        collection.addAll(subList2);
        collection.addAll(subList3);
        collection.addAll(subList4);
        collection.addAll(subList5);

        System.out.println("collection size : "+collection.size()); // collection size : 100

        Collection collection2 = new ArrayList();
        Collection collection3 = new ArrayList();
        for(int idx2=1; idx2<201; idx2++){
            collection2.add(idx2);
            collection3.add(idx2);
        }

        // 1 ~ 200까지 중에 1~100까지 삭제
        collection2.removeAll(collection);
        System.out.println("collection2's first value : "+collection2.toArray()[0].toString()); // 101

        // 1 ~ 200까지 중에 1~100을 남겨두고 나머지 삭제
        collection3.retainAll(collection);
        System.out.println("collection3's first value : "+collection3.toArray()[0].toString()); // 1
    }
    public static void main(String args[]){
        ListTest listTest = new ListTest();
        listTest.basicList();
    }
}
```

## LinkedList

배열은 가장 기본적인 형태의 자료구조로 구조가 간단하며, 사용하기 쉽다.

그러나, 크기를 변경할 수 없고, 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다.

이러한 배열의 단점을 보완하기 위해 LinkedList라는 자료구조가 고안되었다.

```
 ✔️ LinkedList : 배열과 달리 모든 데이터가 연속적으로 존재하는 것이 아니라, 불연속적으로 존재하는 
 
 데이터를 서로 연결(link)한 형태로 구성되어 있다.
```

<img src="https://www.nextree.co.kr/content/images/2021/01/jdchoi_20140225_arrayvslinkedlist11.png">

- 이미지 출처 : [자료구조: Linked List 대  ArrayList](https://www.nextree.co.kr/p6506/)

링크드 리스트에서 데이터 삭제는 이전 요소가 삭제하고자 하는 다음 요소를 참조하도록 변경한다.

**🤔 ArrayList와 LinkedList 누가 더 빠를까?**

```
순차적으로 추가/삭제하는 경우 : ArrayList > LinkedList

중간 데이터를 추가/삭제하는 경우 : LinkedList > ArrayList
```

## Queue


## Stack


# Stream




