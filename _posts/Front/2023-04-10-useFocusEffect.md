---
title: "UseFocusEffect과 라이플사이클"

categories:
  - Frontend
tags:
  - [Frontend]

toc: true
toc_sticky: true
---

​    

# useFocusEffect???

- UseFocusEffect는 React Native에서 존재하는 Hook이다.
  이 친구의 특징은 특정화면(Screen)에 포커스가 일어났을때 실행이 되는 친구이다.
  React Native 공식문서에서는 useCallback()과 같이 사용하라고 나온다.

```typescript
useFocusEffect(
  useCallback(() => {
    if (UI.SelectEventId !== 0) getEventData(); // data를 가져오는 메서드
    if (UI.SelectEventId === 0) navigation.navigate("Home");
    return () => {
      dispatch(EventSlice.actions.deleteEvent);
    };
  }, [])
);
```

- React Native에서는 이렇게 useFocusEffect는 네트워크를 통해 데이터를 가져와야할때 사용하는걸 권장한다고 한다.
- 그 이유에대해서 많은 생각을 해보았는데... 내가 생각하기에 Focus가 일어났다는거는 새로운 Screen일 생성하는 이벤트가 생겼기 때문에 사전에 데이터를 셋팅하기위해 APIServer에 요청을 한 후 데이터를 가져와야하기 때문인 것 같다. 그리고 사실 useEffect하나만으로도 가능하다!

​    

# useFocusEffect가 실행되는 시점

1. Render가 실행이 되기전?
2. Render가 실행이 된 후?

- 정답은 2번이다. React에서 라이프 사이클을 보면 Hook은 Render가 실행이 된후 실행이 된다고 나와있다. 이 부분은 React Native도 동일하게 돌아간다고 볼 수 있다.

그렇다면 나는 여기서 무슨 문제점을 겪었느냐....?

​    

# 뭐가 문제일까?

내가 원하는 플로우는 Render전에 필요한 데이터를 셋팅 후 Render된다고 생각하고 무작정 useFocusEffect와 다른 CallBack함수들로 async await으로 프로미스로 만들고 여러가지 조치를 취했는데도 참조하고 있는 store가 undefined 라고 에러가 나오고 있엇다..
이부분을 나는 어떻게 해결했을까?

```typescript
<View style={{ flex: 1, backgroundColor: "white" }}>
      {event.IsLoading === true ? (
        <Loading />
      ) : (
```

실제로 Slice에 isLoading이라는 상태를 만들어두고 다 셋팅이 완료가 되면 false로 값을 업데이트하게 만들어두었다. 실제로 isLoading이라는 상태는 store에 있기때문에 APIServer에서 받은 데이터들을 store에 셋팅이 완료가 되면 isLoading을 false로 바꾸기 때문에 셋팅이 완료되고 삼항연산자로 false로 바꾸면서 하위컴포넌트를 Render하기 때문에 undefined를 참조하는 문제는 해결할 수 있었다.

<br>

    개인 공부 기록용 블로그입니다.
    잘못된 내용이 있다면 꼭 알려주세요!

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
