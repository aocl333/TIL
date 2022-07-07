## Redux란?

React에서 사용 가능한 JavaScript 상태관리 라이브러리이다.

### Redux의 구조

![-vZFToQsM5lThedIPc0op-1655887585313](https://user-images.githubusercontent.com/56382506/177708924-9630731e-8eaf-46c4-82e6-228598b8b921.gif)

#### Redux는 다음과 같은 순서로 상태를 관리합니다.

1. 상태가 변경되어야 하는 이벤트가 발생하면, 변경될 상태에 대한 정보가 담긴 <b>Action 객체</b>가 생성됩니다.  
2. 이 Action 객체는 Dispatch 함수의 인자로 전달됩니다.  
3. Dispatch 함수는 Action 객체를 Reducer 함수로 전달해줍니다.  
4. Reducer 함수는 Action 객체의 값을 확인하고, 그 값에 따라 전역 상태 저장소 Store의 상태를 변경합니다.  
5. 상태가 변경되면, React는 화면을 다시 렌더링 합니다.  

즉, Redux에서는 <b>Action → Dispatch → Reducer → Store순서</b>로 데이터가 단방향으로 흐르게 됩니다.

#### 액션(Action)

Action은 말 그대로 어떤 액션을 취할 것인지 정의해 놓은 <b>객체</b>

```javascript
// payload가 필요 없는 경우
{ type: 'INCREASE' }

// payload가 필요한 경우
{ type: 'SET_NUMBER', payload: 5 }
```
여기서 ```type``` 은 필수로 지정을 해 주어야 합니다. 해당 Action 객체가 어떤 동작을 하는지 명시해주는 역할을 하기 때문이며, 
대문자와 Snake Case로 작성합니다. 여기에 필요에 따라 ```payload``` 를 작성해 구체적인 값을 전달합니다.

#### 액션 생성함수(Action Creator)

액션 생성함수는 액션 객체를 만들어주는 함수이다. 화살표 함수로도 표현이 가능하다

```javascript
// payload가 필요 없는 경우
const increase = () => {
  return {
    type: 'INCREASE'
  }
}

// payload가 필요한 경우
const setNumber = (num) => {
  return {
    type: 'SET_NUMBER',
    payload: num
  }
}
```

#### Dispatch

Dispatch는 Reducer로 Action을 전달해주는 함수입니다. Dispatch의 전달인자로 Action 객체가 전달됩니다.

```javascript
// Action 객체를 직접 작성하는 경우
dispatch( { type: 'INCREASE' } );
dispatch( { type: 'SET_NUMBER', payload: 5 } );

// 액션 생성자(Action Creator)를 사용하는 경우
dispatch( increase() );
dispatch( setNumber(5) );
```
Action 객체를 전달받은 Dispatch 함수는 Reducer를 호출합니다.

#### Reducer

Reducer는 Dispatch에게서 전달받은 Action 객체의 type 값에 따라서 상태를 변경시키는 함수입니다.

```javascript
const count = 1

// Reducer를 생성할 때에는 초기 상태를 인자로 요구합니다.
const counterReducer = (state = count, action) {

  // Action 객체의 type 값에 따라 분기하는 switch 조건문입니다.
  switch (action.type)

    //action === 'INCREASE'일 경우
    case 'INCREASE':
			return state + 1

    // action === 'DECREASE'일 경우
    case 'DECREASE':
			return state - 1

    // action === 'SET_NUMBER'일 경우
    case 'SET_NUMBER':
			return action.payload

    // 해당 되는 경우가 없을 땐 기존 상태를 그대로 리턴
    default:
      return state;
}
// Reducer가 리턴하는 값이 새로운 상태가 됩니다.
```
이 때, Reducer는 <b>순수함수</b>여야 합니다. 외부 요인으로 인해 기대한 값이 아닌 엉뚱한 값으로 상태가 변경되는 일이 없어야하기 때문입니다.

만약 여러 개의 Reducer를 사용하는 경우, Redux의 ```combineReducers``` 메서드를 사용해서 하나의 Reducer로 합쳐줄 수 있습니다.

```javascript
import { combineReducers } from 'redux';

const rootReducer = combineReducers({
  counterReducer,
  anyReducer,
  ...
});
```

#### Store
Store는 상태가 관리되는 오직 하나뿐인 저장소의 역할을 합니다.

```javascript
import { createStore } from 'redux';

const store = createStore(rootReducer);
```

### Redux Hooks

Redux Hooks는 React에서 Redux를 사용할 때 활용할 수 있는 Hooks 메서드를 제공합니다. 

#### useSelector() 
```useSelector()```는 컴포넌트와 state를 연결하여 Redux의 state에 접근할 수 있게 해주는 메서드입니다.

```javascript
// Redux Hooks 메서드는 'redux'가 아니라 'react-redux'에서 불러옵니다.
import { useSelector } from 'react-redux'
const counter = useSelector(state => state.counterReducer)
console.log(counter) // 1
```

#### useDispatch()
useDispatch() 는 Action 객체를 Reducer로 전달해 주는 메서드입니다.

```javascript
import { useDispatch } from 'react-redux'

const dispatch = useDispatch()
dispatch( increase() )
console.log(counter) // 2

dispatch( setNumber(5) )
console.log(counter) // 5
```

### Redux의 세가지 원칙

#### 1. Single source of truth
동일한 데이터는 항상 같은 곳에서 가지고 와야 한다는 의미입니다. 즉, Redux에는 데이터를 저장하는 Store라는 단 하나뿐인 공간이 있음과 연결이 되는 원칙입니다.

#### 2. State is read-only
상태는 읽기 전용이라는 뜻으로, React에서 상태갱신함수로만 상태를 변경할 수 있었던 것처럼, Redux의 상태도 직접 변경할 수 없음을 의미합니다. 즉, Action 객체가 있어야만 상태를 변경할 수 있음과 연결되는 원칙입니다.

#### 3. Changes are made with pure functions
변경은 순수함수로만 가능하다는 뜻으로, 상태가 엉뚱한 값으로 변경되는 일이 없도록 순수함수로 작성되어야하는 Reducer와 연결되는 원칙입니다.
