# useReducer

- state를 생성하고 관리하는  훅
- 여러개의 하위값을 포함하는 복잡한 state를 다루어야 할 때 사용한다 



## 구성요소

- reducer : state를 업데이트 하는 역할 
- dispatch : state 업데이트를 위한 reducer에 요구를 해준다
- action : 요구의 내용을 나타낸다 



## 사용법

```react
//컴포넌트 외부
//reducer 함수가 불리는 시점의 aaa state의 현재값이 reducer state에 들어가게된다
//즉 reducer를 통하여 aaa state를 수정 한다 
const reducer = (state, action) => {
  //업데이트될 state값, return될 때마다 렌더링 일어남 
  switch (action.type) {
    case 'deposit' : 
      return state + action.payload;
    case 'withdraw' :
      return state - action.payload
    default:
      return state;
  } 
}
const [number, setNumber] = useState(0);
//새로운 state와 dispatch를 배열로 받아주며 첫번째 매개변수로는 reducer를 두번째는 state의 초기값을 넣어준다 
//dispatch 함수를 호출하면 reducer가 실행된다 
const [aaa, dispatch] = useReducer(reducer, 0);

return (
	<>
  	<button onClick={() => {
      //dispatch의 매개변수로 action값을 넣어준다, 이때 action값은 객체 형태이다 
      dispatch({type: "deposit", payload: number})
    }}>더하기</button>
  <button onClick={() => {
      //dispatch의 매개변수로 action값을 넣어준다, 이때 action값은 객체 형태이다 
      dispatch({type: "withdraw", payload: number})
    }}>빼기</button>
  </>
)
```

