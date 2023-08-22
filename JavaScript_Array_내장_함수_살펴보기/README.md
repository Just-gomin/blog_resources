# JavaScript Array 내장 함수 살펴보기

```shell
< JS Array Functions And Result >

< Return, Check Origin >
r1 = numArr                                                              >>   numArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r1: [5,6,7,8,9,10,1,2,3,4]
r2 = strArr                                                              >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [5,6,7,8,9,10,1,2,3,4]

< Map, Return >
r1 = numArr.map((i) => i - 1)                                            >>   numArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r1: [4,5,6,7,8,9,0,1,2,3]
r2 = strArr.map((c) => +c)                                               >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [5,6,7,8,9,10,1,2,3,4]
r2 = strArr.map((c) => Number.parseInt(c))                               >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [5,6,7,8,9,10,1,2,3,4]

< Map, Sort, Return >
- [sort(): 비교 함수가 생략되면 ASCII 문자열 순서대로 오름차순 정렬]
r1 = numArr.map((i) => i - 1).sort()                                     >>   numArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r1: [0,1,2,3,4,5,6,7,8,9]
r2 = strArr.map((c) => +c).sort()                                        >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [1,10,2,3,4,5,6,7,8,9]
r2 = strArr.map((c) => Number(c)).sort()                                 >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [1,10,2,3,4,5,6,7,8,9]

< Map, Sort(compareFn), Return >
r1 = numArr.map((i) => i - 1).sort((a, b) => a - b)                      >>   numArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r1: [0,1,2,3,4,5,6,7,8,9]
r2 = strArr.map((c) => +c).sort((a, b) => a - b)                         >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [1,2,3,4,5,6,7,8,9,10]
r2 = strArr.map((c) => Number(c)).sort((a, b) => a - b)                  >>   strArr: [5,6,7,8,9,10,1,2,3,4]                                           ||   r2: [1,2,3,4,5,6,7,8,9,10]

< Check Origin >
numArr.concat()                                                          >>   origin: [5,6,7,8,9,10,1,2,3,4], [15,16,17,18,19,20,11,12,13,14]          ||   returned: [5,6,7,8,9,10,1,2,3,4,15,16,17,18,19,20,11,12,13,14]
numArr.copyWithin()                                                      >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,6,7,8,9,10,1,2,3,4]
numArr.entries()                                                         >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [[object Array Iterator]]
[...numArr.entries()]                                                    >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [0,5,1,6,2,7,3,8,4,9,5,10,6,1,7,2,8,3,9,4]
numArr.every((v, i, arr) => { /*log(v, i, arr);*/ return v; })           >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [true]
numArr.fill(-1, 1, 3)                                                    >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,-1,-1,8,9,10,1,2,3,4]
numArr.filter((v, i, arr) => v % 2)                                      >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,7,9,1,3]
numArr.find((v, i, arr) => v === 5)                                      >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5]
numArr.findIndex((v, i, arr) => i === 5)                                 >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5]
[numArr, numArr2].flat()                                                 >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,6,7,8,9,10,1,2,3,4,15,16,17,18,19,20,11,12,13,14]
[numArr, numArr2].flatMap((i) => i.join('-')                             >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5-6-7-8-9-10-1-2-3-4,15-16-17-18-19-20-11-12-13-14]
numArr.forEach((v, i, arr) => v + 1)                                     >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [undefined]
numArr.includes(1)                                                       >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [true]
numArr.includes(-1)                                                      >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [false]
numArr.indexOf(1)                                                        >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [6]
numArr.indexOf(-1)                                                       >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [-1]
numArr.join('-')                                                         >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5-6-7-8-9-10-1-2-3-4]
numArr.keys()                                                            >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [[object Array Iterator]]
numArr.lastIndexOf(10)                                                   >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5]
numArr.length                                                            >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [10]
numArr.map(((v, i, arr) => v * 2))                                       >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [10,12,14,16,18,20,2,4,6,8]
numArr.pop()                                                             >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [4]
numArr.push(100)                                                         >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [11]
numArr.reduce((pv, cv, ci, arr) => pv + cv, 0)                           >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [55]
numArr.reduceRight((pv, cv, ci, arr) => pv + cv, 0)                      >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [55]
numArr.reverse()                                                         >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [4,3,2,1,10,9,8,7,6,5]
numArr.shift()                                                           >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5]
numArr.slice(3, 7)                                                       >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [8,9,10,1]
numArr.some((v, i, arr) => v % 3 === 0)                                  >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [true]
numArr.some((v, i, arr) => v % 11 === 0)                                 >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [false]
numArr.sort()                                                            >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [1,10,2,3,4,5,6,7,8,9]
strArr.sort()                                                            >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [1,10,2,3,4,5,6,7,8,9]
numArr.sort((a, b) => a - b))                                            >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [1,2,3,4,5,6,7,8,9,10]
strArr.sort((a, b) => a - b))                                            >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [1,2,3,4,5,6,7,8,9,10]
numArr.splice(3)                                                         >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [8,9,10,1,2,3,4]
numArr.toLocaleString()                                                  >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,6,7,8,9,10,1,2,3,4]
numArr.toString()                                                        >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,6,7,8,9,10,1,2,3,4]
numArr.unshift(-1)                                                       >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [11]
numArr.values()                                                          >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [[object Array Iterator]]
[...numArr.values()]                                                     >>   origin: [5,6,7,8,9,10,1,2,3,4]                                           ||   returned: [5,6,7,8,9,10,1,2,3,4]
```
