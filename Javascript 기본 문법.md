# Javascript



## this

1. `window`

   그냥 쓰거나 함수 안에서 `this` 를 쓰면  `window` 를 뜻한다.

   `window` 란?

   모든 함수, 전역변수, DOM을 보관하고 관리하는 전역객체라고 사전적 정의가 나와있다.

   좀 더 쉽게 풀이하자면,

   alert(), console.log() 등등 평소 쓰는 자바스크립트 함수들을 보관하는 `보관소` 라고 생각하면 좀 더 이해하기 쉽다.

2. Father? Mother?

   `object` 내의 함수가 있을 수 있는데 그 안에 있는 `this` 는 자신의 주일을 나타낸다.

   예를 들어 아래와 같이 `object` 를 만들었을 때 `this` 는 상수인 `fastfood` 의 `data`, `type` 를 출력한다.

   즉, 그 `object` 를 말한다.

   ```javascript
   const fastfood = {
   	data: "Burger King",
   	type: function () {console.log(this) }
   	}
   
   fastfood.type();
   ```

   ```javascript
   { data: 'Burger King', type: [Function: type] }
   ```

   

## spread operator

`...` 이다.

`...` 을 array에 붙이면 안에 있는 모든 원소들을 나열하고 Object에 붙이면 열거할 수 있는 모든 property를 나열한다.

즉, **괄호를 제거해주는 연산자**이다.

```javascript
let example = ['Hi', 'Jacob'];
console.log(...example);
```

위와 같이 했을 때 콘솔창에는 `'HI', 'Jacob'` 이렇게 출력이 된다.

또한 문자에 붙이면 문자를 분해 해준다.

```javascript
let example = 'Jacob';
console.log(...example);
```

이렇게 콘솔창에 쳤을 때 `'J', 'a', 'c', 'o', 'b'` 이렇게 출력이 된다.

### array 합치기, 복사하기 🖨

1. array 합치기

   간단하게 변수로 만들어서 앞에 `...` 을 붙여주면 합쳐진다.

   ```javascript
   let example = [1,2,3];
   let example2 = [4,5,6];
   let combined = [...example, ...example2];
   console.log(combined);
   ```

   위와 같이 콘솔창에 입력했을 때 결과는 `[1, 2, 3, 4, 5, 6]` 이 출력된다.

2. array 복사하기

   array를 복사하기 위해서 아래와 같은 방법을 쓰는 경우가 있다.

   ```javascript
   let example = [1,2,3];
   let exampleCopy = example;
   ```

   위와 같은 방법을 쓴다면 값을 공유하는 경우가 되기 때문에 이렇게 사용 X

   안전하게 copy하는 방법은 아래와 같이 하는 것이다.

   ```javascript
   let example = [1,2,3];
   let exampleCopy = [...example];
   console.log(exampleCopy);
   ```

   위와 같이 콘솔창에 출력하면 완벽히 복사한 것을 확인할 수 있다.

3. Object 합치기/복사하기

   array 합치기/복사하기와 거의 흡사하다.

   다른 점이 있다면 **값이 중복되는 경우이다.**

   그럼 가장 뒤에 있는 값을 사용한다.

   ```javascript
   let example = { a: 1, b: 2 };
   let example2 = { a: 3, ...example };
   console.log(example2);
   ```

   위와 같이 콘솔창에 입력했을 때 값은 `{ a: 1, b: 2 }`이렇게 출력이 된다.

   > **spread operator는 함수소괄호, 오브젝트 중괄호내, 어레이 대괄호내에서 보통 사용해야한다.**
   >
   > **다른 곳에서는 에러가 발생할 수 있다.**



## constructor

1. constructor `상속`이라고 한다.

   object를 생성해주는 constructor가 안에 있는 속성을 물려받아 object를 하나 생성하기 때문이다.

   쓰는 이유는 `object`를 쉽게 생성하려고 쓴다.

2. constructor 사용 방법

   기본적으로는 

   ```javascript
   function example() {
   			this.name = 'park',
       this.age = '20'  
   		}
   new example ();
   ```

   이렇게 쓰며 이를 콘솔창에 입력해보면 `{ name: 'park', age:'20' }`이라고 나온다.

   이를 좀 더 심화버전으로 사용한다면

   ```javascript
   function example (a,b) {
       this.name = a,
       this.age = b,
       this.Hi = function () {
           console.log('HI ' + this.name + ' ' + this.age)
       }
    }
   let person1 = new example ('park', 20);
   let person2 = new example ('Choi', 30);
   person1.Hi();
   person2.Hi();
   ```

   `HI park 20 HI Choi 30`가 출력된다.

#### Prototype ?

`prototype`의 사전적 정의는 원형, 초기단계 등이라고 나오지만 **유전자**라고 알고 있으면 이해가 쉽다. prototype을 쓰는 이유는 constructor에서 추가적으로 값이나 속성을 더 사용하고 싶을 때 사용한다.

```javascript
function example () {
    this.name = 'park',
    this.age = '20'
}
example.prototype.occupation = 'developer';
let person1 = new example();
console.log(person1.occupation);
```

`developer` 가 출력된다.

하지만 `console.log(example.occupation)` 이라고 치면 출력이 되지 않는다.
이유는 prototype은 object의 자료형으로 사용하면 안되기 때문이다.

그리고 값이 example라는 함수에 값이 새로 할당된다기 보다 `prototype`이라는 새로운 공간에 저장한다고 생각하면 된다. 즉, example이 가지고 있는 자료가 아닌 `prototype = 유전자, 원형`이 가지고 있기 때문에 example 안에서 자료형으로는 출력이 안된다.



## class

class는 상속을 하고 싶을 대 사용하는 템플릿 기계이다.

사전적 의미는 `클래스는 오브젝트를 만들기 위해 템플릿`이라고 한다.

#### 사용방법

간단히 클래스 이름을 지어주면 된다.

```javascript
class father {
	constructor(){
		this.name = 'Park',
		this.age = '55'
	}
}
let son = new father();
```

이렇게 사용을 하면 되고 `son`은 `father` 안에 있는 속성을 다 사용할 수 있다.

#### extends?

extends는 앞에 있는 class를 복사해서 사용하고 싶을 때 사용한다.

```javascript
class father{
    constructor(a){
        this.name = 'Park',
        this.age = a
    }
}
class son extends father{
    constructor(a){
        super(a);
        this.occupation = 'Doctor'
    }
}
let person = new son('55')
console.log(person);
```

이렇게 사용하면 되고 `extends`를 사용함으로써 `father` 안에 있는 속성을 전부 다 `son` 으로 가져온다. 그리고 잊지말아야 할 점은 `super를 꼭 써줘야 한다. 

출력 `son { name: 'Park', age: '55', occupation: 'Doctor' }`  이라는 object가 출력된다.



## Toggle

Toggle이란? 전등스위치처럼 on/off 할 수 있는 기능

#### Toggle로 navbar on/off 만들어 보기

 ``` javascript
 <body>
   <button id="btn">☰</button>
 	<div id="nav">
     <ul>
     	<li>menu1</li>
 			<li>menu2</li>
 			<li>menu3</li>
 		</ul>
 	</div>
 
 	<script>
     const btn = document.getElementById('btn');
 		const nav = document.getElementById('nav');
 
 		btn.addEcentListener('click', () => {
     	nav.classlist.toggle('active');
       btn.classList.toggle('active');
     });
 	</script>
 </body>
 ```

코드 설명 :

`button` 과 `nav` 에 아이디를 부여해서 자바스크립트애서 `const 상수` 에 각각 저장한다.
그리고 `btn` 에 `addEventListener` 로 이벤트를 주고 클릭할 때 마다 `active` 클래스르르 `toggle` 로 부여해준다.
마지막으로 css에서 

```javascript
nav{
  	position: fixed;
  	top: 0;
  	right: 0;
  	transform: translateX(100%);
    transitionL transform 0.3s ease-in-out;
}

nav.active{
 		transform: translateX(0);
}
```

이렇게 `transform` 으로 숨김과 나타냄 효과를 주면 깔끔하게 `toggle로 navbara : ham button` 을 만들 수 있다.

