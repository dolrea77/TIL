# useContext



## Context API

- 기존 react는 규모가 큰 프로젝트에서 전역적으로 필요한 데이터가 있을 경우 단계별로 props를 전달 해 주어야 한다
- context는 app안에서 전역적으로 사용되는 데이터들을 여러 컴포넌트에서 쉽게 공유할 수 있게 해준다 
- context로 공유한 데이터를 useContext 훅을 이용하여 필요한 컴포넌트에서 사용 할 수 있다 

### 단점

- 컴포넌트의 재사용하기 어려워 질 수 있다
- prop drilling을 피하기 위한 목적이라면 Component Composition(컴포넌트 합성)을 먼저 고려해보자 

```react
//app.js

//context 미사용
const [isDark, setIsDark] = useState(false);

return <Page isDark={isDark} setIsDark={setIsDark} />


-------------------------------
//page.jsx
    
const Page = ({isDark, setIsDark}) => {
    return (
    	<div className="page">
        	<Header isDark={isDark} />
            <Content isDark={isDark} />
            <Footer isDark={isDark} setIsDark={setIsDark} />
        </div>
    );
};

-------------------------------------------------
//Header.jsx

const Header = ({isDark}) => {
    return (
    	<header
            className="header"
            style={{
                backgroundColor: isDark ? 'black' : 'lightgray',
                color: isDark ? 'white' : 'black', 
            }}
            >
            	<h1>Welcome</h1>
        </header>
    );
};
```



```react
//ThemeContext.js

import {createContext} from "react";

export const ThemeContext = createContext(null);

// app.js

import {ThemeContext} from './context/ThemeContext';

function App() {
    const [isDark, setIsDark] = useState(false);
	
	return (
    	<ThemeContext.Provider value={{isDark, setIsDark}}>
        	<Page/>
        </ThemeContext.Provider>
    );
}


//page.jsx

    return (
    	<div className="page">
        	<Header/>
            <Content/>
            <Footer/>
        </div>
    );
};

//Header.jsx

const Header = () => {
    const {isDark} = useContext(ThemeContext);
    return (
    	<header
            className="header"
            style={{
                backgroundColor: isDark ? 'black' : 'lightgray',
                color: isDark ? 'white' : 'black', 
            }}
            >
            	<h1>Welcome</h1>
        </header>
    );
};
```

