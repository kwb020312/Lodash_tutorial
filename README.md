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