# 💡 Array stack & queue 로 사용하기

## 📌 Stack With JS Array

`Stack` 은 `Last In First Out` 의 특징을 지닌 자료구조로 가장 마지막에 추가된 데이터가 가장 먼저 반출됩니다.

Stack에는 두 가지 주요 기능이 있는데, 데이터를 입력하는 기능인 `PUSH`와 데이터를 출력하는 기능인 `POP`입니다.

JS의 Array를 이용해 `PUSH`와 `POP`을 다루는 것은 Array의 메소드를 이용한 두 가지 조합이 가능합니다.

1. `push` 와 `pop`을 사용하는 조합 => 배열의 끝에서 데이터의 입출이 진행됩니다.
2. `unshift`와 `shift`를 사용하는 조합 => 배열의 앞에서 데이터의 입출이 진행됩니다.

</br>

### 👉 `push` & `pop`

```javascript
const stack = [];

console.log("PUSH ------------------------------");
for (let i = 1; i <= 5; i++) {
    console.log(i);
    stack.push(i);
}

console.log("POP ------------------------------");
for (let i = 1; i <= 5; i++) {
    let popped = stack.pop();
    console.log(popped);
}

/*
    OUTPUT
    PUSH ------------------------------
    1
    2
    3
    4
    5
    POP ------------------------------
    5
    4
    3
    2
    1
*/
```

</br>

### 👉 unshift`와`shift`

```javascript
const stack = [];

console.log("PUSH ------------------------------");
for (let i = 1; i <= 5; i++) {
    console.log(i);
    stack.unshift(i);
}

console.log("POP ------------------------------");
for (let i = 1; i <= 5; i++) {
    let popped = stack.shift();
    console.log(popped);
}
```

</br>

## 📌 Queue With JS Array

`Queue` 는 `First In First Out` 의 특징을 갖는 자료구조로 가장 처음에 들어온 데이터가 가장 처음으로 반출됩니다.

Queue에는 두 가지 주요 기능이 있는데, 데이터를 입력하는 기능인 `Enqueue`와 데이터를 출력하는 기능인 `Dequeue`입니다.

Queue로 JS의 Array를 사용하기 위해선, Stack에서와 마찬가지로 2가지의 조합이 가능합니다.

1. `push` 와 `shift`를 사용하는 조합 => 데이터의 입력은 배열의 끝에서, 데이터의 출력은 배열의 앞에서 진행됩니다.
2. `unshift` 와 `pop`을 사용하는 조합 => 데이터의 입력은 배열의 앞에서, 데이터의 출력은 배열의 뒤에서 진행됩니다.

</br>

### 👉 `push` & `shift`

```javascript
const queue = [];

console.log("Enqueue ------------------------------");
for (let i = 1; i <= 5; i++) {
    console.log(i);
    queue.push(i);
}

console.log("Dequeue ------------------------------");
for (let i = 1; i <= 5; i++) {
    let dequeued = queue.shift();
    console.log(dequeued);
}

/*
    OUTPUT
    Enqueue ------------------------------
    1
    2
    3
    4
    5
    Dequeue ------------------------------
    1
    2
    3
    4
    5
*/
```

</br>

### 👉 `unshift` & `pop`

```javascript
const queue = [];

console.log("Enqueue ------------------------------");
for (let i = 1; i <= 5; i++) {
    console.log(i);
    queue.unshift(i);
}

console.log("Dequeue ------------------------------");
for (let i = 1; i <= 5; i++) {
    let dequeued = queue.pop();
    console.log(dequeued);
}

/*
    OUTPUT
    Enqueue ------------------------------
    1
    2
    3
    4
    5
    Dequeue ------------------------------
    1
    2
    3
    4
    5
*/
```
