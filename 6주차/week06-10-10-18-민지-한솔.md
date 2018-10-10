# QUIZ

# javascript 
- 유효범위
  + let과 const가 바로 `블록 스코프(block scope)`
  + 함수의 매개변수나 var 변수는 `함수 스코프`
- 전역변수
  + 변수를 명시적으로 전역 스코프에서 선언하지 않더라도, 한 번도 선언되지 않은 이름으로 안쪽 스코프에서 let, const, var를 붙여주지 않고 변수를 선언하면 전역 스코프에 변수가 만들어집니다. 
  > 쓰지않기
```js
// 전역 scope에 변수가 생김
  function func() {
  variable = 1; // `variable`이라는 변수가 선언된 적 없으므로, 전역 변수가 됩니다.
}
func();
console.log(variable); // 1

//ex) 전역 변수에 의존해서 프로그래밍을 하는 것은 굉장히 금기시되는 일입니다. 
var i;
for(i=0;i<3;i++){
  console.log(i);
}
```
- 참조 (Reference)
- 원시타입을 인수로 넘길 때, 원본을 변경할 수 없지만, `참조타입`을 인수로 넘길 때 원본을 변경할 수 있다.
  + Primitive : 자바스크립트는 동적 언어로, 타입을 미리 선언할 필요가 없다. 타입은 프로그램이 처리되는 과정에서 자동으로 파악됨.
    > ex) string, number, boolean, null, undefined, symbol 
    * 원본을 변경할 수 있는 방법이 없다. 값의 `불변성`
    * 기존 문자열의 내용을 바꾸는 것이 아니라 새 문자열을 반환합니다.
    * 재대입 가능
  + Reference : 참조, 화살표 / 객체가 컴퓨터 메모리 상에서 어디에 저장되었는지를 가리키는 값
    * 배열의 원본을 변경 가능 => 값을 재대입한다던가, push를 이용해서 변경 등
  + 함수로 호출할땐 값이 복사되어, `객체`를 써주면 참조(화살표)가 복사되어 (원본변경)
  + 위의 등호 연산자 역시, 객체의 내용을 비교하는 것이 아니라 객체의 참조를 비교합니다.
```js
//01
{prop: 1} === {prop: 1}; // false
[1, 2, 3] === [1, 2, 3]; // false
//02
const obj1 = {};
const obj2 = obj1;
obj1 === obj2; // true
```
  + `참조가 같은지 다른지(등호연산자) / 값이 같은지 다른지(라이브러리[npm 'fast-deep-equal'],직접구현) 생각해서 비교해야함.`
```js
//직접 메소드를 만들어서 비교
function User(id) {
this.id = id;
}

User.prototype.isEqual = function(other) {
return this.id === other.id;
}

const john1 = new User('john');
const john2 = new User('john');

john1 === john2; // false
john1.isEqual(john2); // true
```
- 불변성 (Immutability)
  + Object.freeze를 호출한다고 해서 객체 안에 있는 객체까지 얼려버리지는 않으므로, 중첩된 객체에는 Object.freeze를 사용하기가 조금 까다롭습니다.
  + Immutable.js 
    * 불변인 것처럼 사용
  + const와 불변성을 잘 구분하시길 바랍니다.  
- 래퍼 객체 (Wrapper Object)
  + 원시 타입의 값에 대해 속성을 읽으려고 시도하면, 그 값은 그 순간에만 객체로 변환되어 마치 객체인 것처럼 동작합니다.
  + 아래는 래퍼 객체를 생성시키기 위해 사용되는 생성자들의 목록입니다.
    * String
    * Number
    * Boolean
    * Symbol
- `This`
  + 함수에서의 this : window
  + this 바꿔치기
  ```js
  function printGrade(grade) {
  console.log(`${this.name} 님의 점수는 ${grade}점입니다.`);
  }

  const student = {name: 'Mary'};
  const printGradeForMary = printGrade.bind(student);

  printGradeForMary(100); // Mary 님의 점수는 100점입니다.
  ```
  + 함수를 실행할때 this를 바꿔치기 할 수 있는 방법
  ```js
  function printGrade(grade) {
  console.log(`${this.name} 님의 점수는 ${grade}점입니다.`);
  }

  const student = {name: 'Mary'};

  //call() this 는 student로 하고 첫번째 인수를 100으로 해라
  printGrade.call(student, 100); // Mary 님의 점수는 100점입니다.

  //apply this 는 student로 하고 첫번째 인수를 100으로 해라
  // 인수 목록을 명시해주는 방법이 다름 []
  printGrade.apply(student, [100]); // Mary 님의 점수는 100점입니다.
``

- arguments와 나머지 매개변수 (Rest Parameters)
  + 인수갯수에 영향이 없는 함수
  + arguments는 배열이 아니라서 메소드 사용에 제한이 있음. `인수가 들어있는 배열`을 만드려면 ...을 붙여사용 => 나머지 매개변수
  + 단, ... 문법은 마지막 매개변수에만 사용할 수 있습니다.
  + 매개변수의 갯수와 인수의 갯수가 달라도 에러가 나지 않음. => ex) .reduce(매개변수), .map(매개변수)에서 정해진 매개변수를 다 전달하지 않아도됨. 필요없는 매개변수를 생략해 줄 수 있다.
- 화살표함수
  + function으로 생성된 함수는 prototype 속성을 가진다. 하지만 화살표 함수는 없음. 때문에 생성자를 가질 수 없다.
  const func = () => {

  } 
  + 화살표함수는 스스로의 this, arguments, super를 가지지 않습니다.  
  + `call(), bind()`로 화살표함수의 this를 바꿀 수 없다. => this 고정
  + 화살표 함수 내부에서 this를 사용하면 함수가 정의된 스코프에 있는 this를 가리킨다고 했습니다. 즉, 화살표 함수 내부의 this는 화살표 함수가 정의된 문맥에 의해 결정됩니다. 
  + function 키워드로 작성된 함수의 this는 `호출된 형태`에 따라서 this가 가리키는 값이 달라진다.
```js
  function getName(){
    retun this.name;
  }
  //만약에 위의 함수가 화살표 함수 라면 전역객체의 this / ex) mary.getName() => //window
  const getName = () => {
    retun this.name;
  }
  const mary = {
    name : 'mary',
    getName
  }
  const john = {
    name : 'john',
    getName
  }

  //this : mary
  function Person(name) {
    this.name = name;
    this.getName = () => {
      return this.name;
    }
  }
  const mary = new Person('mary');

```
- 매개변수의 기본값(default parameter)


# snakeGame
- 역할부여