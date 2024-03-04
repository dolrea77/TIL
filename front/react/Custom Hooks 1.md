# Custom Hooks 1

- 중복되는 코드를 커스텀하여 훅으로 사용 가능하다
- 커스텀 훅 안에 기존의 훅도 사용 가능하다
- 각각의 커스텀 훅은 서로 다른 state와 effect를 가지기 때문에 재사용성이 좋다 



## useInput 만들어보기

- 커스텀 훅은 독립적인 상태값과 effect를 가지기 때문에 커스텀 훅을 여러개 써서 각각 컨트롤 할 수 있다
- 중복된 코드를 줄여 가독성이 좋아진다 

```react
import {useState} from 'react';
import {useInput} from './useInput';

//확인 버튼 클릭 시 실행할 함수 
function displayMessage(message) {
    alert(message);
}

function App(){
    //커스텀 훅 미사용
    const [inputValue, setInputValue] = useState('');
    
    const handleChange = (e) => {
        setInputValue(e.target.value);
    };
    
    const handleSubmit = () => {
        alert(inputValue);
        setInputValue('');
    };
    
    //커스텀 훅 사용
    //커스텀 훅 useInput의 return값대로 받아준다 
    const [inputValue, handleChange, handleSubmit] = useInput('', displayMessage);
    
    return(
    	<div>
        	<h1>useInput</h1>
            <input value={inputValue} onChange={handleChange} />
            <button onClick={handleSubmit}>확인</button>
        </div>
    );
}

export default App;
```



```react
import { useState } from "react";

//매개변수로 input박스 안에 들어갈 초기값과 확인버튼 클릭시 일어나는 함수를 넣어준다 
export function useInput(initialValue, submitAction) {
    const [inputValue, setInputValue] = useState(initialValue);
    
    const handleChange = (e) => {
        setInputValue(e.target.value);
    };
    
    const handleSubmit = () => {
        //확인버튼 누르면 input박스 내용 초기화
        setInputValue("");
        //매개변수로 들어온 함수에 inputVlaue값을 넣어주고 실행
        submitAction(inputValue);
    }
    
    return [inputValue, handleChange, handleSubmit];
}
```

