## var

### 변수 중복 선언 가능

```jsx
var x = 1;
var y = 2;

var x = 100;
var x = 1000000;
var y;

console.log(x); // 1000000
console.log(y); // 2
```

 → 이렇게 동작하는 프로그래밍 언어는 없기 때문에 비상식적인 동작을 한다고 볼 수 있음

### 함수의 코드 블록만 지역 스코프로 인정

var는 **함수의 코드 블록**만 지역 스코프로 인정한다. 

따라서 if 문 코드 블록은 무시가 되고 10이 출력이 된다. 

```jsx
var x = 1;

if(true) {
  var x = 10; // 코드 블록을 무시하고 변수 x는 전역 변수가 되어버린다...
}

console.log(x); // 10
```

→ 이것도 역시 비상식적인 동작을 한다고 볼 수 있음

참고로 같은 코드를 let 키워드를 사용해서 실행하면 1이 출력이 된다.

```jsx
let x = 1;

if(true) {
  let x = 10;
}

console.log(x); // 1
```

중복 선언 가능. 재할당 가능.

```jsx
var title = 'book';
console.log(title); *// book*var title = 'movie';
console.log(title); *//movie*

title = 'music';
console.log(title);*//music

console.log(score) // undefined
var score*
```

- var 는 원조 변수선언방식으로, 위 코드와 같이 선언한 변수가 동일한 이름으로 중복 선언이 가능하다. 즉, 마지막에 할당된 값이 최종 변수에 저장된다.
- 변수를 유연하게 사용할 수 있지만, 기존에 선언해둔 변수의 존재를 잊고 재선언 하는 경우 문제가 발생할 수 있다.
- 특히 간단한 코드가 아닌, 길고 복잡한 코드에서 같은 이름의 변수가 여러번 선언되어 사용되면 어떤 부분에서 값이 변경되고 문제가 발생하는지 파악하기 힘들다.

이를 보완하기 위해 ES6 부터 추가된 변수선언 방식이 let 과 const 이다.

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fc497181-e119-4e65-9ab2-05543f2b429e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230114%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230114T140544Z&X-Amz-Expires=86400&X-Amz-Signature=ff71cbdc118a28b7b6100c9147cd64b0801b430ed66f664a0490302bd389d583&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/fc497181-e119-4e65-9ab2-05543f2b429e/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230114%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230114T140544Z&X-Amz-Expires=86400&X-Amz-Signature=ff71cbdc118a28b7b6100c9147cd64b0801b430ed66f664a0490302bd389d583&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

변수는 `선언 단계`  > `초기화 단계`  > `할당 단계`  에 걸쳐 생성되는데

var 키워드 변수는 `선언 단계`와 `초기화 단계`가 동시에 진행된다. 즉, 자바스크립트 내부적으로 `실행 콘텍스트의` **변수 객채**에 변수를 등록하는 동시에 메모리를 **`undefined`**로 만들어버린다.

그렇기 때문에 변수에 값이 할당되기 전에 호출해도 `Reference` 에러가 발생하지 않고, `undefined`가 리턴된다.

### var 키워드의 문제점

1. var 호이스팅
2. 블록 스코프를 무시하고 동작
3. 변수 재할당, 재선언이 가능

 → 너무나 자기 마음대로 행동하는 녀석... 😰

**var를 쓰면 예상치 못한 버그가 생기기 너무나 쉽다!!**

let, const는 var의 문제점을 보완하기 위해 만들어진 아이들이고, 이제는 var 대신 let, const를 쓰면 된다. (굳이 var를 써야 하는 이유가 없다!)

## let

### 변수 중복 선언 불가

```jsx
let number = 5;

// 같은 변수 이름을 중복 선언할 수 없다
let number = 100;
```

### 블록레벨 스코프로 동작

```jsx
let x = 1; // 전역 변수

{
  let x = 2; // 지역 변수
  let y = 3; // 지역 변수
}

console.log(x); // 1
console.log(y); // error!
```

let은 var와 달리 중복선언 시, 해당 변수는 이미 선언되었다는 에러 메시지를 뱉는다.

즉, 중복선언이 불가하다. 하지만 변수에 값을 재할당하는 것은 가능하다.

`let` 키워드는 `var` 키워드와 다르게 **선언 단계** 와 **초기화 단계**가 분리되어 진행된다. 실행 컨텍스트의 **변수 객체** 에 변수를 등록했지만, 메모리에 할당되지 않아 접근할 수 없다. 

그래서 Reference Error: Cannot access before `initialization`  에러 문구가 나오는 것이다.

### 변수 호이스팅

let은 다른 프로그래밍 언어와 같이 동작한다

```jsx
console.log(num); // num이라는 변수는 아직 선언되지 않기 때문에 Error가 나온다.

let num;  // 변수 선언만 한 상태
console.log(num); // 아직 변수에 할당된 값이 없기 때문에 undefined가 출력된다.

num = 1; // 변수에 1을 할당
console.log(num); // 이제 변수에 1이라는 값이 할당되었기 때문에 1이 출력된다.
```

그럼 let, const는 호이스팅이 발생하지 않는 걸까...? → NO!🙅🏻‍♀️

<aside>
⚠️ let, const는 호이스팅이 발생하지 않는 것'처럼' 동작한다.(사실 호이스팅이 발생한다.)

</aside>

```jsx
let num = 1;

{
  console.log(num); // 전역 변수 1이 출력이 되는 게 아니라 에러가 출력이 된다
  let num = 100;
}

console.log(num);
```

**즉, 호이스팅 되지 않는 것이 아니라, 호이스팅은 되었으나 메모리가 할당되지 않아 접근할 수 없는 것이다.** 이때 등장하는 개념이 **TDZ** 이다.

## const

### const 키워드는 재할당 불가

const는 한번 값을 할당하면 재할당이 불가능하다

```jsx
const number = 1;
number = 2; // Error!

let num = 100;
num = 2; // 문제없음
```

const를 사용할 때는 선언과 동시에 값을 할당해야 한다.

```jsx
const x = 'apple';
```

이렇게 선언만 하면 에러가 나온다!👇

```jsx
const x; // SyntaxError!

let x; // 문제없음
```

### const는 상수로서 사용도 가능

const로 선언한 변수는 값을 변경할 수 없기 때문에 상수를 표현하는데 사용하기도 한다.

일반적으로 상수의 이름은 **대문자와 언더스코어(_)**를 사용한다.  

```jsx
const TAX_RATE = 0.1; // 상수

let price = 100;

let totalPrice = price + (price * TAX_RATE);
console.log(totalPrice); // 110
```

### 객체(object) 값은 변경 가능

const로 선언한 변수에 객체를 할당한 경우 값을 변경할 수 있다.

```jsx
const person = {
  name: 'Kim'
};

person.name = 'Lee';

console.log(person.name); // 'Lee'
```

### 언제 let를 쓰고 언제 const를 쓰면 될까...❓

재할당이 필요한 경우에만 let을 쓰고 **기본적으로는 const를 사용하면 된다!**👌

let 키워드 사용 예시 코드

```jsx
let count = 0;

for(let i = 0; i < 5; i++) {
  count += i;
}

console.log(count); // 10
```

let와 const의 차이는 **immutable(재할당)가능여부**이다. 재할당은 가능한 let과 달리 const는 재할당 또한 불가하다.

## ****function 키워드 함수****

![https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c52daf3a-9fbb-4659-81ec-ce532e184ff8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230114%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230114T140529Z&X-Amz-Expires=86400&X-Amz-Signature=ccc2514100040cade8435e79e69a7255e04132e7ad222f8b699a0452fe738f77&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/c52daf3a-9fbb-4659-81ec-ce532e184ff8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20230114%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20230114T140529Z&X-Amz-Expires=86400&X-Amz-Signature=ccc2514100040cade8435e79e69a7255e04132e7ad222f8b699a0452fe738f77&X-Amz-SignedHeaders=host&response-content-disposition=filename%3D%22Untitled.png%22&x-id=GetObject)

**함수 선언문**의 경우, **선언/초기화/할당** 단계가 모두 동시에 진행된다. 그래서 할당 전 호출해도 `undefined`가 아니라, 함수 내용이 리턴된다.

## References

[[JS] 호이스팅(Hoisting)을 이해해보자!](https://nuhends.tistory.com/111)

[](https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90)

[var, let, const 차이점](https://80000coding.oopy.io/e1721710-536f-43f2-823b-663389f5fbfa)
