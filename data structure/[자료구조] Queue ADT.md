## 큐 ADT의 데이터 구조

- 가장 먼저 들어간 데이터가 제일 먼저 나온다. `FIFO`
- 가장 나중에 들어간 데이터는 가장 나중에 나온다. `LILO`
- 가장 앞에 있는 데이터를 `front`라고 부르며, `front`부터 삭제(Dequeue)연산을 하게 된다.
- 가장 뒤에 있는 데이터를 `back`이라 부르며, `back`부터 삽입(Enqueue)연산을 하게 된다.

![](images/Pasted%20image%2020241008092204.png)

## 큐 ADT의 연산

### Enqueue(삽입)

Back에서 삽입이 이루어진다. 삽입을 한 요소가 새로운 Back이 된다.
![](images/Pasted%20image%2020241008111007.png)

### Dequeue(제거)

Front에서 제거가 이루어진다. 제거한 요소의 다음 요소가 새로운 Front가 된다.
![](images/Pasted%20image%2020241008110857.png)
