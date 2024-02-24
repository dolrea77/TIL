# Secure & HttpOnly



## Secure

- 네트워크를 감청하여 쿠키를 가로채갈 수도 있다, 이를 막기위하여 HTTPS 프로토콜을 사용하여 예방한다 
  - HTTPS : 비대칭 암호키를 이용하여 데이터를 암호화 할 수 있는 프로토콜
- 개발자의 실수로 src를 http로 보내게된다면 암호화 하지 않은 쿠키를 서버로 전달하게 된다 
- secure를 사용하면 https 일때만 cookie를 보내게 된다

```javascript
'Set-Cookie':[
    'Secure=Secure; Secure'  // 키=벨류; Secure 설정
]
```





## HttpOnly

- HttpOnly 속성이 설정되어 있지 않으면 스크립트 언어를 이용해 XSS 공격이 가능하다 
  - XSS(크로스 사이트 스크립팅) : 공격자가 상대방의 브라우저에 스크립트를 실행되도록 하여 개인정보를 가로채는 공격  
- 서버에서 브라우저로 쿠키값이 왔지만 console에서 javascript로 접근을 할 수 없게 해준다 

```javascript
'Set-Cookie':[
    'HttpOnly=HttpOnly; HttpOnly'  // 키=벨류; HttpOnly 설정
]
```

