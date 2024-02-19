# nest



## nest project 시작

~~~ bash
npm i -g @nestjs/cli  // nest 프레임워크 설치
nest new project-name // nest 프로젝트 파일 생성(project-name에 . 을 붙이면 현재 파일에 생성)
~~~



## nest 어플리케이션 실행

~~~ bash
npm run start 				 // nest 실행
npm run start:dev      // 개발자모드로 실행
npm run start:debug
npm run start:prod
~~~



## 기본구조

- main.ts(변경불가) : 사용하는 module을 호출하며 포드 설정 등  어플리케이션 통합설정을 해준다

- module.ts : 어플리케이션의 단위이며 구현하는 기능의 단위가 된다

  - ~~~ bash
    nest g mo  // g: generate mo: module 모듈 생성 명령어 
    ~~~

- controller.ts : url의 요청을 받아주며 service에 반환을 넘겨준다 

  - ~~~bash 
    nest g co  // g: generate co: controller  컨트롤러 생성 명령어
    ~~~

- service.ts : controller에서 받은 주소에 대응하여 비지니스 로직을 구현하여 준다 

  - ~~~bash
    nest g s  //  g: generate s : service 서비스 생성 명령어
    ~~~

- pakage.json : 설치된 라이브러리 등을 관리



## nest 문법



### Controller url 컨트롤

~~~typescript
import {Body, Controller, Delete, Get, Param, Patch, Post, Put, Query} from '@nestjs/common';

@Controller('movies')
export class MoviesController {

    @Get()
    getAll(){
        return 'This will return all movies';
    }

    @Get("search")  // '/' 생략 가능  id 밑에 있으면 search를 id로 인식해서 movieId 부분에 search로 나옴
    search(@Query("year") searchingYear:string){
        return `We are searching for a movie made after: ${searchingYear}`
    }

    @Get('/:id')  // :?? 이 있다면 이 밑에 Get은 정상 작동하지 않는 문제가 있다
    getOne(@Param('id') movieId:string){
        return `This will return one movie with the id: ${movieId}`;
    }

    @Post()
    create(@Body() movieData){
        console.log(movieData);
        return 'This will create a movie';
    }

    @Delete('/:id')
    remove(@Param('id') movieId:string){
        return `This will delete a movies with the id: ${movieId}`;
    }

    @Patch('/:id')
    patch(@Param('id') movieId:string, @Body() updateData){
        return {
            updateMovie: movieId,
            ...updateData
        }
    }


}
~~~

- @Controller() : 컨트롤러임을 의미하며 현재 모듈의 공통 주소를 써줄 수 있다
  - 보통 클레스에 붙여주며 클래스 밑으로 @Get과같은 요청과 데코레이터에 함수들이 붙어있는 형태 
- @Get() : get요청을 해줄 수 있으며 리소스를 조회 
- @Post() : post요청을 하며 리소스를 생성 
- @Delete() : 리소스 삭제 
- @Put() : 리소스를 전부 업데이트
- @Patch() : 이소스의 일부만 업데이트
- @Param() : '/:??'과 같이 변하는 url값을 가져올 수 있다 이때 '??'부분과 Param괄호에 값은 같아야 하며 바로 뒤에 매개변수는 같지 않아도 된다  
- @Body() : 바로 뒤에 오는 매개변수에 post로 만든 값이 저장된다  
- @Query() : 쿼리문에 들어오는 값을 받아준다. 괄호에 쿼리 키값을 적어주면 매개변수로 벨류값을 받아준다 



## DTO(Data Transfer Object)

프로세스 간에 데이터를 전달하는 객체를 의미하며 id값처럼 자동으로 생성되는 값이 아닌 순수하게 전달하고 싶은 데이터만 담겨있는 객체이다. 

### DTO를 이용한 유효성 검사

~~~bash 
npm i class-validator     // i는 install약자
npm i class-transformer 
~~~



#### validationPipe 

~~~bash
npm i @nestjs/mapped-types  // partialtype 사용을 위하여 설치
~~~

- mapped-types : 타입을 변환시키고 사용할 수 있는 패키지 







## test



- cov
- watch
- unit test : function 하나하나를 따로 테스팅
- e2e : 페이지 이동시 특정 페이지가 나와야 하는 경우/ 사용자가 취할 만한 액션들을 테스트 