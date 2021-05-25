# 허성빈 [201840235]
## [05월 25일]
> 오늘 배운 내용 요약
##### 요청과 응답
 - express 모듈 설치 명령어
     > $ npm install express@4
 - 웹 서버가 하는 일은 요청과 응답의 연속이라고 정의할 수 있다.
  - 예를 들어 웹 브라우저에 네이버 웹 페이지 주소를 입력하면 웹 페이지를 제공하라는 웹 브라우저의 요청을 받은 웹 서버는 요청을 받아들여 웹 페이지를 전송한다.
     > 사용자 → 요청 → 서버 → 응답 → 사용자
 - 요청 메시지 : 클라이언트가 서버로 보내는 편지
 - 응답 메시지 : 서버가 클라이언트로 보내는 편지

##### express 모듈을 사용한 서버 생성과 실행
 - express모듈의 기본 메소드
     > express() : 서버 애플리케이션 객체를 생성한다<br>
     app.use() : 요청이 왔을 때 실행할 함수를 지정한다<br>
     app.listen() : 서버를 실행한다
 - 예제)
     > // 모듈을 추출한다. <br>
     const express = require('express')<br>
     // 서버를 생성한다. <br>
     const app = express(); <br>
     // request 이벤트 리스너를 설정한다. <br>
     app.user((request, response)=> {response.send('hello express'));}) <br>
     // 서버를 실행한다. <br>
     app.listen(52273, () => {console.log('Server running at http:// 127.0.0.1:52273');});
 - 결과
     > Server running at http:// 127.0.0.1:52273
 - 웹 페이지 결과
     > hello express

##### 페이지 라우팅
 - 클라이언트 요청에 적절한 페이지를 제공하는 기술
 - express 모듈의 페이지 라우팅 메소드
     > get(path,callback) : GET 요청이 발생했을 때 이벤트 리스너를 지정 <br>
     post(path,callback) : POST 요청이 발생했을 때 이벤트 리스너를 지정 <br>
     put(path,callback) : PUT 요청이 발생했을 때 이벤트 리스너를 지정 <br>
     delete(path,callback) : DELETE 요청이 발생했을 때 이벤트 리스너를 지정 <br>
     all(path,callback) : 모든 요청이 발생했을 때 이벤트 리스너를 지정
 - 예제
     > // 모듈을 추출한다. <br>
     const express = require('express'); <br>
     // 서버를 생성한다. <br>
     const app = express(); <br>
     // request 이벤트 리스너를 설정한다. <br>
     app.get('/page/:id',(request,response) => { <br>
     &nbsp; // 토큰을 꺼낸다. <br>
     &nbsp; const id = request.params.id; <br>
     &nbsp; // 응답한다. <br>
     &nbsp; response.send(`${id}Page');}); <br>
     // 서버를 실행한다. <br>
     app.listen(52273, () => {console.log('Server running at http:// 127.0.0.1:52273');});
 - 웹 페이지 결과
     > 273 Page

##### 요청과 응답
 - express 모듈에서 사용하는 모든 콜백 함수의 매개 변수에는 request 객체와 response 객체가 들어간다.
 - response 객체의 기본 메소드
     > send() : 데이터 본문을 제공한다 <br>
     status() : 상태 코드를 제공한다 <br>
     set() : 헤더를 설정한다
 - 예제
     > // 모듈을 추출한다. <br>
     const express = require('express'); <br>
     // 서버를 생성한다. <br>
     const app = express(); <br>
     // request 이벤트 리스너를 설정한다. <br>
     app.get('*',(request,response) => { <br>
     &nbsp; response.status(404); <br>
     &nbsp; response.set('methodA','ABCDE'); <br>
     &nbsp; response.set({ <br>
     &nbsp; &nbsp; 'methodB1':'FGHIJ', <br>
     &nbsp; &nbsp; 'methodB2':'KLMNO' <br>
     &nbsp; }); <br>
     &nbsp; response.send('본문을 입력합니다.'); <br>
     }) <br>
     // 서버를 실행한다. <br>
     app.listen(52273, () => {console.log('Server running at http:// 127.0.0.1:52273');});
 - 웹 페이지 결과
     > 본문을 입력합니다.
 - <B>Content-Type</B>
    - MIME 형식
        > text/plain 기본적인 텍스트를 의미 <br>
     text/html html 데이터를 의미 <br>
     image/png png 데이터를 의미 <br>
     audio/mpe MP3 음악 파일을 의미 <br>
     video/mpeg MPEG 비디오 파일을 의미 <br>
     application/json json 데이터를 의미 <br>
     multipart/form-data 입력 양식 데이터를 의미
    - Content-Type 지정 메소드
        > Content-Type을 MIME 형식으로 지정
    - 예제 [ 교제 275-276페이지 참고 
 - <B>HTTP 상태 코드</B>
    - HTTP 상태 코드의 예
        > 1xx &nbsp; 처리중 &nbsp; 100 Continue <br>
     2xx &nbsp; 성공 &nbsp; 200 OK <br>
     3xx &nbsp; 리다이렉트 &nbsp; 300 MUltiple Choices <br>
     4xx &nbsp; 클라이언트 오류 &nbsp; 400 Bad Request <br>
     5xx &nbsp; 서버 오류 &nbsp; 500 Internal Server Error
    - status()메소드
        > status() 상태 코드를 지정한다.
    - 예제 [ 교제 278 페이지 참고 ]
 - <B>리다이렉트</B>
    - 웹 브라우저가 리다이렉트를 확인하면 화면을 출ㄹ력하지 않고, 응답 헤더에 있는 Location 속성을 확인해서 해당 위치로 이동
    - redirect() 메소드
        > redirect() 리다이렉트합니다.
    - 예제
        > // 모듈을 추출한다. <br>
     const express = require('express'); <br>
     // 서버를 생성한다. <br>
     const app = express(); <br>
     // request 이벤트 리스너를 설정한다. <br>
     app.get('*',(request,respone) => { <br>
     &nbsp; response.redirect('http:// hanbit.co.k r'); <br>
     }); <br>
     // 서버를 실행한다. <br>
     app.listen(52273,() => {console.log('Server running at http:// 127.0.0.1:52273');)};

##### request 객체
 - 요청 매개 변수
 - 주소 분석
     > 프로토콜 &nbsp;&nbsp; 통신에 사용되는 규칙을 의미한다. <br>
     호스트 &nbsp;&nbsp; 애플리케이션 서버의 위치를 의미 <br>
     URL &nbsp;&nbsp; 애플리케이션 서버 내부에서 라우트 위치를 나타낸다 <br>
     요청 매개 변수 &nbsp;&nbsp; 추가적인 정보를 의미
 - 예제
     > // 모듈을 추출한다. <br>
     const express = require('express'); <br>
     // 서버를 생성한다. <br>
     const app = express(); <br>
     // request 이벤트를 리스너를 설정 <br>
     app.get('*',(request,response) =>{ <br>
     &nbsp; console.log(request.query); <br>
     &nbsp; response.send(request.query); <br>
     }); <br>
     //서버를 실행한다. <br>
     app.listen(52273, () => {console.log('Server runinng at http:// 127.0.0.1:52273);});
 - 결과
     > Server runinng at http:// 127.0.0.1:52273 <br>
     { a: '10, b: '20'}

##### 미들웨어
 - 쉽게 활용할 수 있도록 여러 가지 기능을 제공한다.
 - 미들웨어 설정 메소드
     > use() 미들웨어를 설정한다.
 - <B>정적 파일 제공</B>
    - 웹 페이지에서 변경되지 않는 요소를 쉽게 제공해주는 기능
    - 변경되지 않는 요소 (이미지,음악,자바스크립트 파일, 스타일시트 파일 등)
    - 예제 [ 교제 283 페이지 참고 ]
 - <B>morgan 미들웨어</B>
    - moragn 미들웨어 설치
        > npm install morgan
    - 예제 [ 교제 284-285 페이지 참고 ]
    - 웹 서버에서 굊아히 기본적이면서도 중요한 미들웨어
 - <B>body-parser 미들웨어</B>
    - 클라이언트에서 서버로 데이터 전송
    - URL을 사용한 요청
    - 클라이언트가 서버로 본문을 전달할 때 요청 본문의 종류를 함께 전달
    - 요청 본문의 종류
        > application/x-www-form-urlencoded : 웹브라우저에서 입력 양식을 POST,PUT,DELETE 방식 등으로 전달 할 때 사용하느 기본적이 요청 형식 <br>
        application/json JSON : 데이터로 요청하는 방식 <br>
        multipart/form-data : 대용량 파일을 전송할 때 사용하는 요청 방식 <br>
    - body-parser 미들웨어 설치
        > npm install body-parser
    - 예제 [ 교제 287 페이지 참고 ]
 - 속성 정리
    > params 객체 : URL의 토큰을 나타낸다. <br>
    query 객체 : URL의 요청 매개 변수를 나타낸다. 토큰보다 많은 데이터를 전달할 수 있으며, 주소로 어떤 데이터가 오고 가는지 확인할 수 있다. <br>
    body 객체 : 대용량 문자열 등을 전송할 때 사용한다. 다만 주소에 데이터를 기록하지 못하므로 새로고치이나 즐겨찾기 기능 등을 활용할 수 없다.

##### RESTful 웹 서비스 개요
 - REST규정에 맞게 만든 ROA를 따르는 웹 서비스 디자인 표준
 - 자원을 다루는 방법과 특정 웹 페이지로 접근하는 방법을 비슷한 형태로 구성한다는 의미
 - RESTful 웹 서비스의 구조
     > GET &nbsp;&nbsp; 컬렉션을 조회한다 &nbsp;&nbsp; 컬렉션의 특정 요소를 조회한다 <br>
     POST &nbsp;&nbsp; 컬렉션에 새로운 데이터를 추가한다 &nbsp;&nbsp; 요소를 사용하지 않는다 <br>
     PUT &nbsp;&nbsp; 컬렉션 전체를 한꺼번에 변경한다 &nbsp;&nbsp; 컬렉션에 특정 요소를 수정한다 <br>
     DELETE &nbsp;&nbsp; 컬렉션 전체를 삭제한다 &nbsp;&nbsp; 컬렉션의 특정 요소를 삭제한다.
 - ex)
     > GET/user : 사용자 전체를 조회한다 <br>
     GET/user/273 : 273번 사용자를 조회한다 <br>
     POST/user : 사용자를 추가한다 <br>
     DELETE/user/273 : 273번 사용자를 삭제한다
 - RESTful 웹 서비스
     > GET &nbsp;&nbsp; /user &nbsp;&nbsp; 모든 사용자 정보를 조회 <br>
     POST &nbsp;&nbsp; /user &nbsp;&nbsp; 사용자를 추가 <br>
     GET &nbsp;&nbsp; /user/:id &nbsp;&nbsp; 특정 사용자 정보를 조회 <br>
     PUT &nbsp;&nbsp; /user/:id &nbsp;&nbsp; 특정 사용자 정보를 수정 <br>
     DELETE &nbsp;&nbsp; /user/:id &nbsp;&nbsp; 특정 사용자 정보를 제거

##### 코드 구성
 - RESTful 웹 서비스 코드 [ 교제 295-298 페이지 참고 ]

##### Postman 크롬 애플리케이션
 - Postman 설치
     > https://www.getpostman.com/
 - RESTful 웹 서비스를 테스트할 수 있도록하는 애플리케이션

## [05월 18일]
> 오늘 배운 내용 요약
##### 전역변수
 - 아무런 변수를 선언하지 않고 모든 곳에서 사용할 수 있는 변수
 - 문자열 자료형의 전역 변수
     > __filename 현재 실행 중인 코드의 파일 경로를 나타낸다<br>
     __dirname 현재 실행 중인 코드의 폴더 경로를 나타낸다
 - ex)
     > console.log(__filename);<br>
     console.log(__dirname);
 - 결과
     > node globalVarialbe.js<br>
     globalVariable.js

##### process 객체의 속성과 이벤트
 - process 객체는 프로세스 정보를 제공하며, 제어할 수 있게 하는 객체
 - process 객체의 속성
     > env 컴퓨터 환경 정보를 나타낸다<br>
     version Node.js버전을 나타낸다<br>
     versions Node.js의 종속된 프로그램 버전을 나타낸다<br>
     arch 프로세서의 아키텍처를 나타낸다<br>
     platform 플랫폼을 나타낸다
 - process 객체의 메소드
     > exit([exitCode=0]) 프로그램을 종료<br>
     memoryUsage() 메모리 사용 정보 객체를 리턴<br>
     uptimem() 현재 프로그램이 실행된 시간을 리턴

##### process 객체오 이번트 개용
 - Node.js의 이벤트 연결 메소드
     > on(<이벤트 이름>,<이벤트 핸들러>) 이벤트를 연결
 - 이벤트 핸들러는 이벤트가 발생했을 때 호출할 함수를 의미
 - process 객체의 이벤트
     > exit 프로세스가 종료될 때 발생<br>
     uncaughtException 예외가 일어날 때 발생
 - [교재 233 페이지 참고]

##### os모듈
 - os모듈은 애플리케이션을 마들 때 많이 활용하지 않는다
 - 모듈의 기본 사용 방법을 익히기에 가장 적당
 - os객체 생성
     > const os = require('os');
 - os모듈의 메소드
     > hostname() 운영체제의 호스트이름을 리턴<br>
     type() 운영체제의 이름을 리턴<br>
     platform() 운영체제의 플랫폼을 리턴<br>
     arch() 운영체제의 아키텍처를 리턴<br>
     release() 운영체제의 버전을 리턴<br>
     uptime() 운영체제가 실행된 시간을 리턴<br>
     loadavg() 로드 에버러지 정보를 담은 배열을 리턴<br>
     totalmem() 시스템의 총메모리를 리턴<br>
     freemem() 시스템의 사용 가능한 메모리를 리턴<br>
     cpus() CPU의 정보를 담은 객체를 리턴<br>
     getNetworkInterfaces() 네트워크 인터페이스의 정보를 담은 배열을리턴

##### url모듈
 - url객체 생성
     > const url = require('url');
 - url모듈의 메소드
     > parse(urlStr[, parseQueryString=false,slashesDenoteHost=false]) url문자열을 url객체로 변환해 리턴<br>
     format(urlObj) url객체를 url문자열로 변환해 리턴<br>
     resolve(from,to) 매개 변수를 조합하여 완전한 url 문자열을 생성해 리턴

##### File System모듈(자주사용)
 - 파일 처리와 관련된 모듈
 - fs객체 생성
     > const fs = require('fs');
 - 파일 읽기 메소드
     > fs.readFileSync(<파일 이름>); 동기적으로 파일을 읽어 들인다<br>
     fs.readFile(<파일 이름>,<콜백 함수>); 비동기적으로 파일을 읽어 들인다
 - 동기식 비동기식 실행 예제 [ 교재 240-241 페이지 참고]
 - 동기식 코드 예제
     > const fs = require('fs'); ① <br>
     const file = fs.readFileSync('testfile.txt'); ② <br>
     cosole.log(file); ③ <br>
     console.log(file.toString); ④ <br>
     // 현재 단계의 코드를 종료 ⑤
 - 동기적으로 파일을 읽어 들일 때 중요한 부분은 ②에서③으로 이동하는 과정이다
 - ②에서 파일을 읽어 들일 때까지 코드가 정지
 - 파일크기가 클 경우 ②에서③으로 이동할 때 10초 이상 정지할 가능성이 있다
 - 10초이상 정지할 경우 사용자가 프로그램이 죽었나 하고 생각하여  프로그램을 강제 종료할 가능성이 있다.
 - 비동기식 코드 예제
     > const fs = require('fs'); ① <br>
     fs.readFile('textfile.txt',(error,file) => { ② <br>
        console.log(file); ④ <br>
        console.log(file.toString()); ⑤ <br>
        //현재 단계의 코드를 종료합니다. ⑥ <br>
     });<br>
     //현재 단계의 코드를 종료합니다. ③ <br>
 - fs.readFile() 메소드는 파일을 읽어 들이는 이벤트를 등록하는 메소드
 - ②에서③으로 이동하는 동안 걸리는 시간이 0초에 가깝다
 - 프로그램이 계속 실행되며 뒷단에서 파일을 읽어 들이는 처리가 수행

##### 비동기 처리의 장점
 - 프로그램을 개발하는 과정에서 Node.js를 사용하면 손쉽게 비동기 처리 구현
 - 순차적으로 읽어 들이는 것이 아니라 병렬적으로 파일을 읽어 들이므로, 파일 하나를 읽어 들이는데 2초씩 걸린다 해도 전체 처리가  2초 밖에 되지 않는다

##### 파일쓰기
 - 파일 쓰기 메소드
     > fs.writeFileSync(<파일 이름>,<문자열>) 동기적으로 파일을 쓴다 <br>
     fs.writeFile(<파일 이름>,<문자열>,<콜백함수>) 비동기적으로 파일을 쓴다
 - 예제 [ 교재 245 페이지 참고 ]

##### 파일 처리와 예외 처리
 - 동기 코드를 예외 처리할 때 try catch 구문을 활용
 - 비동기 코드를 예외 처리할 때는 콜백 함수로 전달된 첫 번째 매개 변수 error를 활용
 - Node.js에서는 동기 처리를 사용할 이유가 없다
 - 동기 코드 예외 처리, 비동기 코드 예외 처리 예제 [ 교재 246-248페이지 참고 ]

##### 노드 패키지 매니저
 - 어떤 프로그래밍 플랫폼이 기본적으로 제공하는 모듈을'내부 모듈'이라고 한다
 - 개인 개발자가 내부 모듈을 조합해서 사용하기 쉬운 형태로 만들거나 새로운 기능을 구현해서 제공하는 것을'외부 모듈'이라고 한다
 - npm(Node.js Package Manager)
 - npm 외부 모듈 설치 명령어
     > npm install<모듈 이름> <br>
     예> npm install express
 - 명령어 뒤에 @기호를 사용하면 원하는 버전을 설치할 수 있다
     > npm install <모듈 이름>@<버전> <br>
     예> npm install express@4.2

##### request모듈
 - 웹 요청을 쉽게 만들어 주는 모듈
 - Node.js가 기본적으로 제공하는 모듈이 아니라 다른 개인이 제공하는'외부 모듈'이다
 - npm으로 설치해야 사용 가능
     > npm install request
 - request 모듈 추출
     > const request = require('request');
 - request모듈 설명 [ GitHub페이지에서 확인 가능 ]
 - request 예제
     > const request = require('request'); <br>
     request('https://naver.com',(error,response,body) => { <br>
         console.log(body); <br>
     })
 - 결과
     > a href="https://blog.naver.com/bizzy78/222251306146" class="theme_info" data-clk="tcc_des.list5.....<br> 등 사이트 body부문 출력

##### cheerio모듈
 - 웹 페이지의 측정 위치에서 손쉽게 데이터를 추출할 수 있다
 - cheerio 모듈 설치
     > npm install cheerio
 - cheerio 모듈 추출
     > const cheerio = require('cheerio');
 - cheerio모듈은 jQuery를 어느 정도 알아야 제대로 활용 가능
 - 예제 [ 교과서 255 페이지 참고 ]

##### async 모듈
 - 비동기적으로 구성되므로 실행 순서를 정의하기가 어렵고, 들여쓰기도 많다. 이 문제를 어느 정도 해결해 줄 수 있는 모듈
 - async 모듈 설치
     > npm install async
 - async 모듈 추출
     > const async = require('async');
 - async 모듈 설명 [ GitHub페이지에서 확인 가능 ]
 - 비동기 처리를 많이 하면 '콜백 지옥'이 발생
 - '콜백 지옥'은 콜백 함수를 여러 개 들여쓰기 하여 코드를 보기 힘든 상태를 의미
 - async 예제 [ 교제 257 페이지 참고 ]

## [05월 11일]
> 오늘 배운 내용 요약
##### Date 객체
 - Date 객체 생성 방법
     > new Date() 현재 시간으로 Date 객체를 생성<br>
     new Date(<유닉스 타임>) 유닉스 타임으로 Date 객체를 생성<br>
     new Date(<시간 문자열>) 문자열로 Date 객체를 생성<br>
     new Date(<년>,<월-1>,<일>,<시간>,<분>,<초>,<밀리초>) 시간 요소를 기반으로 Date 객체를 생성

##### Date 메소드 활용
 - Date 객체는 get ㅇㅇ() 형태와 set ㅇㅇ() 형태의 메소드만 가진다
 - ㅇㅇ에 들어갈 수 있는 문자는 FullYear,Month,Day,Hours,Seconds 등 이다.
 - ex) 시간 더하기
     > let date = new Date();<br>
     console.log(date);<br>
     date.setFullYear(date.getFullYear()+1);<br>
     date.setMonth(date.getMonth()+11);<br>
     date.setDate(date.getDate()+3);<br>
     console.log(date);
 - 출력 (2016년 8월 16일 기준)
     > 2016-08-15T21:57:04.200Z<br>
     2018-07-18T21:57:04.200Z
 - [ 교재 193 - 194 페이지 참고 ]

##### Array 객체
 - Array 객체는 자바스크립트에서 여러 자료를 다룰 때 사용하는 자료형
 - Array 객체의 메소드
     > concat() 매개 변수로 입력한 배열의 요소를 모두 합쳐 배열을 만들어 리턴<br>
     join() 배열 안의 모든 요소를 문자열로 만들어 리턴<br>
     pop()* 배열의 마지막 요소를 제거하고 리턴<br>
     push()* 배열의 마지막 부분에 새로운 요소를 추가<br>
     reverse()* 배열의 요소 순서를 뒤집는다<br>
     slice() 배열 요소의 지정한 부분을 리턴<br>
     sort()* 배열의 요소를 정렬<br>
     splice()* 배열 요소의 지정한 부분을 삭제하고 삭제한 요소를 리턴
 - [ 교재 195 - 198 페이지 참고 ]

##### ECMAScript5에서 추가된 메소드
 - ECMAScript에서 추가된 Array 객체의 메소드 (사용 빈도가 높은 메소드 3개)
     > forEach() 배열의 요소를 하나씩 뽑아 반복<br>
     map() 콜백 함수에서 리턴하는 것을 기반으로 새로운 배열을 만듬<br>
     filter() 콜백함수의 true를 리턴하는 것만으로만 새로운 배열을 만들어 리턴
 - 콜백 함수 형태 ex)
     >let foo = [1, 30, 40, 50, 100];<br> 
     foo.forEach((item,index) => { 출력 });<br>
     let bar=foo.map((item,index) => { 리턴 });<br>
     let foobar = foo.filter((item, index) => { 조건 });

##### 프로토타입에 메소드 추가
 - 메소드를 추가하면 해당 자료형 전체에 추가할 수 있다.
 - ex)
     > String.prototype.contain = function(input){<br>
         return this.indexOf(input) >= -1; <br>
     };<br>
     console.log('안녕하세요'.contain('안녕'));<br>
     console.log('안녕하세요'.contain('데굴데굴'));
 - 익명 함수와 호살표 함수의 차이 때문에 화살표 함수는 사용할 수 없다.

##### underscore.js 라이브러리
 - 자바스크립트에서 굉장히 많은 기본 함수를 제공함에도 실제로 사용하다 보면 부족
 - 개발자가 자주 사용하는 기능을 underscore.js 라이브러리에 정리
 - 자세한 내용은 공식 웹 사이트를 살펴보면 쉽게 이해 가능
 - [ 교재 201 - 202 페이지 참고 ]

##### JSON 객체
 - ECMAScript5에서 추가된 객체 
 - JSON은 JavaScript Object Notation의 약어
 - 자바스크립트 객체를 사용한 데이터 표현 방법
 - 2010년 이후 전 세계 웹에서 가장 많이 사용하는 데이터 표현 방법
 - 제약 사항
     > 문자열은 큰따옴표로 만들어야 한다.<br>
     모든 키는 따옴표로 감싸야 한다.<br>
     숫자,문자열,불 자료형만 사용할 수 있다.
 - JSON 객체의 메소드
     > JSON.string(<객체>,<변환함수>,<공백개수>) 자바스크립트 객체를 문자로 만듬<br>
     JSON.parse(<문자열>) 문자열을 자바스크립트 객체로 파싱
 - [ 교제 204 페이지 예제참고 ]

##### 예외와 기본 예외 처리
 - 오류 : 프로그램을 실행하기도 전에 발생하는 문법적 오류 [ 교재 212 페이지 NOTE 참고 ]
 - 예외 : 실행에 문제가 발생하면 자동 중단됨. 이렇게 발생한 오류
 - 예외 처리 : 오류에 대처할 수 있게 하는 것
 - 예외 상황 확인 [ 교제 213 페이지 예제참고 ]

##### 고급 예외 처리
 - try, catch, finally 키워드로 예외를 처리
 - 기본 형태
     > try { <br>
         예외 발생하면 <br>
     } catch(exception) {<br>
         여기서 처리<br>
     } finally {<br>
         무조건 처리<Br>
     }
 - try, catch, finally 구문 ex)
     > try { <br>
         const array = new Array(-2000); <br>
     } catch(exception) {<br>
         console.log('${exception.name} 예외가 발생했습니다.')<br>
     } finally {<br>
         console.log('finally 구문이 실행되었습니다.')<Br>
     } 
 - 출력
     > RangeError 예외가 발생했습니다.<br>
     finally 구문이 실행되었습니다.
 - [ 교재 216 - 218 페이지 참고 ]

##### 예외 객체
 - 예외가 발생하면 어떤 예외가 발생했는지 정보를 함께 전달받는 기능을 수행
 - 형태
     > try {<br>
     } catch(exception) {<br>
     }
 - exception을 입력할 필요없이 e를 써서 사용가능

##### 강제 예외
 - 예외를 강제로 발생시킬 때 throw키워드를 사용
 - throw 키워드 뒤에 문자열 또는 Error 객체를 입력
     > throw '강제 예외';
 - 더 자세하게 예외를 출력하고 싶을 때 Error객체를 사용
 - Error 객체를 사용하면 어떤 파일의 몇 번째 줄에서 예외가 발생했는지 확인 가능
 - 예외 처리 예제 [ 교제 220 - 221 페이지 참고 ]

## [05월 04일]
> 오늘 배운 내용 요약
##### 생성자 함수
 - 생성자 함수는 일반적인 함수와 구분할 수 있게 대문자로 시작하는 이름을 사용한다.
 - 생성자 함수 ex)
   > function Product(name,price) {<br>
this.name=name;<br>
this.price=price;<br>
}
 - 객체 생성 ex)
   > let product = new Product("바나나",1200);

##### 프로토타입
 - 생성자 함수로 만든 객체는 프로토타입이라는 공간에 메소드를 지정해서 모든 객체가 공유하도록 만들 수 있다.
 - [ 교재 171페이지 참고 ]

##### null
 - 값 = null , 자료형 = object
 - 변수 선언하고 값을 넣지않으면 undefined가 된다.
 - 값이 없는 상태를 구분할 때 사용한다.
 - [ 교재 173페이지 참고]

##### 기본 자료형과 객체 자료형의 차이
 - 숫자,문자열,불을 기본 자료형이라고 한다.
 - typeof를 사용면object 문자가 출력된다.
 - 기본 자료형과 객체의 차이점을 찾기 어렵다.
 - 굳이 찾으면 기본 자료형은 객체가 아니므로 속성과 메소드를 추가할 수 없다는 차이점이 있다.
 - [ 교재 182 - 183 페이지 참고 ]

##### Number객체
 - Number객체 생성 ex)
   > let numberFromLiteral = 273;<br>
   let numberFromConstrctor = new Number(273);

##### Number메소드
 - Number 객체의 메소드
   > toExponential() 숫자를 자수 표시로 나타낸 문자열을 리턴합니다.<br>
   toFixed() 숫자를 고정소수점 표시로 나타낸 문자열을 리턴합니다.<br>
   toPrecision() 숫자를 길이에 따라 자수 표시 또는 고정소수점 표시로 나타낸 문자열을 리턴합니다.

##### 생성자 함수의 속성
 - 객체의 일종이므로 속성과 메소드를 추가할 수 있다.
 - Number 생성자 함수의 속성
   > MAX_VALUE 자바스크립트의 숫자가 나타낼 수 있는 최대 숫자<br>
   MIN_VALUE 자바스크립트의 숫자가 나타낼 수 있는 최소 숫자<br>
   NaN 자바스크립트의 숫자로 나타낼 수 없는 숫자<br>
   POSITIVE_INFINITY 양의 무한대 숫자<br>
   NEGATIVE_INFINITY 음의 무한대 숫자

##### String 객체
 - 자바스크립트에서 가장 많이 사용하는 내장 객체
 - String 객체 생성 ex)
   >let stingFromLiteral='안녕하세요';<br>
   let stringFromConstructor=new String('안녕하세요');

##### String 속성과 메소드
 - String 객체 속성
   >length 문자열의 길이를 나타냅니다.
 - String 객체의 메소드
   >charAt(position) position에 위치한 문자를 리턴합니다.<br>
   charCodeAt(position) position에 위치한 문자의 유니코드 번호를 리턴합니다.<br>
   concat(args) 매개 변수로 입력한 문자열을 이어 리턴합니다.
   ...

##### String 메소드 활용
 - 문자열 포함, 문자열 분해 등에 사용
 - indexOf()메소드
   > let string = '안녕하세요.';<br>
   if (string.indexof('아침')>=0){console.log('좋은 아침이에요.')}
 - 결과
   > 좋은 아침이에요.
 - split()메소드
   > let string = '감자,고구마,바나나,사과';<br>
   let array = string.split(',');<br>
   console.log(array);
 - 결과
   > [ '감자','고구마','바나나','사과' ]

 - [ 교재 190 - 191 페이지 참고 ]

## [04월 27일]
> 오늘 배운 내용 요약
##### 타이머함수
setTimeout(function() {
    clearInterval(foo); <br>
},3000); <br>

setTimeout(함수,시간) 특정 시간 후에 함수를 실행 <br>
setInterval(함수,시간) 특정 시간마다 함수를 실행
- ex)
  > let foo = setInterval( () => {
    console.log("출력합니다.");
},1000);

- 결과
  > 출력합니다.<br>
  > 출력합니다.

##### 변수 덮어쓰기
 - 동일한 이름으로 변수를 다수 선언했을 때 마지막에 선언한 변수값이 덮어서 출력된다.
 - ex)
   >let 변수; 
  변수=10; 
  변수20; 
  console.log("변수");

 - 결과
   > 20

##### 함수 덮어쓰기
 - 동일한 이름의 함수를 다수 선언했을 때 변수때와 마찬가지로 마지막에 선언한 값을 덮어서 출력된다.
 - ex)
   > let 함수;
    함수 =()=>{console.log("첫 번째 함수");} <br>
    함수 =()=>{console.log("두 번째 함수");} <br>
    함수();

 - 결과
   > 두 번째 함수

##### 익명함수와 화살표 함수의 차이
 - this가 가지는 의미에서 차이가 난다.
 - function을 사용할 경우 전역적으로 this 키워드가 사용되고
 ()=>을 사용할 경우 지역적으로 this 키워드가 사용된다.

##### 객체
 - 여러 개의 자료형을 한 번에 저장하는 자료형이다.
    - 배열에 대한 기본적인 지식이 필요하다.
    [ 교재 160 페이지 참고 ]
 - 객체선언 ex)
   > let product{
    제품명: '건조망고', <br>
    유형: '당정임', <br>
    원산지: '필리핀' <br>
  }; <br>
  console.log(product);

 - 결과
   > '제품명': '건조망고' <br>
    '유형': '당정임' <br>
    '원산지': '필리핀' <br>

 - [ 교재 161 - 162 페이지 참고 ]

##### 객체와 반복문
 - 객체에 for in 반복문으로 반복을 적용할 수 있습니다.
 [ 교재 163 페이지 코드6-5 참고 ]
 
##### 속성과 메서드
 - 배열 내부에 있는 값 하나하나를 요소라 한다.
 - 객체 내부에 있는 값 하나하나 속성이라 한다.
 - 객체의 속성 중 자료형이 함수인 속성을 메소드라 한다.
 - 자신이 가지고 있는 속성임을 표시할 때는 this 키워드를 사용한다.
 [ 교재 164 - 165 페이지 코드들 참고 ]

##### JSON
 - 자바스크립트를 사용하면 이처럼 데이터를 문자로 쉽게 표현할 수 있기 때문에 많은 프로그래밍 언어에서 데이터를 통신할 때 활용한다.
 - JSON( JavasScript Object Notation )

## [04월 13일]
> 오늘 배운 내용 요약
##### 익명 함수 ( 이름이 없는 함수 )
> let <변수 이름> = function () { }
 
- 리터럴 - 변수 안에 들어 있는 상태가 아니라, 문자 그대로 자료를 나타내는 것
  [ 교재 136페이지 참고 ]
##### 선언적 함수
> function <함수 이름>() { }

- [ 교재 137페이지 참고 ]

##### 화살표 함수
> let 함수 = () => { }

함수의 매개 변수로 전달하는 콜백 함수 등을 만들 때 활용

##### 함수의 기본 형태
형태 ( 입력 -> 함수 -> 출력 )

 - power 예시
>function power(x) {return x*x} 
console.log(power(10));

- multiply 예시
>function multiply(x,y) {return x*y;}
console.log(multiply(52,273));

 - print 예시
>function print(x) {console.log(x+"(이)라고 말했습니다.");}
print("안녕하세요");

##### 함수의 기본 활용 형태
- [ 교재 142 - 146페이지 참고 ]

##### 콜백 함수
 - 함수의 매개 변수로 전달되는 함수를 '콜백 함수'라고 한다.
 [ 교재 147페이지 참고 ]

##### 표준 내장 함수
 - 자바스크립트에서 기본적으로 지원하는 몇가지 함수
    - >parseInt() 문자열을 정수로 변환합니다.
    parseFloat() 문자열을 실수로 변환합니다.
    setTimeout(함수,시간) 특정 시간 후에 함수를 실행합니다.
    setInterval(함수,시간) 특정 시간마다 함수를 실행합니다.
    clearInterval(아이디) 특정 시간마다 실행하던 함수 호출을 정지합니다.
 - [ 교재 148 - 151페이지 참고 ]


## [04월 06일]
> 오늘 배운 내용 요약
##### 역 for 반복문
 - 배열 반복문을 뒤에서부터 실행해야 할 때 사용
 [ 교재 120 페이지 참고 ]

##### for in 반복문과 for of 반복문
 - for in 반복문과 for of 반복문은 객체에 쉽게 반복문을 적용할 때 사용
> for ( let 인뎃스 in 배열 ) { } for( let 요소 of 배열) { }
 [ 교재 121 페이지 참고 ]

##### 중첩 반복문
 - 중첩 조건문처럼 반복문을 여러 번 중첩해서 사용
 - for (...) { for(...) { } }
 [ 교재 122-123 페이지 참고 ]

##### break키워드
 - 조건문이나 반복문을 벗어날 때 사용
 - 무한 반복문에서 벗어날 때 사용
while(true) { break; }

##### continue키워드
 - 반복문 내부에서 현재 반복을 멈추고 다음 반복을 진행
 - 예제) 홀수만 출력
>for( let i=1;i<10;i++ )
  { 
  if( i%2==0) { continue; } 
  console.log(i) 
  }

##### 스코프
 - 변수를 사용할 수 있는 범위
 - if( <표현식> ) { ------ }, for( <표현식> ) { ----- }

##### var키워드 : 익스플로러
##### let키워드 : 자바스크립트

## [03월 30일]
> 오늘 배운 내용 요약
##### if else if 조건문
 - 중복되지 않는 세 가지 이상의 조건을 구분할 때 사용
  [ 교재 94 페이지 참고 ]

##### switch 조건문
 - 비교할 값이 명확할 때 사용
 - 'switch', 'case', 'break' 키워드 사용
 - 'break' 키워드는 switch 조건문, 반복문을 빠져나갈 때 사용
  [ 교재 97 - 100 페이지 참고 ]

##### 삼항 연산자
> 불 표현식 ? 참 : 거짓
 - 한 줄로 조건문을 표시할 수 있을 때만 사용
[ 교재 102 페이지 참고]

##### 짧은 초기화 조건문
- '||'연산자를 활용
- A || B 에서 A가 참이라면 A로 대치
- A || B 에서 A가 거짓이라면 B로 대치
 [ 교재 103 페이지 코드 3-16 참고]

##### prompt
 [ 교재 104-105 페이지 참고 ]

##### 반복문
 - 여러번 반복하는 일을 간편하게 처리하는 데 사용
    - ex) for (let i =0; i< 1000; i++>) {
            console.log("출력");
          }

##### 배열
 - 여러 개의 자료를 한꺼번에 다룰 수 있는 자료형
 - 크기 설정이 필요없음
 - let 이름 = [ 자료, 자료, 자료, 자료 ]
    - ex)
        let array = [ 52, 273, '아침밥', '점심밥', 'true', 'false' ]
         console.log(array[0]);
         -> 52

##### while 반복문
 - 불 표현식이 참인 동안에는 중괄호 안의 문장을 계속 실행
 - 반복횟수가 불명확할 때 사용
 - while ( 불 표현식 ) {
     불 표현식 참인 동안 실행할 문장
     }
      [ 교재 116 페이지 참고 ]

##### for 반복문
 - 원하는 횟수만큼 반복하고 싶을 때 사용
 - 반복횟수가 명확할 때 사용
 - for( let i =0; i < 반복 횟수; i++) {
     횟수만큼 반복
     }
     [ 교재 118 페이지 참고 ]

## [03월 23일]
> 오늘 배운 내용 요약
 ##### 문자 선택 연산자
 - 문자열[숫자] -문자 선택 연산자
  [ 교재 60 페이지 코드2-10 참고 ]

##### 템플릿 문자열
 - 템플릿 문자열은 ' 기호로 생성한다.
    - 일반 문자열과 똑같은 취급한다.

    ex) '5 + 6 = ${5+6}'  -> 5 + 6 = 11 

##### 불
- 참과 거짓의 표현 ( true 와 false )

 >  * 비교연산자
' == '  같습니다
' != '  다릅니다
' > ' 왼쫀 피연산자가 크다
' < ' 오른쪽 피연사자가 크다
' >= ' 왼쪽 피연산자가 크거나 같다
' <= ' 오른쪽 피연산자가 크거나 같다
> * 논리 연산자
 ' ! ' 논리 부정 연산자
 ' || ' 논리합 연산자 ' or ' (이항 연산자)
 ' && ' 논리곱 연산자 ' and ' (이항 연산자)

- 논리 연산자의 사용
[ 교재 66 페이지 참고]

##### 변수
 - 변수를 선언 ( let 식별자; )
 - 변수에 값을 할당 ( 식별자 = 1123; )
 - 변수 기본 사용 방법
    - [ 교재 68 페이지 참고 ]

##### 복합 대입 연산자
- 변수에 사용할 수 있는 특별한 연산자
> * 복합 대입 연산자
' += ' 숫자 덧셈 후 대입 연산자
' -= ' 숫자 뺄셈 후 대입 연산자
' *= ' 숫자 곱셈 후 대입 연산자
' /= ' 숫자 나눗셈 후 대입 연산자

##### 증감 연산자
- 변수에 사용할 수 있는 증감 연산자
> * 증감 연산자
' 변수++ ' 기존 변수 값에 1을 더한다 (후위)
' ++변수 ' 기존 변수 값에 1을 더한다 (전위)
' 변수-- ' 기존 변수 값에 1을 뺀다 (후위)
' --변수 ' 기존 변수 값에 1을 뺀다 (전위)

ex) 
>let num = 10;
console.log(num++);
console.log(++num);
-------출력-------
10
12

##### 자료형 검사
- 해당 변수의 자료형을 추출한다
> * 자료형 확인 연산자 
' typeof ' 해당 변수의 자료형을 추출한다

ex) typeof 10 -> 'number' , typeof "문자열" -> 'string'

##### undefined 자료형
- 초기화되지 않은 것을 표현하는 자료형
[ 교재 76 페이지 참고 ]
##### 강제 자료형 변환
- 자료형을 특정 자료형으로 강제 변환
> * 강제 자료형 변환 함수
' Number() ' 숫자로 자료형 변환
' String() ' 문자열로 자료형 변환
' Boolean() ' 불로 자료형 변환
- 문자열을 숫자로 변환할 때 NaN이 발생
    - NaN은 무조건적으로 다르다
    - NaN인지 확인할 때는 isNaN()함수를 사용

ex) [ 교재 78-79 페이지 참고 ]

##### 일치 연산자
> * 일치 연산자
' === ' 자료형과 값이 같은지 비교
' !== ' 자료형과 값이 다른지 비교

##### 상수
- 상수를 선언 - const 식별자;
- 변하지 않는 값에 이름을 붙일 때 사용
[ 교재 84 페이지 참고 ]

##### if 조건문
- 불 표현식
- 문장이 true이면 문장을 실행 false이면 문장을 무시
[ 교재 90 페이지 참고 ]

##### if else 조건문
- 상황이 두 가지로 나뉘었을 때 사용
[ 교재 92 페이지 참고 ]

##### 중첩조건문
- 조건문 안에 조건문을 중첩해 사용하느 것
- 중첩에 제한이 없음
[ 교재 94 페이지 참고 ]

## [03월 16일]
> 오늘 배운 내용 요약
 ##### 자바스크립트( JSP )의 발전
 ###### 세계에서 가장 오해를 많이 받는 프로그래밍 언어
 - 부수적인 프로그래밍 언어로 취급을 받았으나 구글 맵을 시작으로 자바스크립트 언어의 위상이 상승한다. 이후 웹 브라우저를 벗어나 다양한 분야에서 개발가능한 프로그래밍 언어로 활용된다. 

 ###### Node.js
 - 자바스크립트의 단점인 속도를 개선
 - 이벤트 기반 비동기 방식으로 작동

 ###### 자바스크립트로 할 수 있는 일
- 웹 클라이언트 애플리케이션 개발 
 웹 서버 개발
 모바일 애플리케이션 개발
 데스크톱 애플리케이셔 개발
 게임 개발
 데이터베이스 관리
 
 ###### 표현식과 문장
- 표현식이 하나 이상 모이면 문장이 된다.
 - 코드문장의 마지막에는 종결한다는 의미로 세미콜론( ; )을 찍는다.

 ###### 키워드
 - [ 교재 59페이지 표 참고]

 ###### 식별자
 - 식별자는 이름을 붙일 때 사용하는 단어
  [식별자 규칙]
 키워드를 사용하면 안 됩니다.
 특수문자는_와$만 허용됩니다.
 숫자로  시작하면 안 됩니다.
 공백은 입력하면 안 됩니다.

 ###### 주석
 - 프로그램의 진행에 전혀 영향을 주지 않는 코드
 - 표현 : // - 한 줄만 주석 , /* ... */ - 여러 줄을 주석

 ###### 출력
 - console.log("문자열"); 사용하여 출력
 [ 교재 52-53 페이지 참고]

 ###### 숫자 연산자
 - 기본적인 사칙 연산자 : + - * /
 나머지 연산자 %

 ###### 문자열
 - 문자열 생성시 큰따옴표("), 작은따옴표(') 사용

