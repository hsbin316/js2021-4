# 허성빈 [201840235]
## [04월 27일]
> 오늘 배운 내용 요약
##### 타이머함수
setTimeout(function() { <br>
    clearInterval(foo); <br>
},3000);
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

