# 💡 Array 순회 하기

## 📌 순회

순회란 데이터를 하나 하나 살펴보는 것을 의미 합니다.

단순히 조회만 해볼 수도 있고, 하나 하나 살펴보며 데이터를 조작하기도 합니다.

## 📌 Array 순회 방법

코드 상에서 사용할 변수는 다음과 같습니다.

```javascript
let sampleArr = [1,2,3,4,5,6,7,8,9,10];
```

### 👉 `for` 문

```javascript
for (let index = 0; index < sampleArr.length; index++) {
    sampleArr[index].value += 2; // index: [INDEX], sampleArr[index]: [VALUE]
}
// sampleArr: [3,4,5,6,7,8,9,10,11,12];
```

### 👉 for...of 문을 사용한 순회

```javascript
for (const sample of sampleArr) {
    sample.value += 2;
}
// sampleArr: [3,4,5,6,7,8,9,10,11,12];
```

`for...of` 문은 배열의 원소를 하나 하나 반환합니다.

### 👉 for...in 문을 사용한 순회

```javascript
for (const property in sampleArr) {
    sampleArr[property].value += 2; // property: [INDEX], sampleArr[property]: sampleClass { value: [VALUE] }
}
// sampleArr: [3,4,5,6,7,8,9,10,11,12];
```

`for...in` 문은 배열 객체의 키를 반환합니다. 원소 자체를 반환하는 것이 아니기 때문에 유의해서 사용해야합니다.

### 👉 `while` 문

```javascript
let whileIndex = 0;
while (whileIndex < sampleArr.length) {
    sampleArr[whileIndex].value += 2; // whileIndex: [whileINDEX], sampleArr[whileIndex]: [VALUE]
    whileIndex++;
}
// sampleArr: [3,4,5,6,7,8,9,10,11,12];
```

### 👉 `do...while` 문

```javascript
let doWhileIndex = 0;
do {
    sampleArr[doWhileIndex].value += 2; // doWhileIndex: [Index], sampleArr[doWhileIndex]: [VALUE]
    doWhileIndex++;
} while (doWhileIndex < sampleArr.length);
// sampleArr: [3,4,5,6,7,8,9,10,11,12];
```

`do...while` 문을 이용한 순회는 무조건 한번은 수행합니다.
