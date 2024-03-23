# javascript 문법



## 함수

- 함수와 함수호출은 다름

  - add : add라는 함수
  - add() : add라는 함수를 호출하여 나오는 return값 

  ```javascript
  const add = (a, b) => a + b;
  
  function calculator(func, a, b) {
      return func(a, b);
  }
  
  calculator(add, 3, 5); //8
  
  //매개변수가 없는 add함수의 리턴값이 calculator의 매개변수로 들어감
  calculator(add(), 3, 5); //undefind + undefind(a, b) 가 되어버림 
  
  const click = () => () => {...};
  
  //만약 return값이 함수이고 의도와 맞다면 호출형태로 쓸 수 있다 
  calculator(click(), 3, 5);  
  ```

- 함수 리턴값으로 함수가 들어가는 것을 고차 함수라 한다  



### 호출 스택

- 함수의 호출은 스택구조로 실행된다 
- 함수의 선언을 먼저 읽고 기억해둔다음 호출이 되었을 때 선언된 함수로 가게되고 그안에 또다른 함수가 있으면 또 한번 그함수의 선언부로 가게되며 이 함수가 끝나야 처음 함수를 이어서 진행하게 되어 스택구조라고 하며 선입후출 구조라고 하게 된다 

```javascript
const a = () => { return const x = x; }

const b = () => { 
    const y= y;
	a();
}

//먼저 b함수가 메모리스택에 올라가서 연산되다가 a함수 호출을 만나 a함수의 선언부로가서 메모리 스택에 a함수를 올리게 된다
//a함수가 끝나게되면 메모리스택에서 a함수가 나가고 다시 b함수로 돌아와 나머지를 진행하고 b함수가 메모리 스택에서 나가게된다
//FILO
b();  
```

