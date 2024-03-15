 # React.Fragment

- 리엑트의 엘리먼트들은 반드시 단 하나의 최상위 태그로 묶여 있어야 한다 

- <React.Fragment></React.Fragment> 로 사용하며 줄여서 <></>로 사용한다 

  - 리엑트에서 실제 돔에 노드를 추가하지 않고 엘리먼트를 묶어 줄 수 있다 
  - React를 import 해주어야 한다 

  

  

  ## 활용 예시 

  

  ```react
  import React from 'react';
  
  const Component = () => {
      return (
      	<>
          	<h1>aa</h1>
          	<p>bb</p>
          </>
      )
  }
  
  export default Component;
  ```

  

  - 만약 위와같은 컴포넌트가 있을 때 <></>가 아닌 <div></div>를 사용 했다면 상위 컴포넌트에서 위 컴포넌트에 바로 접근하는 것이 아닌 div를 거쳐서 접근을 하여야 정상적으로 css를 바꾸어 줄 수 있게 된다 

```react
//App.js
function App = () {
    return (
    	<div className="App">
        	<table>
            	<tbody>
                	<tr>
                    	<Column />
                    </tr>
                    <tr>
                    	<Column />
                    </tr>
                </tbody>
            </table>
        </div>
    );
}



//Column.js
const Column = () => {
    return (
    	<>
        	<td>aa</td>
        	<td>bb</td>
        	<td>cc</td>
        </>
    );
}

```

- 위와 같이 정해진 구조가 있는 table같은 경우 중간에 반복되는 구조를 컴포넌트로 만들때 <div>태그가 구조 중간에 들어가게 된다면 문법 오류가 발생하게 된다
- 하지만 <></>을 사용 해준다면 구조를 망치지 않고 엘리먼트를 넣어 줄 수 있다 

```react
//Column.js
const Column = () => {
    const list = ['aa', 'bb', 'cc'];
    return (
    	<>
			list.map((li, idx) => (
        		<React.Fragment key={idx}>			//반복문 안에 넣어준 엘리먼트 또한 <>로 묶어주어야 함 
        			<td>{li}</td>
        			<td>{li}</td>
        		</React.Fragment>
    		);
        </>
    );
}
```

- map과 같은 반복문에 return값 엘리먼트는 key으로 묶어주는데 key를 넣어줄 <div>를 대체한다면 <React.Fragment>를 사용 할 수 있다
- 하지만 줄인 <>태그를 사용할 수 없고 반드시 <React.Fragment>를 명시 해주고 key값을 넣어주어야 한다 
- <React.Fragment>에 사용할 수 있는 prop은 key가 있으며 그외에는 업데이트로 추가 되었을 수도 있으니 확인이 필요하다 