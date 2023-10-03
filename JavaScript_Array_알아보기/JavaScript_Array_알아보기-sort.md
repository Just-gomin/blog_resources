# Array 정렬 시키기

## Array.prototype.sort

배열 내의 원소를 정렬 시키는 함수 입니다.

정렬된 __새로운 배열을 반환하는 것이 아닌, 원본 배열을 정렬__ 시키는 함수 입니다.

## Array.prototype.sort([compareFunction])

compareFunction 은 두 개의 인자를 받아 서로 비교를 하는 함수로 일관성 있게 -1, 0, 1 중 하나를 반환 해야합니다.

1. compareFunction이 주어지지 않은 경우

    - 원소를 `문자열 변환` 시켜, 문자열 유니코드를 오름차순으로 정렬시킵니다.

2. compareFunction이 주어진 경우

    - compareFunction(a, b) > 0 : a가 b보다 먼저 위치합니다.
    - compareFunction(a, b) = 0 : a와 b의 순서가 바뀌지 않습니다.
    - compareFunction(a, b) < 0 : b가 a보다 먼저 위치합니다.
