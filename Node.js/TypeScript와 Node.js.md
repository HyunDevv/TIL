# TypeScript와 Node.js

---

작성 중 (21.09.12)

---

## JavaScript (ES6) 기초

### Data Type

- Number
- String
  - 글자 수 세기 : string.length
- Boolean
- Array
- Object
- ...

### Variable

- 변수 특징
  
- 변수는 문자와 숫자, $와 _만 사용
  - 첫글자는 숫자가 될 수 없다
  - 예약어는 사용불가
  - 가급적 상수는 대문자
  
- 변수 선언 방식

  - var

    ```javascript
        var name = 'bathingape'
        console.log(name) // bathingape
    
        var name = 'javascript'
        console.log(name) // javascript
    ```

  - let

    ```javascript
        let name = 'bathingape'
        console.log(name) // bathingape
    
        let name = 'javascript'
        console.log(name) 
        // Uncaught SyntaxError: Identifier 'name' has already been declared
    
        name = 'react'
        console.log(name) //react
    ```

  - const

    ```javascript
        const name = 'bathingape'
        console.log(name) // bathingape
    
        const name = 'javascript'
        console.log(name) 
        // Uncaught SyntaxError: Identifier 'name' has already been declared
    
        name = 'react'
        console.log(name) 
        //Uncaught TypeError: Assignment to constant variable.
    ```

  

  
- 호이스팅
  
  - var 선언문이나 function 선언문 등을 해당 스코프의 선두로 옮긴 것처럼 동작하는 특성
  
    - `var` 로 선언된 변수와는 달리 `let` 로 선언된 변수를 선언문 이전에 참조하면 참조 에러(ReferenceError)가 발생한다.
  
      ```js
      	console.log(foo); // undefined
      	var foo;
      
    	console.log(bar); // Error: Uncaught ReferenceError: bar is not defined
      	let bar;
    ```
  
    이는 `let` 로 선언된 변수는 스코프의 시작에서 변수의 선언까지 일시적 사각지대(Temporal Dead Zone; TDZ)에 빠지기 때문이다.
  
    참고로, 변수는 `선언 단계` > `초기화 단계` > `할당 단계` 에 걸쳐 생성되는데
  
      `var` 으로 선언된 변수는 선언 단계와 초기화 단계가 한번에 이루어진다. 하지만,
  
      ```js
      // 스코프의 선두에서 선언 단계와 초기화 단계가 실행된다.
      // 따라서 변수 선언문 이전에 변수를 참조할 수 있다.
      
      console.log(foo); // undefined
      
      var foo;
      console.log(foo); // undefined
      
    foo = 1; // 할당문에서 할당 단계가 실행된다.
      console.log(foo); // 1
    ```
  
      `let` 로 선언된 변수는 선언 단계와 초기화 단계가 분리되어 진행된다.
  
      ```js
      // 스코프의 선두에서 선언 단계가 실행된다.
      // 아직 변수가 초기화(메모리 공간 확보와 undefined로 초기화)되지 않았다.
      // 따라서 변수 선언문 이전에 변수를 참조할 수 없다.
      
      console.log(foo); // ReferenceError: foo is not defined
      
      let foo; // 변수 선언문에서 초기화 단계가 실행된다.
      console.log(foo); // undefined
      
    foo = 1; // 할당문에서 할당 단계가 실행된다.
      console.log(foo); // 1
    ```
  
  - 정리
  
    - 재할당이 필요한 경우에 한정해 `let` 을 사용한다. 이때, 변수의 스코프는 최대한 좁게 만든다.
    - 재할당이 필요 없는 상수와 객체에는 `const` 를 사용한다.



### Template Literal

```javascript
var name = 'egoing';
var letter = `Dear ${name}

Lorem ipsum dolor sit amet, ...
${name}`

console.log{letter};
```

### 형변환

- 명시적 형변환
  - String()                              // ex) String(3)
  - Number()                          // ex) Number("1234")
    - Number(null)             // 0
    - Number(undifined)   // NaN
  - Boolean()
    - false인 경우
      - 숫자 0
      - 빈 문자열 ''
      - null
      - undefined
      - NaN
    - ture인 경우
      - false를 제외 한 모든 것
- 자동 형변환

### 논리연산자

- || (OR)
- && (AND)
- ! (NOT)
- 논리 연산자를 사용 할때는 복잡한 조건을 앞에 배치하여 효율성을 높힌다

### 조건문

```javascript
if(){
   
}else if(){
         
}else{
    
}
```

### 반복문

- for

```javascript
for (let i = 0; i < 10; i++){
    // 반복할 코드
}
```

- while

```javascript
let i = 0;
while (i<10){
     // 코드
    i++;
}
```

- switch

```javascript
switch(fruit){
    case apple:
        // 사과일때 코드
    case banana:
    case melon:
        // 바나나나 멜론일때 코드
    ....
    default:
        // 아무것도 아닐 때
}
```



### 다양한 함수와 연산자

- typeof : 자료형 확인

  ```javascript
  console.log(typeof 3); // "number"
  console.log(typeof null); // "object"
  ```

- alert()

- const name = prompt("이름을 입력하세요. ");

  ![image-20210912153216706](md-images/image-20210912153216706.png)

- confirm() : 확인과 취소가 같이있다. (true/ flase)

### 함수

- ```javascript
  // default value
  
  function sayHello(name = 'friend'){
      let msg = `Hello, ${name}`
      console.log(msg)
  }
  
  sayHello();
  sayHello('Jane');
  ```

- 함수는 한번에 한작업에 집중



- 선언된 모든 함수는 시작 시 초기화 된다 (호이스팅)

- 함수 선언문 : 어디서든 호출 가능

  ```javascript
  function sayHello(){
  	console.log('Hello');
  }
  
  sayHello();
  ```

- 함수 표현식 : 코드에 도달하면 생성

  ```javascript
  let sayHello = function(){  // 생성
      console.log('Hello');   // 사용가능
  }
  
  sayHello();
  ```



- 화살표 함수

  - `let add = (num1, num2) => num1 + num2; `
  - `let sayHello = name => 'Hello, ${name}';`

  

- 함수로 객체 만들기

  ```javascript
  function makeObject(name, age){
      return {
          name : name,
          age : age,
          hobby : 'football'
      }
  }
  
  const Mike = makeObject('Mike', 30);
  console.log(Mike);
  ```

  



### Object

```javascript
const superman = {
    name : 'clark',
    age : 33,
}

// 접근
superman.name
// 추가
superman.gender = 'male';
// 삭제
delete superman.hairColor;
```

```javascript
// Object - 단축 프로퍼티
const name = 'clark';
const age = 33;

const superman = {
    name, // name : name
    age, // age : age
    gender : 'male',
}
```

``` javascript
// Object - 프로퍼티 존재 여부 확인
const superman = {
    name : 'clark',
    age : 33,
}

superman.birthDay; // undefined
'birthDay' in superman; // false
'age' in superman; // true

```

``` javascript
// 객체의 메서드
const user = {
    name : 'Mike',
    sayHello : function(){
        console.log(`Hello, I'm ${this.name}`);
    }
}

user.sayHello();
```

``` javascript
// 화살표 함수에서의 this
let boy = {
    name : 'Mike',
    sayHello : () => {
        console.log(this); // 전역객체 {브라우저 환경 : window, Node js : global} 
    }
}

boy.sayHello(); // this != boy
```



- for ... in 반복문 (객체 순회)

``` javascript
for(let key in superman){
    console.log(key)
    console.log(superman[key])
}
```



### 배열 (Array)

- 순서가 있는 리스트

- 특징

  - 문자, 숫자, 객체, 함수 등도 포함 가능

- array.length : 배열의 길이

- push('추가요소') : 배열 끝에 추가

- pop() : 배열 끝 요소 제거

- array.unshift(0,1) : 배열 앞에 추가

- array.shift() : 배열 앞에 제거

- 배열 반복문 기본

  ```javascript
  let days = ['월', '화', '수'];
  
  for(let index = 0; index < days.length; index++){
      console.log(days[index]);
  }
  ```

- 배열 반복문 : for ... of

  ``` javascript
  let days = ['월', '화', '수'];
  
  for(let day of days){
      console.log(day)
  }
  ```

  

---



## TypeScript

- 변수 값에 데이터 타입 지정
- 객체지향적
- 컴파일 타임 오류
- 타입스크립트를 자바스크립트로 컴파일

```typescript
// typescript
function add (a: number, b: number) {
    return a + b;
}

console.log(add('3', '5')) // error
```

- tsc --init
- tsc -w



### Type Inference (타입추론)

```typescript
let a = 5;
// a = 'x'; 오류
a = 8; // 변수 a 타입이 숫자(Number)로 타입추론이 되었다
```



### 타입 명시

```typescript
let studentID: number = 10;
let studentName: string = 'JaeHyun Kim';

function getStudentDetails(studentID: number):{
    studentID: number;
    studentName: string;
}{
    return null;
}
```



다음강의 : https://www.youtube.com/watch?v=jlzvXcDGZUU&list=PLJf6aFJoJtbUXW6T4lPUk7C66yEneX7MN&index=5

---

## 출처 

- JavaScript 기초 : https://www.youtube.com/watch?v=KF6t61yuPCY
- Node.js : https://www.youtube.com/playlist?list=PLuHgQVnccGMA9QQX5wqj6ThK7t2tsGxjm