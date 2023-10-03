# JavaScript Array 내장 함수 살펴보기

JavaScript의 Array는 기본적인 자료 구조로, 다수의 데이터를 다루기에 적절합니다. 또한 Array를 선언할 때 길이를 정해줄 수도, 정해주지 않을 수도 있고 `push`, `pop`, `shift`, `unshift`와 같은 메서드들 덕분에 스택 혹은 큐처럼 활용도 가능합니다.

이러한 특징들 덕에 [알고리즘 스터디](https://github.com/Just-gomin/Algorithm_Study/tree/master/GroupStudy/JavaScript_Algorithm)를 진행하며 Array와 그 메서드들을 자주 사용하게 되는데, 종류가 다양하여 이를 정리 해봤습니다.

[MDN Array 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array) 의 순서와는 무관하게, 개인적으로 사용 빈도가 높은 순으로 그리고 언제 사용하는지를 정리해봤습니다.

## 1. Array 생성하기

새로운 Array를 생성 합니다. Array를 생성할 때는 대괄호(`[ ]`)를 이용하거나, 생성자를 이용할 수 있습니다.

### 1-1. []

```javascript
let array = []; // []
```

### 1-2. Array() constructor

```javascript
let array;

array = Array(); // [], length: 0

array = new Array(); // [], length: 0

array = Array(10); // [ <10 empty items> ], length: 10

array = new Array(10); // [ <10 empty items> ], length: 10

array = Array(10, 20, 30); // [ 10, 20, 30 ], length: 3

array = new Array(10, 20, 30); // [ 10, 20, 30 ], length: 3

array = Array([10, 20, 30]); // [ [ 10, 20, 30 ] ], length: 1

array = new Array([10, 20, 30]); // [ [ 10, 20, 30 ] ], length: 1
```

- `Array()` 생성자를 사용할 때 인자로 숫자 1개를 넣는 경우 해당 수를 길이로 갖는 배열을 생성합니다.
- 1개의 숫자가 아닌 값을 넣는 경우, 해당 값을 포함한 길이 1의 배열을 생성합니다.
- 1개 이상의 값을 넣는 경우, 해당 값들을 원소로 하는 배열을 생성합니다.
- `new` 키워드는 생략 가능 합니다.

### 1-3. Array.of()

```javascript
let array;

array = Array.of(); // [], length: 0

array = Array.of(1); // [ 1 ], length: 1

array = Array.of(10, 20, 30); // [ 10, 20, 30 ], length: 3
```

- `of` 메소드를 사용한 생성자는 주어진 인수들을 모두 배열의 원소로 사용합니다.

### 1-4. Array.from()

```javascript
let array;

// array = Array.from(); // TypeError: undefined is not iterable (cannot read property Symbol(Symbol.iterator))

array = Array.from(10); // [], length: 0

array = Array.from([10, 20, 30]); // [ 10, 20, 30 ] , length: 3

array = Array.from({ length: 5 }); // [ undefined, undefined, undefined, undefined, undefined ], length: 5

array = Array.from({ length: 5 }, (v, k) => v); // [ undefined, undefined, undefined, undefined, undefined ] , length: 5

array = Array.from({ length: 5 }, (v, k) => k); // [ 0, 1, 2, 3, 4 ] , length: 5
```

- `from` 메소드를 이용하면, 길이와 내부 원소들의 값을 생성하는 함수를 매개변수로서 줄 수 있습니다.
- 또는 iterable을 매개변수로 주면, 해당 iterable을 이용해 배열의 원소로 사용합니다.

### Interface of ArrayConstructor

```typescript
// file: node_modules/typescript/lib/lib.es5.d.ts
interface ArrayConstructor {
    new (arrayLength?: number): any[];
    new <T>(arrayLength: number): T[];
    new <T>(...items: T[]): T[];
    (arrayLength?: number): any[];
    <T>(arrayLength: number): T[];
    <T>(...items: T[]): T[];
    isArray(arg: any): arg is any[];
    readonly prototype: any[];
}

declare var Array: ArrayConstructor;
```

```typescript
// file: node_modules/typescript/lib/lib.es2015.iterable.d.ts
interface ArrayConstructor {
    /**
     * Creates an array from an array-like object.
     * @param arrayLike An array-like object to convert to an array.
     */
    from<T>(arrayLike: ArrayLike<T>): T[];

    /**
     * Creates an array from an iterable object.
     * @param arrayLike An array-like object to convert to an array.
     * @param mapfn A mapping function to call on every element of the array.
     * @param thisArg Value of 'this' used to invoke the mapfn.
     */
    from<T, U>(arrayLike: ArrayLike<T>, mapfn: (v: T, k: number) => U, thisArg?: any): U[];

    /**
     * Returns a new array from a set of elements.
     * @param items A set of elements to include in the new array object.
     */
    of<T>(...items: T[]): T[];
}
```

```typescript
// file: node_modules/typescript/lib/lib.es5.d.ts
interface ArrayLike<T> {
    readonly length: number;
    readonly [n: number]: T;
}
```

## Array 정렬 시키기

### Array.prototype.sort

배열 내의 원소를 정렬 시키는 함수 입니다.

정렬된 __새로운 배열을 반환하는 것이 아닌, 원본 배열을 정렬__ 시키는 함수 입니다.

### Array.prototype.sort([compareFunction])

compareFunction 은 두 개의 인자를 받아 서로 비교를 하는 함수로 일관성 있게 -1, 0, 1 중 하나를 반환 해야합니다.

1. compareFunction이 주어지지 않은 경우

    - 원소를 `문자열 변환` 시켜, 문자열 유니코드를 오름차순으로 정렬시킵니다.

2. compareFunction이 주어진 경우

    - compareFunction(a, b) > 0 : a가 b보다 먼저 위치합니다.
    - compareFunction(a, b) = 0 : a와 b의 순서가 바뀌지 않습니다.
    - compareFunction(a, b) < 0 : b가 a보다 먼저 위치합니다.

## Array 필터링 하기

## 서로 다른 Array 합치기

## Array 문자열로 엮기

## 참고 자료

- MDN JavaScript Array : <https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array>
