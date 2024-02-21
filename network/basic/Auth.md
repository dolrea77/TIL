# Auth

- 유저를 검증하는 기능 



## Cookie

- 브라우저는 쿠키를 이용하여 클라이언트의 데이터를 넣을 수 있다 
  - 브라우저가 유저를 기억 하므로 인증이 필요한 요청 시 마다 로그인을 하지 않아도 된다 
- 브라우저에서 요청을 보낸 후 서버에서 응답을 받을 때 브라우저에 저장하고자 하는 쿠키가 있을 수 있다 
  - 페이지에 요청 시 쿠키값도 같이 보내게 됨 
- 쿠키는 도메인에 따라 제한된다 
  - 응답으로 받은 쿠키는 같은 도메인에서만 요청 시 쿠키를 같이 보낼 수 있음 
- 쿠키는 유통기한이 있다 
  - 서버가 기한을 정한다 
- 쿠키는 브라우저에서만 사용할 수 있으며 앱에서는 사용 할 수 없음 



## Session

- http 프로토콜은 stateless 이다
  - stateless : server로 가는 request는 모두 독립적이여서 각각의 request가 데이터를 공유하지 않고 request가 끝나면 데이터가 사라진다 
  - 이러한 특징으로 server에 request를 할때 마다 어디에서 보낸 request인지 함께 보내주어야 함 
- 매번 클라이언트의 정보를 담아 request를 보내지않고 session을 이용하게됨
  - 처음 server에 클라이언트 인증 정보를 담아(로그인 id, pw 와 같은 정보) request를 보낸다
  - server는 받은 인증정보를 session DB에 저장을 하고 session ID를 응답으로 받는다
  - server는 session ID를 cookie에 담아 브라우저에 response한다
  - 브라우저는 서버에 request를 보낼때 마다 유저정보를 보내지않고 cookie에 session ID를 담아 보내주게된다
  - server는 session ID로 session DB에 있는 클라이언트를 구분하고 유저정보를 받아와 페이지를 response할 수 있다 
- session DB는 현재 로그인한 모든 유저의 정보가 저장되게 된다 
  - server에 요청이 있을 때 마다 session DB를 조회해야 한다 

### session의 장점

- 유저를 session DB기반으로 추적할 수 있다
  - 특정 유저의 계정을 삭제하거나 유저정보를 이용하여 연동 되어있는 계정을 자유롭게 로그아웃 등을 할 수 있다 

### session의 단점

- 유저정보를 저장해야 하므로 DB를 사고 유지하여야 함 
  - redis 사용 



## Token

- 모바일 환경 앱에서는 브라우저에 있는 쿠키를 사용할 수 없기 때문에 token을 사용하게 된다 
- token은 무작위의 string으로 되어 있으며 sever에 token을 보내면 session DB에서 token과 일치하는 유저를 찾게된다 



## JWT

- token 형식의 유저 인증 
- session DB가 없어도 되기 때문에 server가 DB를 조회하지 않게되 부담이 적어진다 
  - 유저정보를 server에 보내게 된다 
  - 유저정보를 회원 DB에서 확인 한다 
  - 유저정보가 맞다면 server는 유저의 정보 일부(ID 등)를 가져다가 사인 알고리즘을 이용 하여 사인을 하게됨(Access Token)
  - 사인된 정보를 string형태로 클라이언트에게 보낸다 
  - token(사인정보)를 server에 보내면 해당 사인이 유효한지 체크하고 유저를 인증한다 

### jwt 장점

- DB를 사고 유지할 필요가 없다

### jwt단점

- 특정 유저를 추적 할 수 없다 
  - 토큰만료를 기다렸다가 특정유저를 차단하여야함 
- 서비스가 크다면 session 방식으로 유저를 관리하는 것이 좋다



### Refresh Token을 이용한 단점 극복

- Access Token의 유효기간이 짧다면 자주 로그인을 해야하며 유효기간이 길다면 Access Token이 탈취 당했을 때 보안에 취약해진다
- 이때 Refresh Token을 이용하여 단점을 보안할 수 있게 된다
  - 사용자가 로그인을 하여 서버에 정보를 보낸다
  - 회원DB에서 사용자를 확인한다 
  - Access Token과 Refresh Token을 발급한다
    - Access Token은 유효기간을 짧게 하고 Refresh Token은 비교적 길게 설정한다(서버 주도적)
    - 이 때 Refresh Token은 회원 DB에도 저장이 된다 
  - 사용자에게 Access Token과 Refresh Token을 보내준다
  - 서버에 Access Token과 함께 데이터 요청을 보내면 서버에서 검증을 하여 응답을 한다
  - Access Token이 만료가 된다면 Refresh Token을 함께 서버에 보낸다
    - Access Token의 유효기간은 Payload를 통해 사용자에서도 알 수 있으므로 만료가 된것을 알게되면 API요청을 보낼 때 Refresh Token을 같이 보내게 된다 
  - 서버는 Access Token의 만료를 확인하면 회원 DB의 Refresh Token을 확인하고 유효기간이 지나지 않았다면 Access Token을 재발급 해 준다
  - 서버는 새로운 Access Token을 헤더에 실어 다시 요정을 진행한다 

#### 장점

- 기존 Access Token만 있을 때보단 안전하다

#### 단점

- 구현이 복잡하다
- Access Token이 만료될 때 마다 새롭게 발급하는 과정에서 서버의 자원 낭비가 발생 한다



