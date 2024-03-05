# Promise Generic type



~~~typescript
const promise = new Promise((resolve, reject) => resolve(45))
promise.then(result => result * 4) // Error
~~~

- 이때 typescript는 result를 {}로 추론하여 에러가 발생 

~~~typescript
const promise = new Promise<number>((resolve, reject) => resolve(45))
promise.then(result => result * 4) // 180
~~~



## resolve, reject type이 다른 경우

- resolve의 type만 지정하면된다.
-  reject는 이미 any타입으로 지정이 되어있다 