# Node.js 에서 환경 변수 다루기

 

## 환경 변수

- 여러 환경에 동일한 애플리케이션을 배포하려면 환경 변수를 사용 해야 함 
- 어떠한 환경에 배포 되느냐에 따라서 다르게 설정되야하는 값들을 환경 변수를 통하여 관리함 
- 환경 변수 파일에 API키나 password같은 민감한 정보들을 넣어 소스 공유 시 노출이 되지 않도록 할 수 있다 
- 모든 OS전반에 걸쳐 적용되는 변수 이다 
- 환경변수에 따라 개발 서버와 운영 서버의 변수 값 들을 변경해서 사용  할 수 있다   



## Node.js 환경 변수 접근

- process.env를 통하여 환경 변수 접근 

  - process : Node.js에 기본적으로 내장된 전역 객체 => 별도로 불러올(import) 필요 없음

- dotenv : node.js에서 환경 변수를 관리하기 위한 모듈  

  - npm i dotenv로 설치하고 .env라는 파일을 만들어 준다

  - .env파일에서 환경 변수 생성 시 key =value 형식으로 생성해 준다

    - react에서는 key값이 REACT_APP_변수명 형식으로 지어 주어야 한다 

  -  next.config.js 파일에서 dotenv를 설정하여 .env파일을 참조할 수 있도록 해 준다

    - ```javascript
      import dotenv from 'dotenv'
      
      ~~
        dotenv.config({path : '.env있는 위치, 없으면 괄호 빈칸으로'});  
      ~~
      ```

  - 필요한 곳에서 process.env.key값 을 이용하여 불러온다

  - gitignore에 .env파일을 추가한다 

