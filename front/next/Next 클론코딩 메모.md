Next 클론코딩 메모



- 페이지를 만들때 layout의 틀을 미리 만들어 두면서 화면을 구성해 나가는 것이 일반적 이다 
- css 를만들때 '.클래스명' 에서 '.클래스명 태그명' 하면 그 클래스에서 해당태그에만 적용되는 css를 만들 수 있게 된다 

- css 에서 container를 잡은후 display를 flex로 잡고 그안에서 원하는 비율로 레이아웃을 잡아준 뒤 다시 display를 flex로 잡아준다 이때 가운데 정렬을 하고싶다면 오른쪽 왼쪽 모두 flex-grow를 1씩 주어서 여유를 주면 나뉜 레이아웃이 가운데 정렬이 된다 
- 태그에서 css에 justify-content를 space-between을 준다면 그 자식 태그간에 최대한 거리를 두게 된다 
- 부모태그의 크기값을 그대로 가져오려면 값에 inherit를 써주면 부모태그의 크기를 그대로 가져와 준다(포지션이 fixed라서 100%가 잘 맞지 않는다면 주로 사용)
  - fixed는 스크롤을 내려도 고정되는 화면을 설정시 사용한다 (position: fixed;)
- flex로 layout비율을 정하기 위해서는 부모 태그에 display: flex; 를 가져야 한다 
  - 자식태그에 flex:1; 을 준다면 빈공간을 최대한 차지하게되고 두개의 자식태그가 둘다1 이라면 1대1비율을 가지게 된 
-  block vs inline
  - block : 해당 태그의 영역에서 width값을 100%로 가지게되며 그다음태그는 block태그의 밑으로 나오게 된다, 주로 박스형태를 가진다 
    - 대표적인 block tag : div, h1, p
  - inline : 주로 텍스트를 주입하며 컨텐츠의 크기만큼 영역이 잡힌다 
    - 대표적인 inline tag : span, a, button 
  - inline-block : inline 과 block의 특징을 모두 가진 요소
    - 줄바꿈이 이루어지지 않는다
    - block처럼 width height를 지정 할 수 있다 
    - width height를 지정하지 않으면 inline과 같이 컨텐츠마큼 영역이 잡힌다 
- svg 복사할 시 해당 svg HTML을 선택 후 우클릭 복사에서 outer HTML  복사를 선택하여 복사한다 
  - svg는 fill로 색칠한다 
- backdrop-filter: blur(12px);  : 뒤에화면을 반투명 블러 처리를 할 수 있도록 한다 
- 폰트 바꾸기 
  - 원하는 css::placeholder   해주고 안에 font-family: Malgun Gothic;  -맑은 고딕으로 폰트 변경 
- z-index : 자신의 깊이 개념
  - auto : 부모의 요소를 따라감
  - 0 : 자신의 위치
  - 양수 : 우선순위를 높일 수 있다 
  - 음수 : 우선순위를 낮출 수 있다 
- position: absolute; : 해당 구역에 어떤 태그가 있어도 상관없이 위치를 조정할 수 있으며 이것을 이용하여 의도적으로 겹치게 태그를 배치할 수도 있다 



next 훅

보통 리엑트 훅과 onClick과같은 이벤트 리스너 같은 것 이 있다면 use client를 써야 할 확률이 높다 

그렇기 때문에 훅이나 이벤트 리스너를 사용한다면 따로 컴포넌트를 만들어서 사용하는 것이 편하다 

- useSelectedLayoutSegment : 주소를 이동시에 현재 컴포넌트 위치에서 보이는 파일명(주소 경로)을 반환해주는 훅이다 

  - localhost:3000/home  -> home
  - localhost:3000/compose/tweet-> conpose  : 현재 훅을 사용한 컴포넌트위치에서 보이는 경로가 compose일때 

- useSelectedLayoutSegments : 주소를 이동시에 해당경로 파일명(주소 경로)을 모두 반환 , '/'는 포함하지 않고 배열로 반환해준다

- usePathname : 도메인 주소 다음부터 쿼리 스트링 전까지 '/' 까지 모두 포함해서 반환해준다 

  - ```typescript
    const pathname = usePathname();
    if(pathname === '/explore')        
    ```

- useRouter : 주소를 바꾸어 주는 훅 , useSearchParams : 현재 쿼리 값을 가져올 때 사용

  - ```typescript
    'use client'
    import {useRouter, useSearchParams} from "next/navigation";
    
    const router = useRouter();
    const searchParams = useSearchParams();
    
    const onClickBt(){
        router.replace(`/search?q=${searchParams.get('q')}`)
    }
    
    const onClickBtn(){
        // searchParams.toString은 현재 쿼리값을 모두 쓸때 사용 
        router.replace(`/search?q=${searchParams.toString()}&f=live`)
    }
    ```

  - 어떠한 주소를 현재 주소를 기준으로 바꾸어주고 싶을 때 활용









createContext API

- props가 아닌 다른 방식으로 컴포넌트 간에 값을 전달하는 방법 
- 보통 한화면 에서 서로 다른 데이터를 갈아 치울 때 사용한다

- createContext는 use client에서 사용
- 같은 용도로 React query와 zustand를 사용할 수 있다 

```typescript
'use client'

import {createContext, useState, ReactNode} from 'react';

export const TabContext = createContext({
    tab: 'rec',
    setTab: (value: 'rec' | 'fol') => {},
});

type Props = {children: ReactNode}

export default function TabProvider({children}: Props) {
    const [tab, setTab] = useState('rec');
    
    return (
    	<TabContext.Provider value={{tab, setTab}}>				//자식 컴포넌트에 tab과 setTab을 보내준다 
        	{children}
		</TabContext.Provider>
    )
}
```

- 여기서 만들어 준 TabProvider의 자식 컴포넌트들은 tab값과 setTab을 사용할 수 있게 된다 



옵셔널 체이닝

- 타입스크립트에서 간단한 조건문 앞에 구문이 true일때 뒤에 구문이 실행 되게 해주는 것
  - imageRef.current?.click(); : imageRef.current 가 null이 아니면 click() 을 실행한다 





라이브러리 

npm trends 에서 라이브러리의 현재 트랜드를 확인 할 수 있다 



dayjs

post게시글 에서 게시글 작성 시간을 계산해서 ~시간 전 등을 표시해 줄 수 있게 된 라이브러리

```bash
npm i dayjs
```





```typescript
import dayjs from 'dayjs';
import relativeTime from 'dayjs/plugin/relativeTime';  // fromNow를 쓸수있도록 하는 플러그인
import 'dayjs/locale/ko';   // 한글 플러그인 

dayjs.extend(relaitveTime);    // dayjs 확장 해줌 
dayjs.locale('ko');  한글 플러그인 사용 

dayjs('생성 시간').fromNow()  //생성시간으로 부터 ~전
dayjs('생성 시간').fromNow(true)  //생성시간으로 부터 ~   '전' 이 빠짐
```



classnames

className을 조건부로 가질 수 있도록 해주는 라이브러리  

```bash
npm i classnames
```



```typescript
'use client'
import cx from 'classnames';
import style from './actionbuttons.module.css'

export default function ActionButtons(){
    return (
         // &&앞 구문이 true가 되면 style.commented가 합쳐지게 된다 
    	 <div className={cx(style.commentButton, commented && style.commented)} /> 
         <div className={cx(style.commentButton,{[style.commented]: commented})} /> 
    )
}
```



```css
.commentButton.commented{
    두개의 클래스를 모두 사용하는 경우의 css 
}
```





searchParams

-  next에서 page.tsx에 기본적으로 가져와 줄 수 있는 props 이다
- 쿼리문을 가져올 수 있다 

```typescript
type Props = {
    searchParams: {q?: string}; // searchParams에서 q라는 쿼리문의 값이 string type 이다, q값이 없을 수도 있어 ?(옵션)
}

export default function Search({searchParams}:Props){
    searchParams.q   // 쿼리문 value를 가져올 수 있다 -> 도메인?q=value
    return (
        <SearchForm q={searchParams.q} />  // 컴포넌트에 props로 보내 줄 수도 있다  
    )
}
```

