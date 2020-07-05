# JavaScript정리

</br>

## JavaScript란

**정의**

>   JavaScript는 객체 기반의 스크립트 언어로 HTML로는 웹의 내용을 CSS는 웹의 디자인을 JavaScript는 웹의 동작을 구현할 수 있다.

**특징**

-   script형 언어 (function형 언어랑 비슷하다)
-   한 줄 한 줄 읽어서 바로 실행한다
-   interpreter언어이다.
-   JavaScript는 객체 기반의 언어이지만 **상속과 클래스의 개념이 없다**
-   자바스크립트 구문에서는 ;(세미콜론)을 써도 되고 안 써도 된다 , 꼭 써야되는 때가 있다
-   **`on`**으로 시작하는 건 javascript라고 생각하면 된다
-   JavaScript영역에서는 ""(더블쿼터),''(싱글쿼터)둘 다 사용할 수 있다.
-   JavaScript는 **타입추론** 한다(자동으로 타입을 잡아준다)

**compiler언어**

>   중간에 목적 코드가 만들어지는데 목적 코드란 코드를 기계어로 변환 해준 것 

**interpreter언어**

>   한 줄 한 줄 변환해서 사용한다 

</br>

## JavaScript 작성방식 3가지

- CSS와 마찬가지로 **인라인, 내부, 외부** 방식이 있다.

    - **인라인** : 태그 안에 작성해준다

    - **내부** : 보통 head태그 안에 script태그 안에 작성해준다
    - **외부** : 외부 .js파일을 script태그의 src속성으로 불러온다 

```html
     <!DOCTYPE html>
     <html>
     <head>
     <meta charset="UTF-8">
     <title>js01</title>
     <style type="text/css">
          li{
                    cursor: pointer;
               }
     </style>
          <!-- 1. src안에 있는 js파일을 사용한다 해놓고 내부 작성방식을 또 써주면 절~~대 안된다 -->
     <script type="text/javascript" src="resources/js/basic.js"></script>
          
		<!--2. html코드와 함께 사용하는 법-->
     <script type="text/javascript"> // = 생긴건 text고 동작은 javascript라는 의미이다 , 없어도 실행 된다

          function embededTest(){ 
               var doc= document.getElementsByTagName("li")[1];
               doc.style.color="red";
               doc.innerHTML="<strong>글자가 바뀌었습니다!!</strong>";	
     }

     </script>

     </head>
     <body>
          <h1> 자바스크립트 작성방식 3가지</h1>

          <ol>
               			<!--3. inline방식으로 태그 안에 작성한다-->
               <li onclick="alert('inline 방식으로 실행됨! ');">inline 방식</li>
               <li onclick="embededTest();">내부 작성방식</li> 
               <li onclick="test();"> 외부 작성방식 (*.js)</li>
     </body>
     </html>
```

</br>

## 변수 규칙

-   var 키워드는 생략할 수 있다. ( 생략시 전역 변수가 된다??)

```html
<dt> 변수 선언규칙</dt>
	<dd>1. 대소문자 구분</dd>
	<dd>2. 영문,$,_로 시작한다</dd>
	<dd>3. 영문,$,_,숫자를 포함할 수 있다</dd>
	<dd>4. 키워드나 예약어를 사용할 수 없다</dd>

```

</br>

## 전역 변수와 지역 변수

#### 지역 변수
-   지역 변수는 **함수안에서 전역변수 보다 높은 우선순위를 가진다**
-   블럭-수준이 아닌 함수-수준의 범위를 가진다
-   해당 함수내에서만 접근가능한 변수
-   지역 변수 선언시 항상(var)키워드를 붙여준다 , 잘못하면 전역 변수가 될 수 있다

#### 전역 변수

-   브라우저에서, 전역 컨텍스트(또는 scope) 는 window 객체를 가리킨다 
-   (var키워드를 사용하여)변수가 최초 선언 없이 초기화 되면, 해당 변수는 자동으로 전역 변수가 된다, 함수 안에 있어도 마찬가지이다 

```javascript
<script type="text/javascript">
	//전역변수: window 객체에 포함되는 변수, 다른 함수들에서 공용으로 사용할 수 있다(값이 유지됨)
	var variable01=10;

	function test01(){
          variable01= variable01+5;
          document.getElementById("v01").innerHTML="<b style='color:red; background:yellow;'>'"
     	+ variable01 + "</b>";
     }
	function test02(){
          //지역변수 : 함수나 객체 내부에 선언되고 실행이 종료되면 사라짐
          	var variable02=variable01+100;
          	document.getElementById("v02").innerHTML="<b style='color:red; background:yellow;'>"
          	+variable02 + "</b>";
     }
</script>
```



</br>

## 호이스팅 

>   JavaScript에서의 호이스팅은 코드에 선언된 변수 및 함수를 코드 상단으로 끌어올리는 것을 말하며 이는 변수 범위가 전역범위인지 함수 범위인지에 따라 다르게 수행될 수 있다
>
>   -   함수 내에서 선언한 함수 범위(function scope)의 변수는, 해당 함수의 최상위로 끌어올려진다
>
>   -   함수 밖에서 선언한 전역 범위(global scope)의 전역 변수는 스크립트 단위의 최상위로 끌어올려진다
>
>   -   주의할 점은 변수의 선언과 할당 내용 모두를 상단으로 끌어올리는 것이 아니라 선언부분만 분리해서 최상위로 끌어올리고 값을 할당하는 부분은 원래 그 라인에 그대로 있다
>
>   -   함수 선언 내용의 경우 선언한 위치와 관계없이 항상 최상단으로 호이스팅되므로 코드상에서 함수를 선언한 위치보다 먼저 호출하더라도 이상없이 호출된다
>
>   -   단, **함수 호이스팅은 선언 방식이 <u>함수 선언식(function declarations)인 경우</u>에만 적용**된다
>   -   함수명과 변수명이 같을때는 함수 선언이 변수명을 덮어 쓴다, 단 변수에 값이 할당 된 경우는 변수가 함수를 덮어 쓴다
>
>   ### 함수 선언 방식 2 가지
>
>   -   #### 함수 선언식(function declarations)
>
>   -   ```javascript
>       function getNames(){
>       var name=$("input:text").val();
>       }
>       ```
>
>       
>
>   -   #### 함수 표현식(function expressions)
>
>   -   ```javascript
>       var checkAge= function(){
>       if($("#age").val()<20){
>       	alert("20세 이상만 신청 가능합니다.");
>       	}
>       }
>       ```
>
>       
>
>   **호이스팅 예제**
>
>   ```javascript
>   noDefine() //함수 선언하기 전에 호출함
>   function noDefine(){
>   //변수 선언 및 할당 이전에 호출 테스트
>   console.log("not defined:"+ name);
>   var name="ojava";
>   //변수 초기화 이후 값 확인
>   console.log("defined: " + name);
>   }
>   결과
>   not defined: undefined
>   defined : ojava
>   ```
>
>   **var를 생략한 경우**
>
>   ```javascript
>   noDefine() //함수 선언하기 전에 호출함
>   function noDefine(){
>   console.log("not defined:"+ name);
>   name="ojava";	//변수 선언 명령어 없이 name 변수에 할당함 , 전역 변수가 됨
>   console.log("defined: " + name);
>   }
>   결과
>   not defined: ojava
>   defined : ojava
>   ```

</br>

## 변수의 타입

-   **null의 타입이 object이다** (type체크시 주의)
-   함수의 타입은 function이다
-   javascript에서 함수는 값이다
    -   함수내부에서 함수를 만들 수 있다
    -   리턴값이 함수일 수 있다.
    -   파라미터가 함수일 수 있다
    -   1급객체이다 

### **1급시민, 1급객체(1급시민을 만족하는 객체)**

-   프로그래밍의 변수에서 1급 시민의 조건
    1.  변수에 담을 수 있다
    2.  함수(혹은 메소드)의 인자(매개변수,Parameter)로 전달할 수 있다
    3.  함수(혹은 메소드)의 반환값(return)으로 전달할 수 있다.

### 타입의 종류

```html
<dt>타입의 종류</dt>
 		<dd>1.문자(String)</dd>
 		<dd>2.숫자(number)</dd>
 		<dd>3.논리(boolean)</dd>
 	
    		<dd>4.null(object)</dd> <!--null도object로뜨니 주의한다 -->
 		<dd>5.객체(object)</dd>
 		<dd>6.함수(function)</dd>
```









## window  메소드 

-   `window.` 은 생략 가능하다

#### `window.alert()`메소드

-   알림창을 띄워주는 메소드

```javascript
function test(){
	window.alert("알림창 내용")
}
```

#### `window.load()`메소드

-   window가 load되는 이벤트 발생시 실행되는 메소드

```javascript
window.load= function(){		//이름이 없는 익명함수 형태이다
alert("윈도우 로딩 후!");
}
```

#### `window.confirm()`함수

-   '확인' , '취소' 버튼이 있는 알림창

-   확인시 true 취소시 false반환

-   ```javascript
    function confirmTest(){
    //confirm의 '확인','취소'버튼의 이름은 바꿀 수 없다
    	if(confirm("배경을 파랑으로 변환?")){//보여줄 텍스트
    		document.body.style.backgroundColor="blue"; //확인 버튼 누를경우(true)
    		}else{
    		document.body.style.backgroundColor="white";//최소 버튼 누를경우(false)	
    	}
    }
    ```

### `window.prompt()`함수

-   텍스트 박스와 확인/취소 버튼을 제공한다

-   확인 :텍스트값  /  취소 : null 값을 리턴한다

-   ```javascript
    function promptTest(){
    			var txt=prompt("좋아하는 과목을 선택해 주세여 \n [1:자바 , 2:db, 3:web]");
    			
    			switch(txt){
    			case "1":
    				alert("역시 자바!");
    				break;
    			case "2":
    				alert("db 좋죠");
    				break;
    			case "3":
    				alert("홈페이지 만들기 재밌죠");
    				break;
    			case null:		//취소 버튼을 눌렀을 경우 
    				alert("취소하면... 다 싫은건가요?");
    				break;
    			default:		//많이 입력했거나 , 아무것도 입력하지않고 확인을 눌렀을 때
    				alert("1,2,3 번 중에 하나만 선택해 주세여.");
    			}
    		}
    ```

    

</br>

## `location.search;`

-   **자바스크립트의 내장 함수**로 URL의 파라미터(쿼리스트링)부분을 가져온다  ex)?변수=값...

-   getParameterByName함수는 이런 기초함수를 이용하여 파라미터의 이름을 입력하면 해당 값을 가져오는 역활을 한다

-   다양한 location함수 https://kdarkdev.tistory.com/124

    -   window.location.hostname; // => kftc.local 

    -   window.location.href; // => http://kftc.local:8088/test.jsp 

    -   window.location.host; // => kftc.local:8088 

    -   window.location.port; // => 8088 

    -   window.location.pathname; // => test.jsp 

    -   window.location.search; // => ?gg=1 

    -   window.location.protocol; // => http:


</br>

>   