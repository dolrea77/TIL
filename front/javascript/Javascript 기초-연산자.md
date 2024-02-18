# Javascript 기초



## or 

- || 기호 사용
- 왼쪽부터 조건확인하여 true가 하나라도 나온다면 true를 반환한다 
  - 가장오래 걸리는 로직의 조건을 오른쪽에 두어 최대한 실행되기 전에 true면 true가 나오도록 한다 
  - 만약 오래걸리는 로직이라고 해도 최종true false에 기여도가 매우 높다면 맨 왼쪽으로두어 한번에 로직으로 종료를 시킬수도 있다



## and 

- && 기호 사용

- 왼쪽부터 조건 확인하여 false가 하나라도 있으면 false를 반환한다

  - 가장 오래 걸리는 로직의 조건을 오른쪽에 두어 최대한 실행되기 전에 false면 false가 나오도록 한다
  - 만약 오래걸리는 로직이라고 해도 최종true false에 기여도가 매우 높다면 맨 왼쪽으로두어 한번에 로직으로 종료를 시킬수도 있다

- null 체크를 할때 활용 가능

  ```javascript
  nullableObject && nullableObject.something // nullableObject가 null이 아닐때만 값을 가져온다 
  ```

  - if문을 사용하여 길게 값을 가져오는것 보다 간편 



## not 

- ! 기호 사용



## Equality

값이 같다



### loose equality

- 기호는 ==
- 타입을 변경하여 검사 

```javascript
const stringFive = '5';
const numberFive = 5;

console.log(stringFive == numberFive); //true
console.log(stringFive != numberFive); //false
```

- null == undefined //true



### strict equality

- 기호는 ===
- 타입을 변경하지 않고 검사

```javascript
const stringFive = '5';
const numberFive = 5;

console.log(stringFive === numberFive); //false
console.log(stringFive !== numberFive); //true
```

- null === undefined //false



## Ternary operator 

- 형식 : condition ? value1 : value2;

```javascript
console.log(name === 'ellie' ? 'yes' : 'no')
```

- 가독성을 위하여 간단한 조건문에만 사용하는 것을 권장 