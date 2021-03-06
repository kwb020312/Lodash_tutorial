Lodash는 2021 세계에서 가장 인기많은 JavaScript Library의 항목에서 당당히 순위권을 차지하여, 다루지 않을 수 없었다.

본 저장소는 <a href="https://lodash.com/">Lodash Official Documentation</a>을 참고하여 만들어졌음을 밝힙니다.

Lodash는 기능적 프로그래밍 패러다임을 사용하여 일반적인 프로그래밍 작업을위한 유틸리티 기능을 제공하는 JavaScript 라이브러리입니다.

라고 공식적으로 전달하는데, 이는 즉 개발자들에게 편의성을 주는 라이브러리 라는 것이다.

## 설치방법

브라우저 환경

```html
<script src="lodash.js"></script>
```

NPM

```javascript
npm i --save lodash
```

NodeJS 환경

```javascript
const _ = require('lodash')
const __ = require('lodash/core')
const fp = require('lodash/fp')
const array = require('lodash/array')
const object = require('lodash/fp/object')
const at = require('lodash/at')
const curryN = require('lodash/fp/curryN')
```

## Array

### _.chunk

chunk는 배열을 일정한 글자 수에 맞추어 나누는 것이다.

```javascript
_.chunk([1,2,3,4],2)
// return [[1,2],[3,4]]
_.chunk([1,2,3,4],3)
// return [[1,2,3],[4]]
```

### _.compact

compact함수는 배열에서 거짓의 값을 제거하여 주는데 false,null,0,"",undefined등 모든 거짓 값을 검열한다.

```javascript
_.compact([0,1,false,2,'',3])
// return [1,2,3]
// 0 또한 검열된다.
```

### _.concat

concat함수는 기존의 javascript함수와 매우 유사하게 작동한다
요소들을 한 배열에 묶어 얕은복제해주는 것

```javascript
const array = [1]
const other = _.concat(array,2,[3],[[4]])

console.log(other)
// return [1,2,3,[4]]

console.log(array)
// return [1]
```

### _.difference

difference함수는 두 번째 배열을 기준으로 첫 번째 인자로 들어온 배열 중 없는 값을 반환합니다.

```javascript
_.difference([2,1], [2,3])
// return [1]
```

### _.differenceBy

differenceBy함수는 difference함수와 매우 유사하게 동작하지만 2번째 인자 값의 폭을 늘려주는 함수 삽입이 가능하다

```javascript
_.differenceBy([2.1, 1.2], [2.3, 3.4], Math.floor)
// 2.3, 3.4가 있는지 먼저 비교 
// Math.floor(2.3) => 2의 값과 Math.floor(첫 번째 인자 배열 하나하나) 비교
// 2.1은 값이 같기 때문에 return 되지않음
// return [1.2]
```

### _.differenceWith

differenceWith함수는 위 두 가지 함수와 같은 역할을 한다.

```javascript
const obj = [{ x:1, y:2 }, { x:2, y:1 }]
_.differenceWith(obj, [{ x:1, y:2}], _.isEqual)
// _.isEqual함수는 ===와 같은 역할을 한다.
// 즉 x가 1이며, y값이 2인 인자를 찾아 제외
// 남은 return 값은 [{ x:2, y:1 }]
```

### _.drop

drop함수는 두 개의 인자를 받을 수 있는데.

1. Number배열
2. [제거하고 싶은 개수]

```javascript
_.drop([1, 2, 3])
// 두 번째 인자 값이 없기 때문에 하나의 개체가 삭제됨 [2, 3]
_.drop([1, 2, 3], 2)
// return [3]
_.drop([1, 2, 3], 5)
// return []
_.drop([1, 2, 3], 0)
// return [1, 2, 3] 두 번째 인자의 값을 0으로 정해줘야만 삭제되지 않음
```

### _.dropRight

drop함수와 삭제 방향이 반대일 뿐 모두 같음

```javascript
_.dropRight([1, 2, 3])
// return [1, 2]

_.dropRight([1, 2, 3], 2)
// return [1]

_.dropRight([1, 2, 3], 5)
// return [0]

_.dropRight([1, 2, 3], 0)
// return [1, 2, 3]
```

### _.dropRightWhile

2가지 인자를 받는데, 해당 배열에서 false를 반환할 때 까지 오른쪽 을 기준으로 삭제한다.

1. 배열
2. 함수

```javascript
const users = [
    { user: 'barney', active: true },
    { user: 'fred', active: false },
    { user: 'pebbles', active: false },
]

_.dropRightWhile(users, (o) => !o.active)
// o는 각각의 users배열의 index정보가 들어가며 즉 !active === false를 반환하는 barney만 출력됨 
// return ['barney']
```

### _.dropWhile

위 RightWhile과 방향만 다를 뿐 같은 역할을 수행한다 즉

```javascript
const users = [
    { user: 'barney', active: false },
    { user: 'fred', active: false },
    { user: 'pebbles', active: true },
]

_.dropRightWhile(users, (o) => !o.active)
// return ['pebbles']
```

### _.fill

fill함수는 매우 많은 인자가 올 수 있으나 첫 번째는 변화를 줄 배열, 두 번째는 채워넣을 값 이다.

```javascript
const arr = [1, 2, 3]

_.fill(arr, 'a')
// return ['a', 'a', 'a']

_.fill(Array(3), 2)
// return [2, 2, 2]

_.fill ([4, 6, 8, 10], '*', 1, 3)
// 첫 번째 인자부터 3까지의 arr.length를 *로 대체함
// return [4, '*', '*', 10]
```

### _.findIndex

findIndex함수는 일치하는 가장 빠른 Index의 값을 출력해주는 함수이다.

```javascript
const users = [
    { user: 'barney', active: false },
    { user: 'fred', active: false },
    { user: 'pebbles', active: true}
]

_.findIndex(users, (o) => o.user === 'barney')
// return 0

_.findIndex(users, { user: 'fred', active: false})
// return 1

_.findIndex(users, ['active', false])
// return 0 (가장 빠른 Index)
```

### _.findLastIndex

findLastIndex함수는 findIndex함수의 방향만 다를 뿐 같은 역할을 수행한다.

```javascript
const users = [
    { user: 'barney', active: true },
    { user: 'fred', active: false },
    { user: 'pebbles', active: false }
]

_.findLastIndex(users, (o) => o.user === 'pebbles' )
// return 2

_.findLastIndex(users, { user: 'barney', active: true})
// return 0

_.findLastIndex(users, ['active', false])
// return 2
```

### _.flatten

flatten함수는 인자로 배열을 입력받아 한 겹을 벗겨내주는데 자세한건 아래 예제를 보자

```javascript
_.flatten([1, [2, [3, [4]], 5]])
return [1, 2, [3, [4]], 5]
```

### _.flattenDeep

flattenDeep함수는 배열이 몇 겹이라도 모두 벗겨내어 1차원 적인 배열을 만들어준다.

```javascript
_.flattenDeep([1, [2, [3, [4]], 5]])
// return [1, 2, 3, 4, 5]
```

### _.flattenDepth

flattenDepth는 몇 겹의 Array를 제거할 것인지 두 번째 인자로 받아 호출된다.

```javascript
const array = [1, [2, [3, [4]], 5]]

_.flattenDepth(array, 1)
// return [1, 2, [3, [4]], 5]

_.flattenDepth(array, 2)
// return [1, 2, 3, [4], 5]
```

### _.fromPairs

fromPairs함수는 배열로 전달받은 값들을 하나의 Object로 묶어서 return한다.

```javascript
_.fromPairs([['a', 1], ['b', 2]])
// return { a: 1, b: 2 }
```

### _.head

head함수는 인자로 들어온 배열의 첫 번째 Index값을 return한다.

```javascript
_.head([1, 2, 3])
// return 1

_.head([])
// return undefined
```

### _.indexOf

indexOf함수는 Vanila JS와 마찬가지로 첫 번째 인자배열의 두 번째 인자 Index결과를 return해준다.

```javascript
_.indexOf([1, 2, 1, 2], 2)
return 1
```

### _.initial

initial함수는 배열의 마지막 index를 제외한 나머지 배열을 반환한다.

```javascript
_.initial([1, 2, 3])
// return [1, 2]
```

### _.intersection

intersection함수는 첫 번째 인자 배열에 포함되어있는 수 중 모든 배열에 공통으로 있는 수에 대하여 반환을 하는데 아래와 같다.

```javascript
_.intersection([2, 1], [2, 3])
// return [2]
```

### _.intersectionBy

intersectionBy함수는 위 intersection과 같이 동작하지만 여러 인자를 받는다.

```javascript
_.intersectionBy([2.1, 1.2], [2.3, 3.4], Math.floor)
// return [2.1] 즉 2.3이 Math.floor의 영향으로 2로 취급되며 2.1을 내림 한 값과 같아져 반환됨
```

### _.intersectionWith

intersectionWith는 객체 단위로 테스트를 진행하는데 세 번째 인자를 기준으로 테스트하며 기준에 적합한다면 반환한다.

```javascript
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }];
const others = [{ x: 1, y: 1 }, { x: 1, y: 2 }]

_.intersectionWith(objects,others,_.isEqual)
// return [{ x: 1, y: 2 }] 가 _.isEqual을 통과하기에 반환됨
```

### _.join

join함수는 첫 번째 인자배열을 두 번째 인자로 합쳐주는 문자열 변환 역할을 수행한다.

```javascript
_.join(['a', 'b', 'c'], '~')
// return 'a~b~c'
```

### _.last

last함수는 인자로 받은 배열의 마지막 인덱스를 출력하는 역할을 수행한다.

```javascript
_.last([1, 2, 3])
// return 3
```

### _.lastIndexOf

lastIndexOf는 끝 자리에서부터 원하는 Index를 출력해주는데,

```javascript
_.lastIndexOf([1, 2, 1, 2], 2)
// return 3 즉 세 번째 숫자1의 위치를 말하는 것
```

### _.nth

nth함수는 첫 번째 인자로 받은 배열의 값 중 두 번째 인자로 준 수의 내용을 출력하는 함수이다.

```javascript
const array = ['a', 'b', 'c', 'd']

_.nth(array, 1)
// return 'b'

_.nth(array, -2)
// return 'c'
```

### _.pull

pull함수는 배열에서의 불필요한 값 없애는 역할을 수행한다

```javascript
const array = ['a', 'b', 'c', 'a', 'b', 'c']

_.pull(array, 'a', 'c')
console.log(array)
// return ['b', 'a', 'b', 'c']
```

### _.pullAll

pullAll함수는 기존의 pull함수와 같은 역할을 수행하지만 중복되는 값 까지 모두 없애는 역할을 수행한다.

```javascript
const array = ['a', 'b', 'c', 'a', 'b', 'c']

_.pullAll(array, ['a', 'c'])
console.log(array)
// return ['b', 'b']
```

### _.pullAllBy

pullAllBy함수는 배열객체를 필터링 하는 곳에 사용이 된다.
첫 번째 인자로 배열을 받은 후 두 번째 조건에 의해 필터링 되며 세 번째 인자에 해당하는 데이터를 기준으로 필터링 된 데이터를 출력한다. 

```javascript
const array = [{ x: 1 }, { x: 2 }, { x: 3 }, { x: 1 }]

_.pullAllBy(array, [{ x: 1 }, { x: 3 }], 'x')
console.log(array)
// return [{ x: 2 }]
```

### _.pullAllWith

pullAllWith함수는 위의 pullAllBy와 매우 유사하게 동작한다

```javascript
const array = [{ x: 1, y: 2 }, { x: 3, y: 4 }, { x: 5, y: 6 }]

_.pullAllWith(array, [{ x: 3, y: 4 }], _isEqual)
// return [{ x: 1, y: 2 }, { x: 5, y: 6 }]
```

### _.pullAt

pullAt함수는 첫 번째 인자로 배열을 받은 후 두 번째 인자배열로 들어온 인덱스를 추출한다. 깊은 복사로 기존 배열또한 변화된다.

```javascript
const array = ['a', 'b', 'c', 'd']
const pulled = _.pullAt(array, [1, 3])

console.log(array)
// return ['a', 'c']

console.log(pulled)
// return ['b', 'd']
```

### _.remove

remove함수는 첫 번째 인자배열을 받은 후 두 번째 함수를 받아 원래의 배열에서 특정 조건을 만족하는 수 들을 따로 빼오는 곳에 사용된다.

```javascript
const array = [1, 2, 3, 4]
const evens = _.remove(array, (n) => {
    return n % 2 === 0
})

console.log(array)
// return [1, 3]

console.log(evens)
// return [2, 4]
```

### _.reverse

reverse함수는 인자로 배열을 받은 후 해당 배열의 요소들을 역순으로 재정렬해준다.

```javascript
const array = [1, 2, 3]

_.reverse(array)
// return [3, 2, 1]

console.log(array)
// return [3, 2, 1]
```

### _.sortedIndex

sortedIndex함수는 이진법을 이용한 정렬로 첫 번째 인자로 배열을 받은 후 두 번째 인자로 받은 수 가 오름차 순으로 배열에 삽입되려면 어느 인덱스에 위치해야하는지 알려준다.

```javascript
_.sortedIndex([30, 50], 40)
// return 1
```

### _.sortedIndexBy

sortedIndexBy함수는 Object를 인덱싱하기 위하여 쓰는 함수로 기능은 sortedIndex함수와 매우 유사하다

```javascript
const objects = [{ x: 4 }, { x: 5 }]

_.sortedIndexBy(objects, { x: 4 }, (o) => o.x)
// return 0
```
### _.sortedIndexOf

sortedIndexOf함수는 중복되는 여러가지 값 또한 정렬이 가능하게 해주며 중복이 되는 수 중 가장 먼저 오게 인덱스 값을 반환해준다 즉,

```javascript
_.sortedIndexOf([4, 5, 5, 5, 6], 5)
// return 1
```

### _.sortedLastIndex

sortedLastIndex함수는 첫 번째 인자로 들어온 배열에서 두 번째 인자로 들어온 값이 존재할 수 있는 가장 마지막 인덱스를 반환한다.

```javascript
_.sortedLastIndex([4, 5, 5, 5, 6], 5)
// return 4
```

### _.sortedLastIndexBy

sortedLastIndexBy함수는 첫 번째 인자로 들어온 배열객체중 두 번째 인자가 위치할 수 있는 가장 뒤 쪽 인덱스 번호를 반환해준다.

```javascript
const objects = [{ x: 4 }, { x: 5 }]

_.sortedLastIndexBy(objects, { x: 4 }, (o) => o.x)
// return 1
```

### _.sortedLastIndexOf

sortedLastIndexOf함수는 첫 번째 인자로 받은 배열 중 두 번째 인자로 받은 수가 들어갈 수 있는 가장 뒤 쪽 인덱스 번호를 반환한다.

```javascript
_.sortedLastIndexOf([4, 5, 5, 5, 6], 5)
// return 3
```

### _.sortedUniq

sortedUniq함수는 인자로 받은 배열중 중복값을 모두 제거한 순수한 배열만을 반환해준다.

```javascript
_.sortedUniq([1, 1, 2])
// return [1, 2]
```

### _.sortedUniqBy

sortedUniqBy함수는 첫 번째 인자로 들어온 배열 중 두 번째 인자로 들어오 조건에 의해서 중복되지 않은 값의 배열만을 반환하며 조건에 가까울 수록 우선순위가 된다.

```javascript
_.sortedUniqBy([1.1, 1.2, 2.3, 2.4], Math.floor)
// return [1.1, 2.3]
```

### _.tail

tail함수는 인자로 들어온 배열 중 첫 번째 인덱스를 가진 요소만 제외하고 반환한다.

```javascript
_.tail([1, 2, 3])
// return [2, 3]
```

### _.take

take함수는 첫 번째 인자로 들어온 배열 중 두 번째 인자로 들어온 수 만큼 잘라내어 반환해준다.

```javascript
_.take([1, 2, 3])
// return 1

_.take([1, 2, 3], 2)
// return [1, 2]

_.take([1, 2, 3], 5)
// return [1, 2, 3]

_.take([1, 2, 3], 0)
// return []
```

### _.takeRight
_
takeRight함수는 첫 번째 인자로 들어온 배열 중 두 번째 인자로 들어온 수 만큼 오른쪽을 기준으로 잘라내어 반환한다.

```javascript
_.takeRight([1, 2, 3])
// return [3]

_.takeRight([1, 2, 3], 2)
// return [2, 3]

_.takeRight([1, 2, 3], 5)
// return [1, 2, 3]

_.takeRight([1, 2, 3], 0)
// return []
```

### _.takeRightWhile

takeRightWhile함수는 첫 번째 인자 배열객체를 받고 두 번째 인자 조건 중 조건식에서 false를 반환할 때 까지 오른쪽 부터 실행된다.

```javascript
const users = [
    { user: 'barney', active: true },
    { user: 'fred', active: false },
    { user: 'pebbles', active: false }
]


_.takeRightWhile(users, (o) => !o.active)
// return ['fred', 'pebbles'] 
```

### _.takeWhile

takeWhile함수는 위 takeRightWhile함수와 매우 유사하게 작동하며 왼쪽부터 실행된다.

```javascript
const users = [
    { user: 'barney', active: false },
    { user: 'fred', active: false },
    { user: 'pebbles', active: true }
]

_.takeWhile(users, (o) => !o.active)
// return ['barney', 'fred']
```

### _.union

union함수는 첫 번째 인자로 들어온 배열을 두 번째 인자로 들어온 배열과 합쳐주는 것을 말하며 정렬은 되지않고 중복값은 제거된다.

```javascript
_.union([2], [1, 2])
// return [2, 1]
```

### _.unionBy

unionBy함수는 union함수와 매우 비슷한 역할을 실행하지만,
배열객체 등 더 다양한 형식의 요소들을 합칠 수 있다는 장점이 있다.

```javascript
_.unionBy([2.1], [1.2, 2.3], Math.floor)
// return [2.1, 1.2]
// 2.1 과 2.3 은 Math.floor상 같은 값으로 처리되므로 2.3 은 중복값취급 되어 생략됨
```

### _.unionWith

unionWith함수는 배열객체를 합치기 위하여 사용된다. 사용법은 union함수와 같다.

```javascript
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }]
const others = [{ x: 1, y: 1 }, { x: 1, y: 2 }]

_.unionWith(objects, others, _.isEqual)
// return [{ x: 1, y: 2 }, { x: 2, y: 1 }, { x: 1, y: 1 }]
```

### _.uniq

uniq함수는 인자로 들어온 배열을 중복 값을 제거한 형태로 반환해준다.

```javascript
_.uniq([2, 1, 2])
// return [2, 1]
```

### _.uniqBy

uniqBy함수는 첫 번째 인자로 들어온 배열을 두 번째 형식에 맞게 중복값을 제거하여 반환해준다.

```javascript
_.uniqBy([2.1, 1.2, 2.3], Math.floor)
// return [2.1, 1.2]
```

### _.uniqWith

uniqWith함수는 uniqBy함수와 동일하게 작동하나 인자로 배열객체를 받는다는 차이점이 있다.

```javascript
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }, { x: 1, y: 2 }]

_.uniqWith(objects, _.isEqual)
// return [{ x: 1, y: 2 }, { x: 2, y: 1 }]
```

### _.unzip

unzip함수는 zip함수로 묶어놓은 압축 상태를 해제하는 함수이다

```javascript
const zipped = _.zip(['a', 'b'], [1, 2], [true, false])
// return [['a', 1, true], ['b', 2, false]]

_.unzip(zipped)
// return [['a', 'b'], [1, 2], [true, false]]
```

### _.unzipWith

unzipWith함수는 이미 압축된 zip형태의 배열을 다른 옵션을 추가하여 다시 재압축시키는 함수이다.

```javascript
const zipped = _.zip([1, 2], [10, 20], [100, 200])
// return [[1, 10, 100], [2, 20, 200]]

_.unzipWith(zipped, _.add)
// return [3, 30, 300]
// _.add는 두 항목을 sum하는 함수이다.
```

### _.without

without함수는 첫 번째 인자로 받은 배열에서 N번째로 받은 인자값들이 포함되어있다면 제외한 나머지를 출력하는 함수이다.

```javascript
_.without([2, 1, 2, 3], 1, 2)
// return [3]
```

### _.xor

xor함수는 논리연산의 xor을 생각하면 쉬운데 즉 같은 값을 제외한 나머지를 의미한다. 첫 번째 인자로 받은 배열과 두 번째 인자로 받은 배열에서 공통되지 않은 값 만을 출력한다.

```javascript
_.xor([2, 1], [2, 3])
// return [1, 3]
```

### _.xorBy

xorBy는 기존 xor함수에 추가 인자로 조건식을 받아서 필터링을 할 수 있다.

```javascript
_.xorBy([2.1, 1.2], [2.3, 3.4], Math.floor)
// return [1.2, 3.4]
```

### _.xorWith

xorWith의 역할을 xorBy와 같으며 배열객체를 받아 사용이 가능하다.

```javascript
const objects = [{ x: 1, y: 2 }, { x: 2, y: 1 }]
const others = [{ x: 1, y: 1 }, { x: 1, y: 2 }]

_.xorWith(objects, others, _.isEqual)
// return [{ x: 2, y: 1 }, { x: 1, y: 1 }]
```