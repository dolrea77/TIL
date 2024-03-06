# Custom Hooks 2



## useFetch 

```react
import {useEffect, useState} from 'react';
import {useFetch} from './useFetch';

//더미 데이터를 보내주는 api
const baseUrl = "https://jsonplaceholder.typicode.com";

function App() {
    //custom hooks 사용전
    const [data, setData] = useState(null);
    
    const fetchUrl = (type) => {
        fetch(baseUrl + '/' + type)
        .then((res) => res.json())
        .then((res) => setData(res));
    }
    
    //첫 화면은 users 화면을 보여준다
    useEffect(() => {
        fetchUrl("users");
    }, []);
    
    //custom hooks 사용
    
    //custom hooks가 반환하는 값에 맞추어 값을 받아준다 return 객체 => const 객체
    const {data, fetchUrl} = useFetch(baseUrl, "users");
     
    return (
    	<div>
        	<h1>useFetch</h1>
            <button onClick={() => fetchUrl("users")}>Users</button>
            <button onClick={() => fetchUrl("posts")}>Posts</button>
            <button onClick={() => fetchUrl("todos")}>Todos</button>
            //javascript값을 json형태로 바꾼다 이때 들여쓰기를 2칸으로 한다 
            <pre>{JSON.stringify(data, null, 2)}</pre>
        </div>
    )
}

export default App;
```



```react
import {useEffect, useState} from 'react';

export function useFetch(baseUrl, initialType) {
    const [data, setData] = useState(null);
    
    const fetchUrl = (type) => {
        fetch(baseUrl + '/' + type)
        .then((res) => res.json())
        .then((res) => setData(res));
    }
    
    useEffect(() => {
        fetchUrl(initialType);
    }, []);
    
    return {
        data,
        fetchUrl
    }
}
```



