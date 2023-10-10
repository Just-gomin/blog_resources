# 💡 Array 정렬 & 필터링

## 📌 Array.prototype.sort

배열 내의 원소를 정렬 시키는 함수 입니다.

정렬된 __새로운 배열을 반환하는 것이 아닌, 원본 배열을 정렬__ 시키는 함수 입니다.

</br>

## 📌 Array.prototype.sort([compareFunction])

```typescript
// file: typescript/lib/lib.es5.d.ts
interface Array<T> {
    ...

    /**
     * Sorts an array in place.
     * This method mutates the array and returns a reference to the same array.
     * @param compareFn Function used to determine the order of the elements. It is expected to return
     * a negative value if the first argument is less than the second argument, zero if they're equal, and a positive
     * value otherwise. If omitted, the elements are sorted in ascending, ASCII character order.
     * ```ts
     * [11,2,22,1].sort((a, b) => a - b)
     * ```
     */
    sort(compareFn?: (a: T, b: T) => number): this;

    ...
}
```

`compareFunction`은 두 개의 인자를 받아 서로 비교해 순서를 정하는 함수로,</br>
일관성 있게 `0보다 작은 수`, `0`, `0보다 큰 수` 중 하나를 반환 해야합니다.

</br>

### 👉 compareFunction이 주어지지 않은 경우

원소를 `문자열 변환` 시켜, 문자열 유니코드를 오름차순으로 정렬시킵니다.

```javascript
    [10, 9, 8, 7, 6, 5, 4, 3, 2, 1].sort(); // [1, 10, 2, 3, 4, 5, 6, 7, 8, 9]
    ['하', '파', '타', '카', '차', '자', '아', '사', '바', '마', '라', '다', '나', '가'].sort();
    // ['가', '나', '다','라', '마', '바','사', '아', '자','차', '카', '타','파', '하']
```

</br>

### 👉 compareFunction이 주어진 경우

- compareFunction(a, b) > 0 : a가 b보다 먼저 위치합니다.
- compareFunction(a, b) = 0 : a와 b의 순서가 바뀌지 않습니다.
- compareFunction(a, b) < 0 : b가 a보다 먼저 위치합니다.

</br>

```javascript
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1].sort((a, b) => a - b); // [1, 2, 3, 4,  5, 6, 7, 8, 9, 10]

['하', '파', '타', '카', '차', '자', '아', '사', '바', '마', '라', '다', '나', '가'].sort((a, b) => a > b ? 1 : -1);
// ['가', '나', '다','라', '마', '바','사', '아', '자','차', '카', '타','파', '하']
```

</br>

```javascript
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1].sort((a, b) => b - a); // [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

['하', '파', '타', '카', '차', '자', '아', '사', '바', '마', '라', '다', '나', '가'].sort((a, b) => b > a ? 1 : -1);
// ['하', '파', '타', '카', '차', '자', '아', '사', '바', '마', '라', '다', '나', '가']
```

</br>

객체를 정렬하는 예제를 작성 해보겠습니다.

이름을 기준으로 오름차순 정렬을 진행하고, 이름이 같은 경우 가격을 기준으로 오름차순 정렬을 진행하는 예제 입니다.

```javascript
let items = [
    { 'name': 'd', price: 121 },
    { 'name': 'c', price: 150 },
    { 'name': 'a', price: 103 },
    { 'name': 'a', price: 107 },
    { 'name': 'd', price: 87 },
    { 'name': 'b', price: 99 },
];

items.sort((a, b) => {
    if (a.name == b.name) {
        return a.price - b.price;
    }

    return a.name > b.name ? 1 : -1;
}); 
/*
items: [
  { name: 'a', price: 103 },
  { name: 'a', price: 107 },
  { name: 'b', price: 99 },
  { name: 'c', price: 150 },
  { name: 'd', price: 87 },
  { name: 'd', price: 121 }
]
*/

```

## Array.prototype.filter()

```typescript
// file: typescript/lib/lib.es5.d.ts
interface Array<T> {
    ...

    /**
     * Returns the elements of an array that meet the condition specified in a callback function.
     * @param predicate A function that accepts up to three arguments. The filter method calls the predicate function one time for each element in the array.
     * @param thisArg An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
     */
    filter<S extends T>(predicate: (value: T, index: number, array: T[]) => value is S, thisArg?: any): S[];
    /**
     * Returns the elements of an array that meet the condition specified in a callback function.
     * @param predicate A function that accepts up to three arguments. The filter method calls the predicate function one time for each element in the array.
     * @param thisArg An object to which the this keyword can refer in the predicate function. If thisArg is omitted, undefined is used as the this value.
     */
    filter(predicate: (value: T, index: number, array: T[]) => unknown, thisArg?: any): T[];

    ...
}
```

`filter` 는 주어진 배열의 일부에 대한 얕은 복사본을 생성하고, 인수로 전달된 함수 `predicate` 에서 통과한 요소들만을 포함 시킵니다.

`predicate` 는 결과 배열에서 원소가 포함 되었으면 하는 경우 `true`를 반환하고, 포함 되지 않았으면 하는 경우 `false`를 반환 해야합니다.

```javascript
let numberArr = [10, 9, 8, 7, 6, 5, 4, 3, 2, 1];

let oddArr = numberArr.filter(function (v, i, arr) {
    return v % 2;
}); // [ 9, 7, 5, 3, 1 ]

let evenArr = numberArr.filter((v, i, arr) => {
    return v % 2 === 0;
}); // [ 10, 8, 6, 4, 2 ]
```
