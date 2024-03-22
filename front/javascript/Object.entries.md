# Object.entries

- 객체의 key와 value를 하나의 배열로 바꾸어주고 배열이 모여 2차원배열 형태가 된다 
- 객체의 key나 value에 접근하기 위하여 반복문을 사용하여 값들을 꺼내어 주는 작업이 필요하다
- Object.entries로 배열로 바꾸어준뒤 Object.fromEntries로 다시 객체로 변환해주면 반복문을 사용하지 않는다 



## 사용법

```javascript
const obj = {
    hotdog: 5,
    buger: 8,
    pizza: 10,
};

//value값을 *2해줄 때
//반복문 사용
for (let o in obj) {
    obj[o] *= 2;
}

//Object.entries사용
Object.fromEntries(Object.Entries(obj).map((v) => [v[0],v[1]*2]));
```

- Object.entries로 변환된 이차원 배열의 형태를 iterable이라고 한다 
  - 반복가능한 이라는 뜻으로 배열이 이터러블이다 

