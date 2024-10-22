

> LinkedList란?

LinkedList는 노드를 연결해서 만든 리스트이다. 링크드 리스트의 노드는 데이터를 보관하는 필드와, 다음 노드와의 연결을 나타내는 포인터로 이루어진다.
![](../_assets/images/data-structure/linkedlist/img-[자료구조]-2linkedlist.png)

포인터로 노드들을 연결해보면 링크드 리스트가 되는 것이다.
![](../_assets/images/data-structure/linked-list/img-linked-list%201.png)

이렇게 각 노드에 대한 데이터와 포인터만 정의해두면 어렵지 않게 링크드 리스트를 만들 수 있다. 이제 실제로 코드로 구현해서 만들어보자. 

링크드 리스트의 ADT는 다음과 같은 연산을 가진다.

- 노드 생성/소멸
- 노드 추가
- 노드 탐색
- 노드 삭제
- 노드 삽입



하나씩 구현해보며 특징을 살펴 보자.

### 링크드 리스트의 노드 표현

``` java
class Node {
    int data; // 노드에 저장되는 데이터
    Node next; // 다음 노드를 가리키는 포인터

    Node(int data) {
        this.data = data;
        this.next = null; // 초기화 시 다음 노드는 null
    }
}
```

링크드 리스트의 노드는 다음과 같이 `data`와, 다음 노드를 가리키는 `next` 필드를 가진다.



### 노드 추가

```java
public void addLast(int data) {
        Node newNode = createNode(data); // 새로운 노드 생성
        if (head == null) {
            head = newNode; // 리스트가 비어있으면 헤드에 새 노드 설정
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next; // 마지막 노드까지 이동
            }
            current.next = newNode; // 마지막 노드의 next에 새 노드 연결
        }
    }
```



