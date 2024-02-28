# 제너레이터 함수(Generator function)

- 함수의 실행을 중간에 멈췄다가 재개할 수 있는 기능 



## 사용법

```javascript
function* fn() {	// generator 함수는 * 을 붙여 표시한다 
    console.log(1);
    yield 1;
    console.log(2);
    yield 2;
    console.log(3);
    console.log(4);
    yield 3;
    return "finish";
}

const a = fn();

// next메서드를 이용하여 generator 함수를 실행시켜주며 가장 가까운 yield를 만날 때 까지 실행한다 
a.next(); // 1   반환된 객체 : {value: 1(yield 값), done: false(함수전체가 끝나면 true)} 
a.next(); // 2	 반환된 객체 : {value: 2, done: false}
a.next(); // 3 4 반환된 객체 : {value: 3, done: false}
a.next(); //     반환된 객체 : {value: "finish", done: true}
a.next(); //     반환된 객체 : {value: undefined, done: true}
```



### 메소드 종류

- next() : 순차적으로 yield를 만날때까지 함수를 실행하고 멈추어 준다 이때 멈춘 위치는 기억하고 있다
- return() : 함수가 끝나지 않았어도 return이 나오면 바로 done가 true가 된다
  - a.return('반환된 객체의 value값')
- throw() : 에러가 반환되고 done가 true가 된다
  - a.throw(new Error('에러 구문')) 

## Generator

- iterable : 반복이 가능하다
  - Symbol.iterator 메서드가 있다
  - Symbol.iterator는 iterator를 반환해야 한다
- iterator
  - next 메서드를 가진다
  - next 메서드는 value 와 done 속성을 가진 객체를 반환한다
  - 작업이 끝나면 done은 true가 된다 

```javascript
function* fn(){
    yield 4;
    yield 5;
    yield 6;
}

const a = fn();

a[Symbol.iterator]() === a;  // true

for(let num of a){
    console.log(num);
}

// 4  5  6  각 반환값의 value값이 num으로 들어가서 나오게 된다  => done이 true가 될때까지 반복
// for of 문을 통하여 generator 함수 사용 
```



``` javascript
function* fn(){
    const num1 = yield "첫번째 숫자를 입력해주세요";
    console.log(num1);
    
    const num2 = yield "두번째 숫자를 입력해주세요";
    console.log(num2);
    
    return num1 + num2;
}

const a = fn(); 

a.next();  // {value: "첫번째 숫자를 입력해주세요", done: false}
a.next(2); // 2  => num1에 2가 저장됨 즉, next에 인자를 넣어주면 value값이 된다 
a.next(4); // 4  반환된 객체 : {value: 6, done: true}
```



```javascript
function* fn(){
    let index = 0;
    while(true){
        yield index++;
    }
}

const a = fn();


next.a();   // {value: 1, done: false}
next.a();   // {value: 2, done: false} => 무한반복문을 원하는 만큼 사용 가능하게 컨트롤 할 수 있다 
```



```javascript
function* gen1(){
    yield "w";
    yield "o";
    yield "r";
    yield "l";
    yield "d";
}

function* gen2(){
    yield "Hello,";
    yield* gen1();
    yield "!";
}

// yield* 외부 generator 함수 사용 및 반복 가능한 모든 객체도 가능 
console.log(...gen2()); // Hello, w o r l d !  ...gen2 : done이 true가 될때까지 펼쳐주는 역할 
```

