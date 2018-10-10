# 객체

- 비슷한 객체들이 공유하는 속성을 한 곳에 모아두기 위해 '프로토타입' 사용!
- 프로토타입 기능을 이용해 한 객체에서 다른 객체의 기능을 가져와 사용하는 것을 프로토타입 상속(prototype inheritance)이라고 합니다. 위와 같은 경우는 "personPrototype은 person1의 프로토타입이다.", "person1 객체는 personPrototype 객체를 상속받았다"고 표현
`person1의 부모는 personPrototype이다` 라고 말하기도함.
- 객체 리터럴을 통해 생성된 객체의 프로토타입에는 자동으로 Object.prototype이 지정됩니다.
```js
const parent = {
  a: 1
};
const child = {
  b: 2
};
Object.setPrototypeOf(child, parent); //child 의 부모를 parent로 지정
//parent를 상속받아도, a라는 속성이 child에 실제 속성이 들어가지 않음.
console.log(child); // { 'b': 2 }
console.log(child.a); // 1
//child에는 없으니까 '부모'를 봄. '부모'를 없다면, '부모의 부모' / 프로토타입객체(부모)까지 본다. => 상속
//프로토타입 체인을 올라가다가 처음 만나는 속성을 사용함
```
- 그래도 찾지 못하면 그때서야 속성값으로 undefined를 반환합니다 => 없는 속성
- Object.prototype.isPrototypeOf
- 자식객체를 통해서 프로토타입을 간접적으로 변경하는 것은 불가능 => 읽어오기만 가능
- Object.getPrototypeOf(person1) === Person.prototype; // true
  + 생성자로부터 생성된 인스턴스는 생성자의 부모다.
  + 생성자 문법 (ES2015 이전)
  ```js
function Person (name) {
  this.name = name;
}
Person.prototype.familyName = 's'
Person.prototype.introduce = function(){
  console.log(`안녕하세요. ${this.familyName}${this.name}입니다.`);
}
const person1 = new Person('dd')
person1.introduce();
//new Person 문법으로 인스턴스 생성하면 부모로 자동설정 === 생성자.prototype
// 인스턴스의 부모 === 생성자 부모
//return 없어서 확인
```
- function 키워드 함수로 만들어진 메소드 내부의 this는 `호출되는 시점`에 결정 vs `화살표함수`의 this는 `정의되는 시점`
  +
  ```js 
  Person.prototype.introduce = function(){
  console.log(`안녕하세요. ${this.familyName}${this.name}입니다.`);
  }
  person1.introduce(); //01. person1이 this에 
  person2.introduce(); 
```
- 객체.constructor === 생성자 => prototype에 constructor 속성이 자동 생성됨
```js
function Person() {
  // ...
}
const person = new Person();
person.constructor === Person;
```
- Person.compareAge : 프로토타입 체인에 들어있지 않음 ex)Array.from()
- Person.prototype.compareAge : this가 필요한 경우 ex)push() : 특정 배열에 접근
- `reduce();`
  + reduce를 가지고 메소드를 만들 수도 있음
```js
const arr = [1, 2, 3];
arr.reduce((누적값, item) => acc + item, 0);  // 6
// default 값 : 0

//기본형태
arr.reduce((acc, item, index, array) => {
  return acc + `(${index}: ${item})`;
}, '');
// index 생략하면 item[0]을 사용하기 때문에 초기 누적값을 항상 적어주는게 좋다!

//ex
function filter(arr, func) {
  return arr.reduce(function(acc, item) {
    if (func(item)) {
      acc.push(item)
    }
    return acc
  }, [])
}

const arr = [1, 2, 3, 4, 5]

filter(arr, x => x % 2 === 0)

```
> 배열을순회할때 순회중인 배열을 편집해서는 안된다!