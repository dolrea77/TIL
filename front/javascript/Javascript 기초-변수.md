# Javascript 기초



## let

ES6이전에 사용하던 변수 선언문인 var는 더이상 사용하기엔 적합하지 않다



### 1. var hoisting

var로 변수를 선언하기도 전에 변수에 값을 할당하거나 사용할 때 에러가 뜨지 않는 것

(hoisting : 어디에 선언했는지 상관 없이 선언을 제일 위로 끌어 올려주는 것)

```javascript
console.log(age)   //undefined
age = 4;
var age;   
console.log(age)  //4
```



### 2. 블록 스코프 무시

var는 블록을 무시하여 블록안에서 선언된 변수를 블록 밖에서도 사용할 수 있다 

즉 어디서 선언이 되었는지 모르는 값들이 혼재되어 나올 수도 있다

```javascript
{
    var age = 4;
}
console.log(age);  //4
```



위와 같은 단점을 극복하고자 let이 생김 





## Constants

바뀔 수 없는 값 상수(Immutable)이다

장점

- security : 해커들이 변수의 값을 임의로 변경하는 것을 차단한다 
- thread safety : 여러 쓰레드에서 동시에 변수에 접근할때 안전하다 
- reduce human mistakes : 코드 변경 시 실수로 인한 변수 변형이 일어나지 않음 



 ## 데이터 타입

종류 

- number

- string

- boolean

- null : 비어 있다는 '값'

- undefined : 비어있는지 아닌지 정해지지도 않아 알 수 없는 값

- symbol : 고유한 식별자가 필요시 사용 

  ```javascript
  const symbol1 = Symbol('id');
  const symbol2 = Symbol('id');
  console.log(symbol1 === symbol2); //false
  
  const gSymbol1 = Symbol.for('id');
  const gSymbol2 = Symbol.for('id');
  console.log(gSymbol1 === gSymbol2); //true
  
  //Symbol 타입은 출력 시 .description을 사용하여 string으로 변환 해주어야 한다 
  console.log(`value: ${symbol1.description}, type: ${typeof symbol1}`)
  ```

- object



## Dynamic typing

데이터 타입을 선언하지 않고 자동으로 선언되게 하는 것

```javascript
let text = 'hello';
console.log(`value: ${text}, type: ${typeof text}`); //value: hello, type: string
text = 1;
console.log(`value: ${text}, type: ${typeof text}`); //value: 1, type: number
text = '7' + 5;
console.log(`value: ${text}, type: ${typeof text}`); //value: 75, type: string
text = '8' / '2';
console.log(`value: ${text}, type: ${typeof text}`); //value: 4, type: number
```

중간에 number로 데이터타입이 바뀐 'text' 변수를 String타입으로 생각하여 인덱싱하게 된다면 런타임 에러가 발생하게 된다 (이로인하여 typescript가 생김)