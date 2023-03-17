
리액트와 함께 리덕스를 사용하기 위해서 필요한 것들은 react-redux 라이브러리에 있음

**Provider**

-   컴포넌트에 store가 저장된 context를 제공

  
connect()(SomeComponent)

-   SomeComponent를 인자로 받아 Connect Component로 Wrapping하여 리턴
-   wrapping을 통해 SomeComponent는 Props를 받게을 수 있음
-   이때 props로 state, dispatcher 등을 받을 수 있음


**bindActionCreators**(someActionCreator, dispatch)
-   actionCreator와 dispatch를 바인드 해줌

**connect(mapStateToProps, mapDispatchToProps)(SomeComponent)**

```js

const mapStateToProps = (state) => {
	return{
		count: state
	}
}

//increment, decrement -> actionCreator
const mapDispatchToProps = (dispatch) => {

	return {
		increment: bindActionCreators(increment, dispatch),
		decrement: bindActionCreators(decrement, dispatch),
	}

}

connect(mapStateToProps, mapDispatchToProps)(SomeComponent)
//SomeComponent에서 Props로 state와 dispatch를 받을 수 있다.

```


리덕스를 사용하면
비지니스 로직이 reducer, actionCreator를 정의한 곳으로 빠지게 되며
React는 Props를 전달받거나 state를 가져와 View에 렌더링만 하면 되기 때문에
컴포넌트 자체는 깔끔해 질 수 있다.

ducks패턴 
reducer와 actionCreator를 같은 파일에 정의


리덕스를 사용할 때 생각 흐름

1. 어떤 상태를 store에 저장하고 관리할 것 인가?
2. 어떤 액션이 필요한가? -> action 정의
3. 해당 액션을 위한 actionCreator 정의
4. state와 action을 인자로 받는 reducer 정의

리액트와 리덕스

1. 리덕스를 사용하여 어떤 state를 store에 관리할것인가?
2. state, action, actionCreator, reducer 만들기
3. 컴포넌트에 Props로 넣어주기 (connect)
4. getState() 로 상태값 가져오기
5. dispatch() 로 상태값 업데이트


