### 얕은 복사(shallow copy)

- 얕은 복사는 참조(주소)값 의 복사를 나타낸다.
- 참조 자료형을 복사할 때 변수가 객체의 주소를 가리키고 있기 때문에 복사된 변수 또한 객체가 저장된 메모리 공간의 참조를 가리킨다. 그래서 복사를 하고 객체를 수정하면 두 변수는 똑같은 참조를 가리키고 있기 때문에 기존 객체를 저장한 변수에 영향을 끼친다.

```javascript
const obj1 = { value: 1 };
const obj2 = obj1;

obj2.value = 2;

console.log(obj1.value); // 2
console.log(obj1 === obj2); //true 
```

### 깊은 복사(deep copy)

- 깊은 복사는 실제 값의 복사 를 나타낸다.
- 원시 자료형를 복사할 때 또다른 독립적인 메모리 공간에 값 자체를 할당하기 때문에, 복사를 하고 값을 수정해도 기존 원시값을 저장한 변수에는 영향을 끼치지 않는다.

```javascript
let a = 1;
let b = a;

b = 2;

console.log(a); //1
console.log(b); //2
console.log(a === b); //false
```
