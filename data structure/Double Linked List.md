# 이중 연결 리스트(Double Linked List)

이중 연결 리스트는 각 노드가 두 개의 포인터를 가지며, 앞 노드와 뒤 노드를 참조할 수 있는 자료구조이다. 단일 연결 리스트와 달리 양방향으로 탐색할 수 있다는 특징이 있다. 이 구조는 양쪽으로 탐색이 가능하다는 장점 때문에 다양한 상황에서 활용된다.

## 이중 연결 리스트의 특징

1. 노드 구조: 각 노드는 데이터를 저장하는 필드와 앞 노드(prev), 뒤 노드(next)를 가리키는 두 개의 포인터를 가진다.

2. 양방향 탐색:
   노드가 앞, 뒤로 이동할 수 있으므로 리스트를 순차적으로 탐색할 때 더 유연하다.

3. 효율적인 삽입 및 삭제:
   특정 위치에 새로운 노드를 삽입하거나 삭제할 때, 해당 노드의 앞뒤 포인터만 수정하면 된다. 이는 단일 연결 리스트에 비해 삽입과 삭제가 더 빠르다.

## 이중 연결 리스트의 주요 연산

#### 삽입(Insert)

리스트의 앞, 끝, 또는 중간에 새로운 노드를 추가할 수 있다.

#### 삭제(Delete)

특정 데이터를 가진 노드를 리스트에서 제거한다.

#### 탐색(Search)

리스트의 앞이나 뒤에서부터 원하는 데이터를 탐색한다.

## 이중 연결 리스트 구현

```java

// Node 클래스: 이중 연결 리스트의 노드
class Node {
    int data;
    Node prev;
    Node next;

    // 생성자
    public Node(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

// 이중 연결 리스트 클래스
class DoublyLinkedList {
    private Node head; // 리스트의 첫 번째 노드

    // 생성자: 리스트를 비워둠
    public DoublyLinkedList() {
        this.head = null;
    }

    // 리스트의 끝에 노드를 추가하는 메서드
    public void append(int data) {
        Node newNode = new Node(data);

        if (head == null) { // 리스트가 비어 있을 경우
            head = newNode;
            return;
        }

        Node current = head;
        while (current.next != null) { // 마지막 노드를 찾음
            current = current.next;
        }

        current.next = newNode;
        newNode.prev = current; // 양방향 연결 설정
    }

    // 리스트의 앞에 노드를 삽입하는 메서드
    public void prepend(int data) {
        Node newNode = new Node(data);

        if (head == null) { // 리스트가 비어 있을 경우
            head = newNode;
            return;
        }

        newNode.next = head;
        head.prev = newNode;
        head = newNode; // 새로운 노드를 head로 설정
    }

    // 리스트에서 특정 데이터를 가진 노드를 삭제하는 메서드
    public void delete(int data) {
        if (head == null) {
            System.out.println("리스트가 비어 있다.");
            return;
        }

        Node current = head;

        // 첫 번째 노드를 삭제할 경우
        if (current.data == data) {
            head = current.next;
            if (head != null) { // 리스트에 남은 노드가 있을 경우
                head.prev = null;
            }
            return;
        }

        // 중간 또는 끝에 있는 노드를 삭제할 경우
        while (current != null && current.data != data) {
            current = current.next;
        }

        if (current == null) { // 삭제할 노드를 찾지 못한 경우
            System.out.println("해당 데이터를 가진 노드가 없다.");
            return;
        }

        if (current.next != null) {
            current.next.prev = current.prev;
        }

        if (current.prev != null) {
            current.prev.next = current.next;
        }
    }

    // 리스트를 출력하는 메서드 (정방향)
    public void printList() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
}

public class Main {
    public static void main(String[] args) {
        DoublyLinkedList dll = new DoublyLinkedList();

        // 리스트에 노드 추가
        dll.append(10);
        dll.append(20);
        dll.append(30);

        System.out.println("리스트 출력:");
        dll.printList(); // 10 20 30

        // 리스트의 앞에 노드 삽입
        dll.prepend(5);
        System.out.println("앞에 5 추가 후:");
        dll.printList(); // 5 10 20 30

        // 특정 노드 삭제
        dll.delete(20);
        System.out.println("20 삭제 후:");
        dll.printList(); // 5 10 30
    }
}
```
