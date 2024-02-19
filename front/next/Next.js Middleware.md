# Next.js Middleware

- next.js에서 페이지를 렌더링하기 전에 실행되는 함수
- 서버로 요청을 보낼 시 서버로 가기 전 request 값을 받아 response를 줄 수 있다 
- 캐시된 페이지보다 먼저 실행이 된다



## 활용법

- 페이지 렌더링 전에 인증을 확인하거나 요청을 한다
- 요청 데이터를 사전에 처리하거나 특정 API요청을 수행
- 캐시를 관리
- 요청에 대한 응답을 변환하거나 에러를 처리할 수 있다 



## 사용법

- middleware.ts파일은 pages경로와 같은 위치에 만든다 

  ```typescript
  // middleware.ts
  import { NextResponse } from 'next/server'
  import type { NextRequest } from 'next/server'
  
  // This function can be marked `async` if using `await` inside
  export function middleware(request: NextRequest) {
    return NextResponse.redirect(new URL('/about-2', request.url))
  }
  
  // See "Matching Paths" below to learn more
  export const config = {
    matcher: '/about/:path*',
  }
  ```

- middleware의 파라미터 값으로 NextRequest와 NextResponse를 사용할 수 있어 요청 응답을 핸들링 할 수 있다. 

- 기본적으로 모든 파일시스템의 정적인 콘텐츠들에 대한 요청에서도 동작함

- matcher 값을 지정해주지 않으면 원치 않는 요청까지 미들웨어를 거치는 비효율이 발생 한다 

  ```typescript
  export const config = {
    matcher: [
      /*
       * Match all request paths except for the ones starting with:
       * - api (API routes)
       * - _next/static (static files)
       * - _next/image (image optimization files)
       * - favicon.ico (favicon file)
       */
      '/((?!api|_next/static|_next/image|favicon.ico).*)',
    ],
  }
  ```

- 모든 page route에 미들웨어를 적용 한다면 위와같이 작성하면 된다 

  - /((?!).*) 은 부정 선행 주시 이며 앞문자 '/'뒤로 적힌값을 제외한 모든 문자열을 선택한다는 의미이다 
  - 이곳에 다른 pathname을 적는다면 그 url은 미들웨어를 사용하지 않게 된다 
  - 뒤에 *이 있기때문에 적힌값 뒤로 다른 pathname이 이어져도 미들웨어를 사용하지 않게 된다 



## 응답 조작

### redirect 

- 오는 요청에 대한 경로를 다른 URL로 redirect 시킨다 

  ```typescript
  return NextResponse.rewrite(new URL('/me/categories', request.nextUrl.origin))
  ```

### rewrite

- 오는 요청에 대한 경로는 유지하고 rewrite하는 URL의 응답을 보여준다

- redirect와의 차이는 주소창에 변화가 없기 때문에 rewrite는 사용자가 URL변형을 알 수 없다 

  ```typescript
  return NextResponse.rewrite(new URL('/me/categories', request.nextUrl.origin))
  ```

  

