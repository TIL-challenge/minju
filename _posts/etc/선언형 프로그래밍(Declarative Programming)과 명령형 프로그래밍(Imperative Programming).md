---
title: 선언형 프로그래밍(Declarative Programming)과 명령형 프로그래밍(Imperative Programming)
date: 2024-11-06
author: minjumost
category: 
tags: []
---

`선언형 프로그래밍`은 `무엇을` 해야 하는지를 기술하는 방식의 프로그래밍 패러다임이다. 쉽게 말해, 코드에서 원하는 결과를 설명하지만, 그 결과를 얻는 방법(절차나 단계)은 명시하지 않는 것이다.

반대로 명령형 프로그래밍은 `어떻게` 해야하는지를 단계별로 기술하는 방식이다. 을 `명령형 프로그래밍`이라고 한다.

코드를 통해 비교해보자.

```javaScript
// 명령형 프로그래밍
const numbers = [1, 2, 3, 4, 5];
const doubled = [];

for (let i = 0; i < numbers.length; i++) {
  doubled.push(numbers[i] * 2);
}
```

명령형 프로그래밍은 for문을 통해 push한다는 것을 우리가 잘 알고있다.

```JavaScript
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(num => num * 2);
```

반면에 선언적 프로그래밍은 어떻게 반복할지 전혀 명시하지 않고 각 요소에 2를 곱한 새로운 배열을 얻기만 하고 있다.
