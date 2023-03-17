
https://github.com/reduxjs/redux-thunk

The word "thunk" is a programming term that means ["a piece of code that does some delayed work"](https://en.wikipedia.org/wiki/Thunk).


Thunk [middleware](https://redux.js.org/tutorials/fundamentals/part-4-store#middleware) for Redux. 
It allows writing functions with logic inside that can interact with a Redux store's `dispatch` and `getState` methods

Using thunks requires the [`redux-thunk` middleware](https://github.com/reduxjs/redux-thunk) to be added to the Redux store as part of its configuration.

---------------

기본적으로 
store.dispatch는 action을 인자로 받는다.
이때 action는 plain js object로
{
	type: 'blahblah'
	data: data
}
이런 형태이다.
=> 즉 리덕스는 객체 타입의 액션을 받아 dispatch를 통해 store로 보내지고 store 내부에서
reducer를 통해 state를 업데이트 한다.

액션을 객체가 아닌 객체를 리턴하는 `함수`를 줄 순 없을까?
비동기 api , 비동기 함수를 통해 데이터를 받고 그 결과를 비동기적으로 dispatch하고 싶다!

이런 생각?(요구)들이 있어서 store를 생성할 때 미들웨어를 적용할 수 있다.

미들웨어 적용방법은 https://github.com/reduxjs/redux-thunk 참고


thunkMiddleware의 로직은 다음과 같다.

```js

// standard middleware definition, with 3 nested functions:  
// 1) Accepts `{dispatch, getState}`  
// 2) Accepts `next`  
// 3) Accepts `action`  
const thunkMiddleware =  
({ dispatch, getState }) =>  
next =>  
action => {  
// If the "action" is actually a function instead...  
if (typeof action === 'function') {  
// then call the function and pass `dispatch` and `getState` as arguments  
return action(dispatch, getState)  
}  
  
// Otherwise, it's a normal action - send it onwards  
return next(action)  
}



```

1. 가장 바깥 함수가 store api를 받음 보통 (dispatch, getState)
2. action이 객체면 기존 dispatch가 하는것 처럼 next(action)을 하고
3. 액션이 함수이면 dispatch와 getState함수를 넘겨주고 그 함수에서 서비스 로직이 돌고 dispatch를 한다.

여길 보면 자세히 알 수 있다.
[Redux middleware are all written as a series of 3 nested functions](https://redux.js.org/tutorials/fundamentals/part-4-store#writing-custom-middleware):


--------------

thunk역할을 하는 함수에서는 dispatch와 getState를 받아
내부에서 비동기 로직을 처리하고
그 결과를 바탕으로
액션을 만들어 dispatch(createdAction)을 넘겨주면 상태가 업데이트 됨!
