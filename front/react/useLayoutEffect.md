# useLayoutEffect

- useEffect와 사용 방법이 같다
- useEffect는 화면이 모두 업데이트가 되면 콜백 함수가 실행이 된다 (effect 실행)
  - 처음 실행 될 경우 제외 
- useLayoutEffect는 콜백 함수(effect 실행)가 실행완료 후 화면이 업데이트 된다 



## 사용 예시

```react
import { useLayoutEffect, useEffect, useState } from "react";

function App(){
    const [count, setCount] = useState(0);
    
    //useEffect 사용
    useEffect(() => {						
        console.log("useEffect", count);
    }, [count]);
    
    //useLayoutEffect 사용
    useLayoutEffect(() => {						
        console.log("useLayoutEffect", count);
    }, [count]);
    
    
    const handleCountUpdate = () => {
        setCount(count + 1);
    };
    
    return (
    <div>
            <p>Count: {count}</p>
            <button onClick={handleCountUpdate}>Update</button>
    </div>
    );
}

export default App;


//console
useLayoutEffect 0  
useEffect 0
```

- 버튼을 누르면 카운트가 증가
- 위의 코드에서 useEffect가 위에 있고 useLayoutEffect가 아래에 있어 같은 동작을 할 때 useEffect가 먼저 동작하여 console에 나와야 하지만 useLayoutEffect가 먼저 실행된 것을 볼 수 있다 
- 실행 순서
  - useLayoutEffect -> 컴포넌트 렌더링 -> useEffect
- useEffect는 비동기 적으로 실행되지만 useLayoutEffect는 동기적으로 실행된다 
  - useLayoutEffect안에 내용이 오래걸린다면 컴포넌트의 렌더링이 오래 걸릴 수 있다 



```react
import { useRef, useLayoutEffect, useEffect, useState } from "react";

function getNumbers() {
    return [1, 2, 3, 4, 5, 6, 7 ,8, 9, 10, 11, 12, 13, 14, 15];
}

function App(){
    const [numbers, setNumbers] = useState([]);
    const ref  = useRef(null);

	useEffect(() => {
        const nums = getNumbers();
        setNumbers(nums);
    }, []);
    
    //useEffect
    useEffect(() => {
        if (numbers.length === 0) {
            return;
        }
        
        ref.current.scrollTop = ref.current.scrollHeight;
    }, [numbers]);
    
    //useLayoutEffect
    useLayoutEffect(() => {
        if (numbers.length === 0) {
            return;
        }

        ref.current.scrollTop = ref.current.scrollHeight;
    }, [numbers]);
    
    return (
    <div
        ref={ref}
        style={{
                height: "300px",
                border: "1px solid blue",
                overflow: "scroll",
            }}
        >
        	{numbers.map((number, idx) => (
            	<p key={idx}>{number}</p>
            ))}
        </div>
    );
}

export default App;
```

- 동작
  - 어떠한 값들을 받으면 박스안에 그값을 넣는다, 이때 값이 박스 밖을 벗어난다면 스크롤을 적용해서 박스 밖에 나가지 않게 해준다	
  - 그리고 스크롤은 제일 밑에 값이 보이도록 내려가있도록 한다 
- 만약 웹사이트가 연산이 많을 경우 useEffect를 이용하였다면 스크롤이 내려가지 않았다가 내려가는 딜레이가 생길 수 있다 
  - 첫번째 useEffect로 인하여 state가 변경된다
  - 컴포넌트가 update된다
  - 두번째 useEffect가 어떠한 이유로 오랜 시간이 걸려서 실행이 되었다
  - 이미 그려진 화면이 출력이 되다가 두번째 useEffect가 동작이 완료되면 바뀐 화면이 적용되게 된다 
- useLayoutEffect을 두번째 useEffect대신 넣어준다면 스크롤내려가기 전 모습을 보이다가 내려가는 딜레이가 사라진다
  - 컴포넌트의 update전 useLayoutEffect가 실행되며 동기적으로 실행되어 완료 후에 update가 된다
  - 화면 렌더링자체의 딜레이가 생길 수 있지만 스크롤이 이미 내려가있는 화면을 정확하게 보여주게 된다  