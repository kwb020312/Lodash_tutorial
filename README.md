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