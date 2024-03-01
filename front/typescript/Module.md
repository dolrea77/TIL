# Module

- 대규모 웹사이트의 등장으로 코드가 복잡해지며 문제가 발생하여 모듈화를 하게 됨
  - 기능별로 의존성을 줄여 기능 개선 및 수정이 편해짐
  - 각 모듈들은 모듈만의 네임스페이스를 가지게 되어 변수명이 같아 충돌하는 문제가 없어짐
  - 똑같은 코드를 반복하지 않고 필요할 때 마다 사용할 수 있음 
- import 또는 export가 있는 파일은 module로 취급이 된다
- import는 모듈에서 데이터를 불러올 때, export는 모듈에서 데이터를 내보낼 때 사용 



## JS의 모듈 시스템

### commonjs

```javascript
//module.js
const hello = 'module';

//하나의 결과값을 보내줄 때는 module.exports를 이용하여 보내준다.
module.exports = hello;

//module2.js

//객체형태로 여러 모듈을 보내줄 때는 exports.객체명 을 이용해서 보내준다
exports.a = 'b';		
exports.b = false;

//또는 {}로 묶어서 보내준다 => module.exports는 하나의 값만 보내기 때문에 하나로 묶어서 보내준다 
//exports.객체명 과 module.exports를 함께쓰면 module.exports값만 보내지게 된다 
module.exports = {
  a: 'b',
  b: false
}
```



```javascript
//run.js
const hi = require('./module');    //require('./module'); 이 자체가 hello라는 모듈임

console.log(hi)  // module

//run2.js
const { a, b } = require('./module'); //여러 객체이므로 사용할 객체를 {}로 묶어서 가져온다

console.log(a); //b
console.log(b); //false
```







## TS의 모듈 시스템

### es2015(esnext)

~~~typescript
//module.ts

//commonjs에서 exports 같은 역할이며 객체를 보내 줄 수 있다
const a: string = 'b';   
export const b: boolean = false;

//commonjs의 module.exports의 단점인 exports값을 module.exports가 덮어씌워 보내 버린다는 것을 해결
// default는 export, export defaule를 별개로 보게되며 같이 보낼 수 있게 됨
export default function() {
  
};

export { a };

---------------------------------------------
//만일 commonjs형태의 모듈이 있다면
const a = 'b';

module.exports = a;
~~~



```typescript
//run.ts

//export default는 모듈에 하나뿐이기 때문에 import 작명 을 해주어 사용 할 수 있다 
// 이때 export, export default는 {}의 여부로 구분한다 
import hi, { a, b } from './module';
//import를 따로 할 수도, 함께 쓸 수도 있다 
import hi from './module';

console.log(a, b);
console.log(hi());

-----------------------------------------------
//import 작명 from 경로 => 이 형태는 default 사용시 사용 
//esModuleInterop: true 를 해야 import hi from './module'로 쓸 수 있다(바추)
import * as hi from './module';

console.log(hi);
```

