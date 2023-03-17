
## Core Concepts and Principles
https://redux.js.org/understanding/thinking-in-redux/three-principles

- ### Single Source of Truth
- ### State is Read-Only
- ### Changes are Made with Reducer Functions


---


## 장점
- 단일 출처로 예측하기 쉬운 시스템
- SSR 가능
- Debugging 용이 Chrome extention Redux-DevTools 

## 주요 구성
- action, actionCreator
- reducer
- store

### action
- a plain JS object that has a type field.

### actionCreator
-   action을 반환하는 함수, 즉 action을 서비스 로직에 맞게 만들어 반환

### store
-   state 를 저장하는 컨테이너 개념
-   redux에서 제공하는 createStore를 통해 생성가능
-  getState(), dispatch() 제공
-   createStore(reducer)

### selectors

state에서 원하는 value를 추출하기 위함 함수

```js
const selectCounterValue = state => state.value

const curValue = selectCountValue(store.getState())
```

[React with Redux](React%20with%20Redux.md)

[Redux Tool Kit](Redux%20Tool%20Kit.md)

[Redux with Async (redux-thunk)](Redux%20with%20Async%20(redux-thunk).md)
