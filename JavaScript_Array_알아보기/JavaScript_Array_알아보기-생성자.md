# JavaScript Array 알아보기 - 생성자

새로운 Array를 생성 합니다. Array를 생성할 때는 대괄호(`[ ]`)를 이용하거나, 생성자를 이용할 수 있습니다.

## []

```javascript
let array = []; // []
```

## Array() constructor

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

## Array.of()

```javascript
let array;

array = Array.of(); // [], length: 0

array = Array.of(1); // [ 1 ], length: 1

array = Array.of(10, 20, 30); // [ 10, 20, 30 ], length: 3
```

- `of` 메소드를 사용한 생성자는 주어진 인수들을 모두 배열의 원소로 사용합니다.

## Array.from()

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

## Interface of ArrayConstructor

Array 생성 방법에 대해 TypeScript에 정의된 interface들입니다. 위에서 설명한 내용들을 되새기며, 아래 정의된 interface를 살펴보시면 좋을 것 같습니다.

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
