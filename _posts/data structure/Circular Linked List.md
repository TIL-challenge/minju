## 순환 연결 리스트(Circular Linked List)

순환 연결 리스트는 마지막 노드가 첫 번째 노드와 연결되어 원형 구조를 이루는 리스트다. 이 리스트는 끝이 없기 때문에, 노드를 탐색할 때 리스트의 마지막에 도달하면 다시 처음으로 돌아갈 수 있다.

## 순환 연결 리스트의 특징

1. **순환 구조**:
    
    - 마지막 노드의 `next` 포인터가 첫 번째 노드를 가리키고, 첫 번째 노드의 `prev` 포인터가 마지막 노드를 가리킨다.
    - 리스트를 양방향으로 탐색할 수 있으며, 끝이 없이 순환한다.
2. **노드 구조**
    
    - 각 노드는 데이터를 저장하는 필드와 함께 앞 노드(`prev`)와 뒤 노드(`next`)를 가리키는 포인터를 가진다.
3. **효율적인 삽입과 삭제**:
    
    - 특정 위치에 노드를 삽입하거나 삭제할 때, 인접한 두 노드의 포인터만 변경하면 되므로 효율적이다.
    - 첫 번째나 마지막 노드에서 작업할 때도 동일한 방식으로 처리할 수 있다.
4. **연결 방식**:
    
    - 리스트는 마지막 노드와 첫 번째 노드가 서로 연결된 구조로, 모든 노드가 원형으로 연결되어 있다.

## 순환 연결 리스트의 주요 연산

1. **삽입(Insert)**:
    
    - 리스트의 앞, 끝, 또는 중간에 새로운 노드를 삽입할 수 있다.
2. **삭제(Delete)**:
    
    - 특정 데이터를 가진 노드를 리스트에서 제거할 수 있다.
3. **탐색(Search)**:
    
    - 리스트를 순환하며 데이터를 탐색할 수 있다. 원하는 데이터를 찾을 때까지 순환하면서 탐색이 가능하다.

## 순환 이중 연결 리스트 구현

```java
// Node 클래스: 순환 이중 연결 리스트의 노드
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

// 순환 이중 연결 리스트 클래스
class CircularDoublyLinkedList {
    private Node head; // 리스트의 첫 번째 노드

    // 생성자: 리스트를 비워둠
    public CircularDoublyLinkedList() {
        this.head = null;
    }

    // 리스트의 끝에 노드를 추가하는 메서드
    public void append(int data) {
        Node newNode = new Node(data);

        if (head == null) { // 리스트가 비어 있을 경우
            head = newNode;
            head.next = head; // 자기 자신을 가리키는 순환 구조
            head.prev = head;
            return;
        }

        Node last = head.prev; // 마지막 노드 찾기

        last.next = newNode;
        newNode.prev = last;
        newNode.next = head; // 마지막 노드가 첫 노드를 가리킴
        head.prev = newNode; // 첫 노드의 prev가 새 노드를 가리킴
    }

    // 리스트의 앞에 노드를 삽입하는 메서드
    public void prepend(int data) {
        Node newNode = new Node(data);

        if (head == null) { // 리스트가 비어 있을 경우
            head = newNode;
            head.next = head;
            head.prev = head;
            return;
        }

        Node last = head.prev; // 마지막 노드 찾기

        newNode.next = head;
        newNode.prev = last;
        head.prev = newNode;
        last.next = newNode;
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
            if (head.next == head) { // 리스트에 노드가 하나일 경우
                head = null;
            } else {
                Node last = head.prev;
                head = head.next;
                head.prev = last;
                last.next = head;
            }
            return;
        }

        // 중간 또는 끝에 있는 노드를 삭제할 경우
        do {
            if (current.data == data) {
                current.prev.next = current.next;
                current.next.prev = current.prev;
                return;
            }
            current = current.next;
        } while (current != head);

        System.out.println("해당 데이터를 가진 노드가 없다.");
    }

    // 리스트를 출력하는 메서드 (정방향)
    public void printList() {
        if (head == null) {
            System.out.println("리스트가 비어 있다.");
            return;
        }

        Node current = head;
        do {
            System.out.print(current.data + " ");
            current = current.next;
        } while (current != head);
        System.out.println();
    }
}

public class Main {
    public static void main(String[] args) {
        CircularDoublyLinkedList cdll = new CircularDoublyLinkedList();

        // 리스트에 노드 추가
        cdll.append(10);
        cdll.append(20);
        cdll.append(30);

        System.out.println("리스트 출력:");
        cdll.printList(); // 10 20 30

        // 리스트의 앞에 노드 삽입
        cdll.prepend(5);
        System.out.println("앞에 5 추가 후:");
        cdll.printList(); // 5 10 20 30

        // 특정 노드 삭제
        cdll.delete(20);
        System.out.println("20 삭제 후:");
        cdll.printList(); // 5 10 30
    }
}

```