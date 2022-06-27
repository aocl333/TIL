
## 문제

아래와 같이 정의된 피보나치 수열 중 n번째 항의 수를 리턴해야 합니다.  

- 0번째 피보나치 수는 0이고, 1번째 피보나치 수는 1입니다. 그 다음 2번째 피보나치 수부터는 바로 직전의 두 피보나치 수의 합으로 정의합니다.
- 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, ...

## 입력

### 인자 1 : n

number 타입의 n (n은 0 이상의 정수)

## 출력

number 타입을 리턴해야합니다.

## 주의 사항

- 재귀함수를 이용해 구현해야 합니다.  
- 반복문(for, while) 사용은 금지됩니다.  
- 함수 fibonacci가 반드시 재귀함수일 필요는 없습니다.  

## 입출력 예시

```javascript
let output = fibonacci(0);
console.log(output); // --> 0
```

## 풀이
```javascript
let fibonacci = function (n) {
  const memo = [0, 1];
  const aux = (n) => {
    // 이미 해결한 적이 있으면, 메모해둔 정답을 리턴한다.
    if (memo[n] !== undefined) return memo[n];
    // 새롭게 풀어야하는 경우, 문제를 풀고 메모해둔다.
    memo[n] = aux(n - 1) + aux(n - 2);
    return memo[n];
  };
  return aux(n);
};
```
