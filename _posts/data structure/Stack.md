## 스택ADT의 데이터 구조

가장 마지막에 들어간 데이터가 제일 먼저 나온다. `LIFO`  
가장 먼저 들어간 데이터는 가장 나중에 나온다. `FILO`  

이때 가장 끝에 있는 데이터를 Top이라고 부르며, Top을 이용해서 연산을 수행하게 된다.

![](../_assets/images/data-structure/stack/img-stack.png)

## 스택 ADT의 연산

스택 ADT의 연산은 삽입, 제거 두 가지 뿐이다. 그 외의 기능들은 두 연산을 위한 보조 연산이다.

- 삽입(Push)
    십입은 스택 위에 새로운 노드를 쌓는것이다.
    삽입을 할때에는 Top을 기준으로 Top위에 쌓는 것이며 새롭게 쌓인 데이터가 Top이 된다.
    ![](../_assets/images/data-structure/stack/img-stack%202.png)

- 제거(Pop)
    제거는 스택의 최상위 노드를 걷어내는 것이다.
    Top이 가리키는 데이터를 걷어내고, 해당 데이터를 반환한다.
    해당 데이터 바로 이전에 들어온 데이터가 Top이 된다.
    ![](../_assets/images/data-structure/stack/img-stack%201.png)

## Stack 구현

```java
public class ArrayStack<T> {
    private T[] stack;
    private int top;
    private int capacity;

    public ArrayStack(int size){
        stack = (T[]) new Object[size];
        capacity = size;
        top = -1;
    }

    public void push(T item){
        if(top == capacity-1){
            throw new StackOverflowError();
        }
        stack[++top] = item;
    }

    public T pop(){
        if(top == -1){
            throw new EmptyStackException();
        }
        return stack[top--];
    }
}
```
