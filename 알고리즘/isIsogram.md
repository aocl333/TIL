## 문제

문자열을 입력받아 아이소그램인지 여부를 리턴해야 합니다. 아이소그램(isogram)은 각 알파벳을 한번씩만 이용해서 만든 단어나 문구를 말합니다.

## 입력

### 인자 1 : str

string 타입의 공백이 없는 알파벳 문자열

## 출력

boolean 타입을 리턴해야 합니다.

## 주의사항

빈 문자열을 입력받은 경우, true를 리턴해야 합니다.<br>
대소문자는 구별하지 않습니다.


## 입출력 예시

```javascript
let output = isIsogram('aba');
console.log(output); // false

output = isIsogram('Dermatoglyphics');
console.log(output); // true

output = isIsogram('moOse');
console.log(output); // false
```

## 풀이
```javascript
function isIsogram(str) {
    if (str.length === 0) {
    return true;
  }

  let cache = {};
  let strLowered = str.toLowerCase();

  for (let i = 0; i < strLowered.length; i++) {
    if (cache[strLowered[i]]) {
      return false;
    }
    cache[strLowered[i]] = true;
  }

  return true;
}

```
