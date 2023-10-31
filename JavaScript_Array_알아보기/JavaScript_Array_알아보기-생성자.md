# JavaScript Array 알아보기 - 생성자

새로운 Array를 생성 합니다. Array를 생성할 때는 대괄호(`[ ]`)를 이용하거나, 생성자를 이용할 수 있습니다.

## `[]`

```javascript
let array = []; // [], length: 0
```

</br>

대괄호를 이용해 생성한 배열로, 길이 0의 배열이 생성됩니다.

## Array() constructor

### ArrayConstructor Interface

</br>

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

</br>

TypeScript에 정의된 Array 생성자 Interface를 참고하면 다음과 같이 정리할 수 있습니다.

- `Array()` 생성자를 사용할 때 인자로 숫자 1개를 넣는 경우 해당 수를 길이로 갖는 배열을 생성합니다.
- 1개의 숫자가 아닌 값을 넣는 경우, 해당 값을 포함한 길이 1의 배열을 생성합니다.
- 1개 이상의 값을 넣는 경우, 해당 값들을 원소로 하는 배열을 생성합니다.
- `new` 키워드는 생략 가능 합니다.

</br>

### Code of ArrayConstructor

위에서 살펴본 Interface와 특징들을 이용해 실제 코드 상에서 배열을 생성하면 어떤 원소들과 길이를 갖는지 확인해봤습니다.

</br>

```javascript
let array;

array = Array(); // [], length: 0

array = new Array(); // [], length: 0

array = Array(10); // [ <10 empty items> ], length: 10

array = new Array(10); // [ <10 empty items> ], length: 10

array = Array('a'); // [ 'a' ], length: 1

array = new Array('a'); // [ 'a' ], length: 1

array = Array(10, 20, 30); // [ 10, 20, 30 ], length: 3

array = new Array(10, 20, 30); // [ 10, 20, 30 ], length: 3

array = Array([10, 20, 30]); // [ [ 10, 20, 30 ] ], length: 1

array = new Array([10, 20, 30]); // [ [ 10, 20, 30 ] ], length: 1

array = Array(...[10, 20, 30]); // [ 10, 20, 30 ], length: 3

array = new Array(...[10, 20, 30]); // [ 10, 20, 30 ], length: 3
```

위에서 살펴 본대로, 아무것도 주어지지 않은 경우 빈 배열을 생성합니다. 숫자 1개만 주어진 경우 해당 숫자 만큼의 길이를 갖는 배열을 생성합니다. 1개 이상의 데이터가 주어지면 해당 데이터들을 원소로 갖는 배열을 생성합니다.

## Array.from() & Array.of()

### ArrayLike & ArrayConstructor Interface

```typescript
// file: node_modules/typescript/lib/lib.es5.d.ts
interface ArrayLike<T> {
    readonly length: number;
    readonly [n: number]: T;
}
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

</br>

TypeScript에 정의된 `Array.from` & `Array.of` 생성자 Interface를 참고하면 다음과 같이 정리할 수 있습니다.

</br>

- `from` 메소드를 이용하면, `ArrayLike`, 즉 길이 정보와, 인덱스에 대한 값을 갖는 객체를 이용해 배열을 생성할 수 있습니다. 또한, 원소의 각 값마다 생성시에 적용될 함수를 부여해 값 생성을 진행 시킬 수 있습니다.
- `of` 메소드를 사용한 생성자는 주어진 인수들을 모두 배열의 원소로 사용합니다.

</br>

### Array.from()

</br>

`from` 메소드를 통해 배열을 생성하는 코드들 입니다.

</br>

```javascript
let array;

// array = Array.from(); // TypeError: undefined is not iterable (cannot read property Symbol(Symbol.iterator))

array = Array.from(10); // [], length: 0

array = Array.from([10, 20, 30]); // [ 10, 20, 30 ] , length: 3

array = Array.from({ length: 5 }); // [ undefined, undefined, undefined, undefined, undefined ], length: 5

array = Array.from({ length: 5, 0: 0, 1: 1, 2: 2, 4: 4 }); // [ 0, 1, 2, undefined, 4 ], length: 5

array = Array.from({ length: 5 }, (v, k) => v); // [ undefined, undefined, undefined, undefined, undefined ], length: 5

array = Array.from({ length: 5 }, (v, k) => k); // [ 0, 1, 2, 3, 4 ], length: 5

array = Array.from({ length: 5, 0: 0, 1: 1, 2: 2, 3: 3, 4: 4 }, (v, k) => v + k); // [0, 2, 4, 6, 8], length: 5

array = Array.from([1, 2, 3, 4, 5], (v, k) => v + k); // [ 1, 3, 5, 7, 9 ] , length: 5
```

</br>

### Array.of()

</br>

`of` 메소드를 통해 배열을 생성하는 코드들 입니다.

</br>

```javascript
let array;

array = Array.of(); // [], length: 0

array = Array.of(1); // [ 1 ], length: 1

array = Array.of(10, 20, 30); // [ 10, 20, 30 ], length: 3

array = Array.of([10, 20, 30]); // [ [ 10, 20, 30 ] ], length: 1

array = Array.of(...[10, 20, 30]); // [ 10, 20, 30 ], length: 3
```
