## 큐 ADT의 데이터 구조

- 가장 먼저 들어간 데이터가 제일 먼저 나온다. `FIFO`
- 가장 나중에 들어간 데이터는 가장 나중에 나온다. `LILO`
- 가장 앞에 있는 데이터를 `front`라고 부르며, `front`부터 삭제(Dequeue)연산을 하게 된다.
- 가장 뒤에 있는 데이터를 `back`이라 부르며, `back`부터 삽입(Enqueue)연산을 하게 된다.

![](../_assets/images/data-structure/queue/img-queue.png)

## 큐 ADT의 연산

### Enqueue(삽입)

Back에서 삽입이 이루어진다. 삽입을 한 요소가 새로운 Back이 된다.
![](../_assets/images/data-structure/queue/img-queue%201.png)

### Dequeue(제거)

Front에서 제거가 이루어진다. 제거한 요소의 다음 요소가 새로운 Front가 된다.
![](../_assets/images/data-structure/queue/img-queue%202.png)

## 구현

```java
public class ArrayQueue {
    private int front, rear, size;
    private int capacity;
    private int[] queue;

    // 큐를 초기화하는 생성자
    public ArrayQueue(int capacity) {
        this.capacity = capacity;
        this.front = this.size = 0;
        this.rear = capacity - 1; // rear는 마지막 요소를 가리킵니다.
        this.queue = new int[this.capacity];
    }

    // 큐가 가득 찼는지 확인하는 메서드
    public boolean isFull() {
        return (this.size == this.capacity);
    }

    // 큐가 비어 있는지 확인하는 메서드
    public boolean isEmpty() {
        return (this.size == 0);
    }

    // 큐에 데이터를 추가하는 메서드 (Enqueue)
    public void enqueue(int item) {
        if (isFull()) {
            System.out.println("Queue is full. Cannot enqueue.");
            return;
        }
        this.rear = (this.rear + 1) % this.capacity;
        this.queue[this.rear] = item;
        this.size++;
        System.out.println(item + " enqueued to queue");
    }

    // 큐에서 데이터를 제거하는 메서드 (Dequeue)
    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return Integer.MIN_VALUE;
        }
        int item = this.queue[this.front];
        this.front = (this.front + 1) % this.capacity;
        this.size--;
        return item;
    }

    // 큐의 첫 번째 요소를 확인하는 메서드 (peek)
    public int front() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return Integer.MIN_VALUE;
        }
        return this.queue[this.front];
    }

    // 큐의 마지막 요소를 확인하는 메서드 (peek)
    public int rear() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return Integer.MIN_VALUE;
        }
        return this.queue[this.rear];
    }

    public static void main(String[] args) {
        ArrayQueue queue = new ArrayQueue(5);

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);

        System.out.println("Front item is: " + queue.front());
        System.out.println("Dequeued item is: " + queue.dequeue());
        System.out.println("Front item is: " + queue.front());

        queue.enqueue(50);
        System.out.println("Rear item is: " + queue.rear());
    }
}

```
