# JavaScript Array 내장 함수 살펴보기

[알고리즘 스터디](https://github.com/Just-gomin/Algorithm_Study/tree/master/GroupStudy/JavaScript_Algorithm)를 진행하며 JS의 Array 메서드를 자주 사용하는데, 그 종류 및 기능이 다양합니다. 쓸 때마다 반환 값이 있는지 없는지, 있다면 무엇인지 헷갈렸기에 정리하기로 마음 먹었습니다.

[MDN Array 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array) 의 순서와는 무관하게, 개인적으로 사용 빈도가 높은 순으로 정리했습니다.

정리 뿐 아니라, 해당 메서드를 어떤 상황에서 사용하는 지도 작성했습니다.

알고리즘 문제를 풀때 혹은 프로젝트를 진행할 때도 유용했으면 하는 마음으로 정리했습니다.

## Array() constructor

배열을 생성할 때, 사용하는 방법은 두 가지 입니다. 한 가지는 대괄호를 이용한 선언 입니다.

## Array.prototype.sort

배열 내의 원소를 정렬 시키는 함수 입니다.

정렬된 새로운 배열을 반환하는 것이 아닌, 원본 배열을 정렬시키는 함수 입니다.

### Array.prototype.sort([compareFunction])

compareFunction 은 두 개의 인자를 받아 서로 비교를 하는 함수로 일관성 있게 -1, 0, 1 중 하나를 반환 해야합니다.

1. compareFunction이 주어지지 않은 경우

    - 원소를 `문자열 변환` 시켜, 문자열 유니코드를 오름차순으로 정렬시킵니다.

2. compareFunction이 주어진 경우

    - compareFunction(a, b) > 0 : a가 b보다 먼저 위치합니다.
    - compareFunction(a, b) = 0 : a와 b의 순서가 바뀌지 않습니다.
    - compareFunction(a, b) < 0 : b가 a보다 먼저 위치합니다.
