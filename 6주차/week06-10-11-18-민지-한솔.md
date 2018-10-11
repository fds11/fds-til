# QUIZ


# Javascript
- `고차 함수 (Higher-order Function)` : 함수를 인수로 받는 함수 또는 함수를 반환하는 함수
  + forEach, map, reduce, filter, sort, every, some, find
  + bind 함수를 반환하는 함수
  + `콜백(callback)` : 다른 함수의 인수로 넘겨지는 함수
- 클로저 (Closure) 
  + 바깥 스코프에 있는 변수를 가져다 사용하는 함수 !
  + 변수가 저장되는 저장소
```js
function func1(x) {
  // 여기서 반환되는 함수는 바깥 스코프에 있는 변수 `x`를 사용하고 있습니다.
  return function () {
    return x;
  }
}

const func2 = func1(1);

// `func1`의 실행은 끝났지만, `func2`를 통해서 변수 `x`를 사용할 수 있습니다.
console.log(func2()); // 1 // *


function makerAdder(x) {
  return function(y) {
    return x + y ;
  }
}
const add2 = makeAdder(2) //2
console.log(add2(3)); //5
```
- 재귀함수 : 문제를 같은 형태의 부분문제로 쪼갤 수 있을 때, 재귀함수를 활용할 수 있다.
```js
// function sumBy(num){
//   let memory = 0;
//   for(let i =0; i <= num ; i++){
//     memory += i;
//   }
//   retunr memory
// }

function sumByRec(num){
  // return num===1 ? 1 : sumByRec(num - 1) + num
  if(num===1){
    return 1
  } else {
    return sumByRec(num - 1) + num
  }
}
sumByRec(5); // 1 + 2 + 3 + 4 + 5
// sumByRec(4) + 5 같은 형태의 부분문제로 쪼갤 수 있기때문에



//피보나치 재귀함수
function fibo(n){
  //다음단계의 수는 이전 두 단계 수의 합
  let x = 0;
  let y = 1;
  for(let i=0; i<n ; i++){
    const sum = x + y
    x = y //다음단계
    y = sum //다음단계
  }
  return x
}
fibo(2)

// fibo(5) = fibo(3) + fibo(4)
// 재귀함수 : 부분문제, 종료조건 생각하기
function fiboRec(n){
  if(n===0){
    return 0
  } else if(n===1){
    return 1
  } else {
    return fiboRec(n - 2) + fiboRec(n - 1);
  }
} 
fiboRec(7);
```
- 데이터 속성(Data Property)의 부수속성(Property Attribute) : 어떤 속성의 성질을 결정해서 만듬.
  + 속성은 지울 수도 있지만, 삭제 되지 않는 것도 있음 ex) delete Math.PI;
  + 객체의 부수속성을 알아보려면, Object.getOwnPropertyDescriptor라는 정적 메소드를 사용해 부수속성을 나타내는 객체를 얻을 수 있습니다. 이 객체를 일러 속성 기술자(property descriptor), Descriptor 라고 부릅니다. 
    * value: 속성에 어떤 값이 저장되어 있는지를 나타냅니다.
    *  writable: 변경할 수 있는 속성인지를 나타냅니다.
    *  enumerable: 열거 가능한 속성인지를 나타냅니다.
    *  configurable: 부수속성을 변경하거나 속성을 삭제할 수 있는지를 나타냅니다.
  + Object.getOwnPropertyDescriptors
  + enumerable: true, 을 해주지 않으면 default가 false
  + 접근자 속성을 쓰지 않고, 속성 값을 변경해야한다면 객체의 속성을 변경해도 다른 객체의 속성값이 영향받지 않음.
    * 생성자 호출할때 매개변수 won 하나만 받아서, prototype으로 여러가지 메소드 만들기 (ex/ 원,달러 등)
    => 코드가 길어진다. 속성을 사용하기위해 매번 메소드를 호출해야하는데 불-편, 
  + 대신! `getter`, `setter `  : 속성을 계산해서 반환을 할 수 있구나
- 객체의 속성 열거하기 : 객체 자신의 속성만 반환한다. 열거가능한 속성만(.keys(), .values(), .entries())
  + ex)
  ```js
  const obj = {
    a: 1,
    b: 2
  };

  // Object.keys(obj); // ['a', 'b']
  // Object.values(obj); // ['a', 'b']
  Object..entries(obj); // ['a', 'b']  
``
- Object.getOwnPropertyNames
- `.keys()` : for...in 대신 / 오해 : 정의된 순서대로 반환하기도 함
- `객체의` 얕은 복사(Shallow Copy) & 깊은 복사(Deep Copy)
  + const obj2 = Object.assign({}, obj);
  + 배열의 slice() / 객체의 객체, 객체의 배열 => 충첩된 객체는 복사하지 못함, 원본의 배열을 변경 / 겉껍질만 복사
- 깊은 복사는 라이브러리 사용
- 자바스크립트는 객체의 편집을 막아버리는 함수들이 존재한다.
```js
const obj = {};

// 객체에 속성이 추가되는 것을 막습니다.
// Object.preventExtensions(obj);
// 객체의 속성이 삭제되는 것을 막습니다.
Object.seal(obj);
// 변경,삭제 전부 막기
Object.freeze(obj);

function func() {
  'use strict';
  // obj.a = 1;
  delete obj.a;
}

func();
```