- 

```javascript
alert('Welcome JS!!');
```



-  window 안에 document가 있지만 생략 가능

```javascript
document.write('<h1>Hello world!</h1>');
window.document.write("<h1 id='hi'>Hello world!</h1>");
```



- 변수 설정 var는 function-scoped

```javascript
var name = 'ssafy';
```



- for문

```javascript
var a = 30

for (var a = 0; a < 10 ;a ++){
    console.log(a)
}
console.log(a)
```



- Uncaught ReferenceError: i is not defined

```javascript
function count () {
    for(var i=0; i<10; i++){
        console.log('i',i)
    }
}
count ()
console.log('after loop i is',i)
```



- Identifier 'word' has already been declared
   let은 한번더 let으로 재정의가 안됨

```javascript
let word = "안녕하세요";
document.write(word);

word = "안녕하세요";
document.write(word);

let word = "이건 들어감???"
```



- const(상수) : 바뀌지 않음

```javascript
const word = "외안되";
document.write(word);

word = "왜안돼";
document.write(word);
```



- python의 f-string

```javascript
const firstName = "SANGGWON";
const lastName = "CHA";
const fullName = firstName + lastName;
document.write('<h1>'+fullName+'!!'+'</h1>');
// + 기호로 합치는게 가능

document.write(`<h1>${fullName}!!</h1>`);
```



- python의 print

```javascript
const firstName = "SANGGWON";
const lastName = "CHA";
const fullName = firstName + lastName;
console.log(`Consloe ${fullName}`);
```



- python의 input

```javascript
const userName = prompt("너 누구야??")

let message = `${userName}님 반갑습니다!`
document.write(`<h1>${message}</h1>`)
```



- if else if else

```javascript
if (userName === "admin"){
    document.write("관리자님 안녕하세요")
} else if (userName === "sang") {
    document.write("상권님 안녕하세요")
} else {
    document.write(`${userName}님 안녕하세요`)
}
```



- === : 엄격한 같음(형을 비교)
- == : 느슨한 같음(값을 비교)



- 삼항연산자

```javascript
const number = 10
let result = number === 10 ? document.write(`<h1>정답입니다.</h1>`):document.write(`<h1>정답이 아닙니다.</h1>`)
```



- hoisting(지양)

```javascript
console.log(number)
var number = 10
console.log(number)
---------------------
var number
console.log(number)
number = 10
consloe.log(number)
```



- 반복문

```javascript
let i = 0;

while(i<10){
    console.log(i)
    i++
}

----------------------
for(let i = 0; i<10; i++){
    console.log(i)
}

---------------------
let list = [1,2,3,4]

for(let item of list){
    console.log(item)
}
for(const item of list){
    console.log(item)
}
// const item이 서로 다른 {}에 있기때문에 간섭하지 않음
```



- 다양한 함수

```javascript
let numbers = [1,2,3,4]

numbers.reverse(); 
// 반대로
numbers.push('a');
// 오른쪽에 추가
numbers.pop();
// 오른쪽 삭제
numbers.unshift('a');
// 왼쪽에 추가
numbers.includes(1);
// 1이 있는지 확인(변수로 활용)
numbers.indexOf('b');
// 있으면 index, 없으면 -1(변수로 활용)
numbers.join('-');
// 사이에 '-'를 넣어줌(변수로 활용)
console.log(numbers)
```



- 오브젝트

```javascript
const me = {
    name : 'ssafy',
    'phone number': '010123456',
    languageLevel : {
        python: 'master',
        django: 'pro',
        javascript: 'junior',
    }
}
console.log(me.name)
console.log(me['phone number'])
console.log(me.languageLevel.python)
console.log(me.languageLevel.django)
console.log(me.languageLevel.javascript)
```



- 타입확인

```javascript
const dessert = {
    coffee : 'Americano',
    iceCream : 'Cookie and cream',
}
console.log(typeof(dessert))
console.log(typeof dessert)
```



- JSON

```javascript
const dessert = {
    coffee : 'Americano',
    iceCream : 'Cookie and cream',
}
console.log(typeof(dessert))
console.log(dessert)

const jsonData = JSON.stringify(dessert);
console.log(typeof(jsonData))
console.log(jsonData)
// 보낼때 string 변환

const parseData = JSON.parse(jsonData);
console.log(typeof(parseData))
console.log(parseData)
// 받을때는 object로 parsing

------출력-------
object
{ coffee: 'Americano', iceCream: 'Cookie and cream' }
string
{"coffee":"Americano","iceCream":"Cookie and cream"}
object
{ coffee: 'Americano', iceCream: 'Cookie and cream' }
```



- 함수(1급객체)
  - first-class citizen의 조건
    - 변수나 데이터 구조안에 담을 수 있다.
    - 파라미터로 전달 할 수 있다.
    - 리턴 값으로 사용할 수 있다.

```javascript
function add(a,b){
    return a+b
}

console.log(add(5,10))
-----------1-------------

const add = function (a,b){
    return a+b
}

console.log(add(5,10))

-----------2-------------

const sub = (num1,num2) => {
    return num1-num2
}

console.log(sub(10,5))

-----------3-------------

let square = (num) => {
    return num**2
}
console.log(square(3))

square = (num) => num **2;
console.log(square(3))
```



- arrow function expression

```javascript
const min = (list) => {
    let min_num = Infinity;
    // 여기서 정의한 let은 block 안에서는 모든 같은 값을 참조한다.
    for(let num of list){
        if (num <= min_num){
            min_num = num;
        }
    }
    return min_num
}
console.log(min([1,2,3,4]))
```



- 기본인자함수

```javascript
const sayHello = (name="noName") => console.log(`hi ${name}`)
sayHello('join');
sayHello()
```



- 익명함수

```javascript
(function (num) { console.log(num**3)})(5);
((num) => {console.log(num**3)})(5);
```



- 함수안의 함수를 변수로

```javascript
const numbersEach = (numbers, callback) => {
    let sum
    for (const number of numbers) {
        sum = callback(number, sum)
    }
    return sum
}

const addEach = (number, sum=0) => {
    return number + sum
}

console.log(numbersEach([1,2,3],addEach))
```

