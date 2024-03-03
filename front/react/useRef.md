# useRef

- 저장공간으로서의 기능
- DOM요소를 선택하는 기능 



## 저장 공간으로서의 기능



### react에서 변수를 잘 사용하지 않는 이유

- 값을 UI에 반영하지 않음(console.log로만 확인 가능)
- 렌더링 시 값이 초기값으로 돌아가게 된다 



### useState + 변수 = useRef

- useState
  - 장점 : 렌더링이 일어나도 값이 유지가된다
  - 단점 : 값이 변할때 마다 UI변경을 위하여 렌더링을 해준다
- 변수
  - 장점 : 값이 변하여도 렌더링이 일어나지 않는다
  - 단점 : 렌더링이 일어나면 값이 초기화가 된다 
- useRef
  - 렌더링이 일어나도 값을 유지해주며 값이 변화한다고 렌더링이 발생하지 않는다 
  - UI에 바로 반영될 필요가 없는 값들을 변수처럼 사용하고 싶을 때 사용한다
    - useState를 자주 사용하여 렌터링이 많이 일어나면 자원 소모가 커진다 
  - 객체 형태로 값이 저장됨 
    - 객체의 값에 접근하려면 current를 통하여 접근한다 

```react
const refCount = useRef(0);

return (
  <div>ref : {refCount.current}</div> //렌더링 되야 UI에 값이 반영된다 
	<button onClick={() => {
      refCount.curren++;		//버튼을 누르면 값이 증가하지만 렌터링이 일어나지 않기때문에 UI변화는 없다
    }}></button>
)
```





## DOM요소를 선택하는 기능



### react에서 document를 사용하지 않는 이유

- jsx라는 것을 사용하게 되면서 js에 html을 녹여 내서 사용하기 때문에 직접 접근이 가능하기 때문 
- 하지만 특정 태그에 접근하여 값을 바꾸어 주어야 하는 일이 생길 수도 있음 (style값 등)



### useRef의 태그 선택 기능

- js에서는 태그에 id를 만들어 다른 태그에서 접근을 하였다면 react에서는 useRef를 이용하여 다른 태그에 접근을 하도록 한다  

```react
//비어있는 useRef를 생성
const inputEl = useRef(null);

return (
	<div>
    //ref를 이용하여 해당 태그를 useRef로 선택해줌
  	<input type="text" ref={inputEl} />
    //버튼을 클릭하면 ref를 이용하여 다른 태그에 접근하도록 한다 
    <button onClick={() => inputEl.current.focus()}>검색</button> //버튼을 클릭하면 인풋창이 focus된다 
  </div>
);
```

