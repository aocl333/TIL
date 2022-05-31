## 문제

문자열을 입력받아 문자열을 구성하는 각 단어의 첫 글자로 이루어진 문자열을 리턴해야 합니다.

## 입력

### 인자 1 : str
number 타입의 정수 (num >= 1)

## 출력
string 타입을 리턴해야 합니다.

## 주의 사항
단어는 공백 한 칸으로 구분합니다.<br>
연속된 공백은 없다고 가정합니다.<br>
빈 문자열을 입력받은 경우, 빈 문자열을 리턴해야 합니다.

## 입출력 예시

```javascript
let output = firstCharacter('hello world');
console.log(output); // --> "hw"

output = firstCharacter(
  'The community at Code States might be the biggest asset'
);
console.log(output); // --> "TcaCSmbtba"
```

## 풀이
```javascript
function firstCharacter(str) {
  // TODO: 여기에 코드를 작성합니다.
  if(str === ''){
    return ''
  }
  let words = str.split(' ');
  let result= '';
  for(let i = 0; i < words.length; i += 1){
    result = result + words[i][0];
  }
  return result;
}
```
