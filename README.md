# JavaScript
1. 자바스크립트의 용도 : 웹브라우저 제어

2. 웹서버에서 사용되는 프로그래밍 언어 : PHP, JAVA, PYTHON


## 수의 연산
 	Math.pow(3,2);		// 9, 3의 2승 
	Math.round(10.6);	// 11, 10.6을 반올림
	Math.ceil(10.2); 	// 11, 10.2를 올림
	Math.floor(10.6); 	// 10, 10.6을 내림
	Math.sqrt(9); 		// 3, 3의 제곱근
	Math.random(); 		// 0부터 1.0 사이의 랜덤한 숫자


## 따옴표 출력
	alert('sso\'s javascript')
 \를 ' 앞에 위치시키면 ' 를 문자열의 시작과 끝을 구분하는 구분자가 아니라 단순히 문자로 해석하도록 강제 할 수 있다. \
 이러한 기법을 이스케이프(escape)라고 한다.	


## 문자+문자(+)
	alert("coding" + " everybody");        //coding everybody
	
	
## 문자열의 길이(.length)
	alert("coding everybody".length)        //16

	  
# 객체지향


## 객체지향 프로그래밍 (Object-Oriented Programming)


## 객체 
객체란 서로 연관된 변수와 함수를 모아둔 그릇
객체 = 변수(property) + 함수(method)

(1)
	var person = {}					// {}객체(object)를 만듬
	person.name = 'sso';    			// 그릇안에 name이란 변수(속성)를 넣고, 변수의 내용 = sso
	person.introduce = function(){ 			// 변수에 담긴 값이 함수라면 method( introduce===method)
	    return 'My name is ' + this.name;       	// function이 담겨있는 객체(person)을 가르킴
	}
	document.write(person.introduce());
	
(2)
	var person = {
	    'name' : 'sso',
	    'introduce' : function(){
		return 'My name is '+ this.name;
	    }
	}
	ducument.write(person.introduce());


## 생성자(Constructor)
객체를 만드는 역할을 하는 함수
함수를 호출할 때 new를 붙이면 새로운 객체를 만든 후 리턴한다.

	var p =new Person()		// person() === 객체의 생성자(함수X)
	
생성자는 객체에 대한 초기화(init)를한다.
->코드의 재사용성이 높아진다.

	function Person(name){			// 생성자 내에서 객체의 property 정의===초기화
	    this.name = name;
	    this.introduce = function() {
		return 'my name is '+this.name;
	    }
	}

	var p1 = new Person('park');
	documentwrite (p1.introduce()+"<br />");

	var p2 = new Person('sso');
	document.write(p2.introduce());
일반함수와 구분하기 위해서 생성자 합수의 첫글자를 대문자로 한다.


## 전역객체(Global object)

모든 객체는 전역객체의 속성이다.

	function func() {
	    alert ('Hello!');
	}
	func();			// 둘다 실행됨
	window.func();		// 모든 전역변수와 함수는 window 객체의 속성이다.

객체를 명시하지 않으면 암시적으로  window의 속성으로 간주한다.
