# 컴포넌트 분할과 Children Prop



## 컴포넌트 분할

```react
// UserProfile 컴포넌트
function UserProfile({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age} years old</p>
    </div>
  );
}

// UserList 컴포넌트
function UserList({ users }) {
  return (
    <div>
      {users.map((user) => (
        <UserProfile key={user.id} name={user.name} age={user.age} />
      ))}
    </div>
  );
}
```

- 장점	
  - 재사용성 : 많은 웹 애플리케이션들이 공통적으로 사용하는 특정 기능 또는 UI 요소들을 공통 컴포넌트로 분할 하여 만들면, 이를 필요한 곳에서 재사용 할 수 있게 된다. 따라서 코드의 중복을 줄이고, 유지보수를 편리하게 만들어 주는 역할을 한다.
  - 가독성 : 기능 또는 뷰 별로 컴포넌트를 잘 분할 해둔다면 코드를 이해하거나 수정하는데 도움이 된다.



## Children prop

```react
// Card 컴포넌트
function Card({ children }) {
  return <div className="card-style">{children}</div>;
}

// Card 컴포넌트의 사용
//h2,p 태그가 children props를 통해 전달된다 
<Card>
  <h2>안녕하세요!</h2>
  <p>React 학습 중입니다.</p>
</Card>
```

- 장점
  - 재사용성 : children prop을 사용하면, 공통 구조를 가진 컴포넌트를 쉽게 재사용할 수 있다
    - ex) 동일한 스타일과 레이아웃을 가진 컴포넌트 안에 다른 내용을 삽입하는 경우
  - 유연성 : children prop은 JSX 요소 뿐만 아니라 문자열, 숫자, 배열 등 어떤 종류의 데이터도 받을 수 있다. 또한 컴포넌트 자체도 받을 수 있으므로, 이를 이용해 동적으로 컴포넌트를 조합 할 수도 있다.
  - 가독성 : 컴포넌트의 시작태그와 종료 태그 사이에 내용을 직접 삽입할 수 있기 때문에 코드를 읽기 쉽다.
  - 코드의 명확성 : 어떤 컴포넌트가 자식 컴포넌트를 어떻게 가지고 있는지, 그리고 그 자식 컴포넌트들이 어떻게 조합되는지 코드 상에서 명확하게 확인 할 수 있다. 