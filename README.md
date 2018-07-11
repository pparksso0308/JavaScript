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



## 리터럴(literal)
값을 만들 수 있도록 도와주는 문법체계 

	var o = {}		// 객체 리터럴
	var a = [1,2,3]		// 배열 리터럴


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

## this
함수 내에서 함수의 호출 맥락(context)
즉, 함수를 호출하는 방법에 따라 this의 의미가 달라진다.

### 함수 호출

	function func(){
	    if(window === this){
		console.log("window === this"); 
	    }
	}
	func();		// 실행 O
	
	결과
	this === window
	
### 메소드 호출

this === 메소드가 소속되어 있는 객체

	var o = {
	    func : function() {
		if( o === this) {
		    console.log("o === this");
		}
	    }
	}
	o.func();
	
	결과
	o === this
	

함수의 호출과 메소드의 호출은 결국 같다.

### apply
함수의 메소드인 apply를 이용해 this를 제어할 수 있다.

	var o = {}
	var p = {}
	function func(){
	    switch(this){
		case o:
		    document.write('o<br />');
		    break;
		case p:
		    document.write('p<br />');
		    break;
		case window:
		    document.write('window<br />');
		    break;          
	    }
	}
	func();
	func.apply(o);
	func.apply(p);
	
	결과
	window
	o
	p 

### 생성자의 호출 

	var funcThis = null; 

	function Func(){
	    funcThis = this;
	}
	var o1 = Func();
	if(funcThis === window){
	    document.write('window <br />');
	}

	var o2 = new Func();
	if(funcThis === o2){
	    document.write('o2 <br />');
	}
	결과
	window
	o2

생성자는 빈 객체를 만들고 이 객체내에서 this는 만들어진 객체를 가르킨다.

생성자가 실행되기 전까지 객체는 사용할 수 없다.

	function Func(){
  		 document.write(o);
	}
	var o = new Func();
	
	결과
	undefined		// o가 생성되기 전에 생성자에서 사용함
	

## 상속(inheritance)
객체의 로직을 그대로 물려받는 또 다른 객체를 만들 수 있는 기능 /
-> 코드의 재활용성이 높아짐

	function Person(name){
	    this.name= name;
	}
	Person.prototype.name = null;
	Person.prototype.introduce = function(){
	    return 'My name is '+this.name;
	}

	function Programmer(name){
	    this.name = name;
	}

	Programmer.prototype = new Person();    //상속

	var p1 = new Programmer('sso');
	document.write(p1.introduce()+ "<br / >");

	결과
	My name is sso

Programmer이라는 생성자를 만들고 이 생성자의 prototype과 Person객체를 연결하면 Programmer 객체도 메소드 introduce를 사용할 수 있게된다.

	function Person(name){
	    this.name= name;
	}
	Person.prototype.name = null;
	Person.prototype.introduce = function(){
	    return 'My name is '+this.name;
	}

	function Programmer(name){
	    this.name = name;
	}

	Programmer.prototype = new Person();    //상속
	Programmer.prototype.coding = function(){
	    return "Hello World";
	}

	var p1 = new Programmer('sso');
	document.write(p1.introduce()+ "<br / >");
	document.write(p1.coding()+"<br />");
	
	결과
	My name is sso
	Hello World
	
## prototype
객체의 원형
함수는 객체 -> 생성자로 사용되는 함수도 객체 ->객체는 property를 가짐 
->prototype이라는 property는 용도가 이미 약속되어있는 특수 property이다.

prototype에 저장된 속성들은 생성자를 통해서 객체가 만들어질 때 그 객체에 연결된다(prototype chain).

	function Ultra(){}
	Ultra.prototype.ultraProp = true;

	function Super(){}
	Super.prototype = new Ultra();

	function Sub(){}
	Sub.prototype = new Super();

	var o = new Sub();	
	console.log(o.ultraProp);

	결과
	true

prototype chain : prototype이 객체와 객체를 연결하는 체인 역할을 하는 것

1. 객체 o에서 ultraProp를 찾는다.
2. 없다면 Sub.prototype.ultraProp를 찾는다. 있다면 반환
2. 없다면 Super.prototype.ultraProp를 찾는다. 있다면 반환
2. 없다면 Ultra.prototype.ultraProp를 찾는다. 있다면 반환

! 주의
자식이 변하면, 부모도 변한다.

## 표준 내장 객체(Standard Built-in Object)
자바스크립트가 기본적으로 가지고 있는 객체들

* Object
* Funtion
* Array
* String
* Boolean
* Number
* Math
* Date
* RegExp

자바스크립트는 위와 같은 내장 객체를 가지고 있다.

배열에서 값을 랜덤하게 추출하기

	var arr = new Array('one','two','three','four', 'five');
	function getRandomValueFromArray(haystack){
	    var index = Math.floor(haystack.length*Math.random());	//수의 연산
	    return haystack[index]; 
	}
	console.log(getRandomValueFromArray(arr));
	
함수를 배열 객체에 포함시키기

	Array.prototype.rand = function(){
	    var index = Math.floor(this.length*Math.random());  //this === 배열 객체
	    return this[index];
	}
	var arr = new Array('one', 'two', 'three', 'four', 'five');
	console.log(arr.rand());

결과 실행할 때마다 배열의 값중 하나가 랜덤하게 출력된다.

## Object
object 객체는 객체의 가장 기본적인 형태를 가지고 있는 객체이다.
(아무것도 상속받지 않은 순수한 객체)
자바스크립트에서는 object를 값을 저장하는 기본적인 단위로 사용한다.

자바스크립트의 모든 객체는 Object 객체를 상속 받기 때문에 모든 객체는 object 객체의 프로퍼티를 가지고 있다.
(object의 prototype은 모든 객체가 사용가능하다.

prototype가 없는 메소드 사용

	//object.keys()
	var arr = ["a", "b","c"]
	console.log(Object.keys(arr));		// Object === 생성자 함수

prototype가 있는 메소드 사용
	//Object/prototype.toString()
	var o = new Object();			// 객체를 만듬
	console.log(o.toString());

	결과
	["0","1","2"]
	[object Object]

 ### Object 확장	
 
 	Object.prototype.contain =function(needle){
	   for (var name in this){//this=== 메소드가 소속되어 있는 객체 ===o===a
		if(this[name]===needle){
		    return true;
		}
	   } 
	   return false
	}

	var o = {'name':'park', 'city':'seoul'}
	console.log(o.contain('park'));
	var a = ['park','sso','yeon'];
	console.log(a.contain('sso'));

	결과
	true
	true

Object 확장은 모든 객체에 영향을 주기 때문에 신중하게 사용해야 한다.

객체.hasOwnProperty(property 이름) : 인자로 전달된 속성의 이름이 객체의 속성인지 여부를 판단한다(T/F)
만약 prototype으로 상속 받은 객체라면 false가 된다.

## 데이터 타입
원시 데이터 타입(객체가 아닌 데이터 타입) <-> 참조 자료형 (객체)
*숫자
*문자열
*boolean
*null
*undefined

wrapper object : 원시 데이터 형을 객체처럼 다룰 수 있도록 한 객체 (객체지향)
*숫자 		 -> Number
*문자열		->String
*boolean 	  -> Boolean
*null		  -> 없음
*undefined	  ->없음


## 참조(reference)

	var a = {'id':1};	// 객체(참조 자료형)
	var b = a;		// 참조
	b.id = 2;
	console.log(a.id);  // 2
결과
	2
	
만약 a의 값이 객체라면 참조 발생 O 복사 발생 X <br />
객체가 아니라 원시 데이터 타입이라면 참조 발생 X 복사 발생 O<br />

! 주의
	var a = {'id':1};
	var b = a;
	b={'id':2};		// 객체 생성 == 참조X
	console.log(a.id); 	//1
	
	결과
	1
	
## 함수와 참조
(1)
	var a = {'id':1};
	function func(b){		//b=a
	    b = {'id':2};		// b = {'id':2};
	}				// b와 a사이의 링크가 끊김
	func(a);
	console.log(a.id);  // 1
	
	결과
	1

 b = {'id':2}; b가 가리키는 객체를 변경했기 때문에 a에 영향을 미치지 않는다.

(2)
	var a = {'id':1};
	function func(b){	// b=a
	    b.id = 2;
	}
	func(a);
	console.log(a.id);  // 2
	
	결과
	1
	
	


매개 변수 b는 객체 a의 레퍼런스이므로 b를 수정하면 a에도 영향을 미친다.
