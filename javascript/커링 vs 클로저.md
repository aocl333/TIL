### Closure

클로저는 내부함수(클로저함수)에서 외부함수의 값을 사용하는 기법

```javascript
function closure(){
 function first(){console.log('first!')};
 function second(){console.log('seconde!')};
 function third(){console.log('third!')};
 return [first,second, third];
}

let f = closure;
f = f();
f[0](); // expected output -> 'first!'
f[1](); // expected output -> 'seconde!'
f[2](); // expected output -> 'third!'
var makeCounter = function() {
let privateCounter = 0;
function changeBy(val) {
privateCounter += val;
}
return {
increment: function() {
changeBy(1);
},
decrement: function() {
changeBy(-1);
},
value: function() {
return privateCounter;
}
}
};

var counter1 = makeCounter();
var counter2 = makeCounter();

console.log(counter1.value()); // returns 0
console.log(counter1.increment()); // adds 1
console.log(counter1.increment()); // adds 1
console.log(counter1.value()); // returns 2
console.log(counter1.decrement()); //subtracts 1
console.log(counter1.value()); // returns 1
console.log(counter2.value()); // returns 0
```

### Currying
Currying은 외부함수의 인자를 재사용하고 싶을때 사용하는 기법

```javascript
let greeting = function (a) {
    return function (b) {
        return a + ' ' + b
	}
}

//함수표현식 let greeting = (a) => (b) => a + ' ' + b 

let hello = greeting('Hello')
let morning = greeting('Good morning')

hello('Austin') // returns Hello Austin
hello('Roy') // returns Hello Roy
morning('Austin') // returns Good morning Austin
morning('Roy') //returns Good Morning Roy
```

### 참조
https://www.digitalocean.com/community/tutorials/an-introduction-to-closures-and-currying-in-javascript
