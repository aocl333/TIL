
# type of 연산자

- typeof는 변수의 데이터 타입을 반환하는 연산자입니다.

### typeof 연산자 사용법

<br>

```javascript
typeof 값;
```

### 개발자 도구를 이용해 실습하기

```javascript
console.log(typeof 1) // ----- (1)
console.log(typeof '1') // ----- (2)
console.log(typeof (1 < 2)) // ----- (3)
// const NotInUse = 'this is not used'
```

typeof 연산자를 사용하면 이렇게 간단하게 특정한 값의 타입을 확인할 수 있습니다.

```javascript
let number = 1;
console.log(typeof number) // --- (1)
let string = '1';
console.log(typeof string) // --- (2)
```

변수에 할당한 값도 typeof 연산자로 타입을 확인할 수 있습니다.
