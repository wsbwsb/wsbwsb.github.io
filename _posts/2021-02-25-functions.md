---
title: Javascript(3) - Arrow Function은 무엇인가? 함수의 선언과 표현
categories: [dev]
comments: true
---

### 드림코딩 엘리 Javascript 강의 (3)

### Arrow Function은 무엇인가? 함수의 선언과 표현

```js
//Function
//하나의 함수는 한가지 일만 하게 만들어야 한다.
//함수 이름은 무언가를 동작하는것이기 때문에 동사형태로 이름을 짓는다. ex) doSomething
//자바스크립트에서 함수는 object의 일종이다
function printHello() {
    console.log('Hello');
}
printHello();

//위 처럼 함수를 짜면 hello밖에 출력이 안되기 때문에 좀 더 유용한 함수를 만들려면
//밑 함수처럼 파라미터로 message를 전달하면 전달된 메세지를 화면에 출력되게 한다.
function log(message) {
    console.log(message);
}
log('Hello@');

//- Parameters
//Premitive parameter: passed by value
//object parameter: passed by reference
function changeName(obj) {
    obj.name = 'coder';
}
const sobin = { name: 'sobin' };
changeName(sobin);
console.log(sobin);

//- Default parameters(added in ES6)
function showMessage(message, from = 'unknown') {
    console.log(`${message} by ${from}`);
}
showMessage('Hi!');

//- Rest parameters (added in ES6) ... <-rest parameter 배열형태로 전달.
function printAll(...args) {
    for (let i = 0; i < args.length; i++) {
        console.log(args[i]);
    }
    for (const arg of args) {
        console.log(arg);
    } //for-of 문법으로 간단하게 출력할수도 있음. args에 있는 값들이 arg로 하나씩 전달이되면서 출력

    args.forEach((arg) => console.log(arg)); //forEach문으로 더 간단하게 작성가능
}
printAll('dream', 'coding', 'ellie');

//- Local scope 자바스크립트에서 scope란 밖에서는 안이 보이지 않고 안에서만 밖을 볼 수 있다.
let globalMessage = 'global'; //global variable
function printMessage() {
    //{}안에 출력하면 지역변수라고 한다.
    let message = 'hello';
    console.log(message); //local variable
    console.log(globalMessage);
    function printAnother() {
        console.log(message);
        let childMessage = 'hello';
    }
}
printMessage();

//- Return a value
function sum(a, b) {
    return a + b;
}
const result = sum(1, 2); //3
console.log(`sum: ${sum(1, 2)}`);

//- Early return, early exit 현업 포인트
//나쁜 예
function upgradeUser(user) {
    if (user.point > 10) {
        //long upgrade logic...
    }
}
//좋은 예 (조건이 맞지 않는경우, 값이 undefined인경우, 값이-1인경우 빨리 리턴하고 필요한 로직을 작성하는것이 좋다!)
function upgradeIser(user) {
    if (user.point <= 10) {
        return;
    }
    //long upgrade logic...
}

//Function expression
const print = function () {
    //anonymous function
    console.log('print');
};
print();
const printAgain = print;
printAgain();
const sumAgain = sum;
console.log(sumAgain(1, 3));

//Callback function using function expression
function randomQuiz(answer, printYes, printNo) {
    if (answer === 'love you') {
        printYes();
    } else {
        printNo();
    }
}
const printYes = function () {
    //anonymous function
    console.log('Yes!');
};
const printNo = function print() {
    //named function
    console.log('no!'); //디버깅 할때 함수의 이름이 나오게 할때, 함수 안에서 자신 스스로 또다른 함수를 호출할때(recursions)
};
randomQuiz('wrong', printYes, printNo);
randomQuiz('love you', printYes, printNo);

//Arrow function
//항상 이름이 없는 함수

//일반적으로 함수 쓸 때
const simplePrint1 = function () {
    console.log('simplePrint!');
};
simplePrint1();

//arrow함수 쓸때
const simplePrint2 = () => console.log('simplePrint!');
simplePrint2();

const add1 = (a, b) => a + b;
//->풀어서 쓰면
const add2 = function (a, b) {
    return a + b;
};

const simpleMultiply = (a, b) => {
    //do something more
    return a * b; //arrow함수에서 블록씌울땐 return을 써서 값을 출력해준다
};

//IIFE : Immediately Invoked Function Expression
(function hello() {
    console.log('IIFE');
})(); //함수를 따로 호출하지 않아도 이렇게 써주면 호출까지 된다.

//Fun quiz time💖
//function calculate(command, a, b)
//command: add, substract, divide, multiply, remainder

function calculate(command, a, b) {
    switch (command) {
        case 'add':
            return a + b;
        case 'substract':
            return a - b;
        case 'divide':
            return a / b;
        case 'multiply':
            return a * b;
        case 'remainder':
            return a % b;
        default:
            throw Error('unkown command');
    }
}
console.log(calculate('add', 2, 3));
```
