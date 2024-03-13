# reduce()

- 배열 요소를 하나로 줄여주는 함수 



```javascript
const numbers = [1,2,3,4];

//forEach
let total = 0;
numbers.forEach((number) => {
    total = total + number;
});
console.log(total)  //10

//reduce
//accumulator, currentValue는 다른 이름이여도 상관 없음 
const total = numbers.reduce((accumulator, currentValue) => {
    return accumulator + currentValue
}, 0)
```

- reduce의 인자로 받는 함수를 reducer함수 라고 한다
- reducer 함수는 두가지 매개변수를 전달받는다
  - accumulator(첫번째 매개변수) : 현재까지 누적된 값 
  - currentValue(두번째 매개변수) : 현재 처리중인 요소를 뜻
- reduce의 두번째 인자는 accumulator의 초기값이 된다 
- return된 값이 다음 accumulator값이 된다 
  - 요소를 모두 돌고 반환되는 값이 reduce의 최종 반환 값이 된다  



| 요소 | accumulator | currentValue | 반환값 |
| ---- | :---------- | ------------ | ------ |
| 1    | 0           | 1            | 1      |
| 2    | 1           | 2            | 3      |
| 3    | 3           | 3            | 6      |
| 4    | 6           | 4            | 10     |



```javascript
//최솟값 찾기
const numbers = [10, 4, 2, 8];

const smallest = numbers.reduce((accumulator, currentValue) => {
    if(accumulator > currentValue){
        return currentValue
    }
    return accumulator
});
console.log(smallest); // 2
```

- reduce의 두번째 인자(초기값)를 비우면 accumulator가 첫번째 요소가 되고 currentValue는 두번째 요소부터 돈다  
  - reducer함수는 첫번째 요소를 넘어간다고 볼 수 있다 



| 요소 | accumulator | currentValue | 반환값 |
| ---- | ----------- | ------------ | ------ |
| 10   | -           | -            | -      |
| 4    | 10          | 4            | 4      |
| 2    | 4           | 2            | 2      |
| 8    | 2           | 8            | 2      |

