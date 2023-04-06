---
title: "Props Drilling에 관한 고민"

categories:
  - Moim
  - Frontend
tags:
  - [Project, ReactNative]

toc: true
toc_sticky: true
---

## Props는?

- React에서 제공하는 Hook으로서 Component안에서 상태를 관리할 수 있게 제공하는 Hook이다.

```typescript
const [isLoading, setIsLoading] = useState(false);
```

위에 코드처럼 간단하게 사용할 수 있는 Hook이다.

IsLoading이라는 state를 component안에서 관리함으로써 해당 Component에서 사용할 수 있다.
하지만 하위 Component에게도 props(파라미터)로 넘겨줄 수 있는데, 하위 컴포넌트에게 넘겨야할 props가 1~2개정도라고 하면 타이핑도 적고 문제가 없다고 생각한다.

But... 만약 넘겨야하는게 10~20개 정도라면? 하위 Component 또 하위 Component 있고, 그 안에 또 하위Component 가 있다면?

## Props Drilling?

많은 하위 Component 에게 props 로 전해주는 행위를 보고 Props Drilling이라는 행위라고 한다.

무조건 나쁜 행위라고는 단정짖기 어렵지만, 나의 경우엔 PostScreen을 제작을 하면서 "유저"에게 받아야 하는 내용이 많았다.

Title, Dscription, images, date, map(tradeName, Address, longitued, latitude,), OpenTalkLink 등 최상위 Component에서 이 많은 정보들을 가지고 있어야 햇다.

물론 각각의 하위 Component에서 관리를 할 수 있지만, 우리 프로젝트에서는 Submit 버튼이 눌렀을때, APIServer에 데이터를 저장해달라고 POST요청을 해야했기에 다른 Component로 모든 State를 보내줘야하는 상황이였다.

이렇게 되니... 코드도 더럽고, 너무 길어지고, 단점이 많았다.

이 문제를 해결하기 위해 처음에 잘 몰랐기 때문에 쓸 엄두가 안났었던 Redux라는걸 정복해보자 하고 마음을 먹고 만 이틀을 Redux를 해딩해가면서 정복해가기 시작한다.

## Redux?

Redux는 전역상태관리라고 한다.

전역상태관리?????

예전부터 42Seoul에서 프로젝트를 할때마다 struct table을 만들어서 프로세스 전역에서 사용하는 데이터들을 저장하는 table을 만들어서 사용을 했었다.
나한텐 그런 친구들처럼 느껴졌다.

그렇지만 이번 프로젝트를 하면서 처음 해보는 Redux를 어떻게 사용하는걸까?

```typescript
interface event {
  eventId: number;
  eventTitle: string;
  eventimages: string[];
}
```

이런 타입들도 만들어줘야하고... reducer, action등을 만들어줘야하는데, 너무너무 어려웠다.....

하지만 Redux에서 update가 되면서 나온 Slice라는걸 알게 됬다.

## Slice?

여러 Slice가 모여 store가 완성이 된다고 볼 수 있는데, 여기서 Slice는 Reducer이면서 동시에 type도 지정해줄 수 있다고 볼수 있다.

그 동안에 Redux는 type, reducer, action등을 나눠서 만들어야 했다면, Slice는 이 하나에서 모든걸 해볼 수 있다.

```typescript
import { createSlice, PayloadAction } from "@reduxjs/toolkit";

export interface summaryEvent {
  eventId: number;
  eventMainImage: string;
  eventTitle: string;
  eventLocation: string;
}

const initialState = {
  hashtagId: [1, 2, 3, 4, 5, 6, 7, 8],
  summaryEvents: [] as summaryEvent[],
  isLoading: true,
};

export const HomeSlice = createSlice({
  name: "Home",
  initialState: initialState,
  reducers: {
    addSummaryEvent(state, action: PayloadAction<summaryEvent>) {
      state.summaryEvents = [...state.summaryEvents, action.payload];
    },
    setLoading(state, action: PayloadAction<boolean>) {
      state.isLoading = action.payload;
    },
    deleteAll(state) {
      state = initialState;
      return state;
    },
  },
});
```

위에 코드는 Moim 프로젝트에서 실제로 HomeScreen에서 사용중인 HomeSlice이다.

코드를 하나하나 설명해보자면

- initialState

  이부분은 homeSlice에 관해 초기화를 담당하고 있다고 볼 수 있다. Redux에서 Type들을 지정해주던걸 initialState로 Redux가 type을 만들어준다고 볼 수 있다.

- name: "Home",

  이건 이 slice의 alias을 말하며

- reducers

  Slice에서 실제 dispatch로 실행할 action 함수들을 정의하는 곳이다.

Slice들을 사용하는 방법은 다른 곳에서 포스팅을 하겠다.

그래서 나는 이 프로젝트에서 어떻게 사용했나??

Slice들을 만들고 사용하면서 실제로 Component안에서 사용하는 State들을 initialState로 만들어두고 Component에서는 행위가 일어날때마다 dispatch로 store에 update를 해주면서 데이터들을 저장하고 최종 submit에서 slice에서 가지고 있는 state를 APIServer에 보내는 로직으로 처리했다.

```typescript
return (
  <View
    style={{
      backgroundColor: "white",
    }}
  >
    <PostHeader />
    <KeyboardAvoidingView
      behavior={Platform.OS === "ios" ? "padding" : "height"}
      keyboardVerticalOffset={Platform.OS === "ios" ? 64 : hp * 0.07}
    >
      <ScrollView
        contentContainerStyle={{
          paddingBottom: hp * 0.3,
          paddingTop: hp * 0.08,
          flexGrow: 1,
        }}
      >
        <View style={StylePost.container}>
          <View style={{ alignItems: "center" }}>
            <Text style={{ fontSize: 28, fontWeight: "bold" }}>
              이벤트 작성하기
            </Text>
            <View
              style={{
                flexDirection: "row",
              }}
            >
              <Text style={{ fontSize: 12 }}>(</Text>
              <Octicons
                name="check"
                size={15}
                color="red"
                style={{ paddingHorizontal: 4 }}
              />
              <Text style={{ fontSize: 12 }}> 필수항목)</Text>
            </View>
          </View>
          <PostTitleInput />
          <Spacer size={hp * 0.05} />
          <PostDescriptionInput />
          <Spacer size={hp * 0.05} />
          <View
            style={{
              width: wp * 0.9,
            }}
          >
            <ImagePickerComponent />
          </View>
          <Spacer size={hp * 0.07} />
          <View>
            <PostMaxParticipantInput />
          </View>
          <Spacer size={hp * 0.07} />
          <PostTitle postTitle="이벤트 해시태그 선택" isCheck={true} />
          <HashtagList />
          <Spacer size={hp * 0.07} />
          <PostTitle postTitle="이벤트 날짜 선택" isCheck={true} />
          <PostCalender />
          <Spacer size={hp * 0.07} />
          <View>
            <PostTitle postTitle="이벤트 장소 선택" isCheck={true} />
            <Spacer size={hp * 0.01} />
            <MapScreen />
          </View>
          <Spacer size={hp * 0.1} />
          <PostOpenTalkInput />
        </View>
        <Spacer size={hp * 0.05} />
      </ScrollView>
    </KeyboardAvoidingView>
  </View>
);
```

위에 코드는 실제 Moim 프로젝트에서 사용하고 있는 PostScreen에 대한 TSX문이다.

실제로 하위 컴포넌트도 많고, 사용자에게 받는 데이터들의 종류도 많다. 만약 내가 Redux를 쓸 생각을 안했다면, 저정도로 끝나진 않았겟지...? 더 길고... 더 더럽게 보이고.. 그러겠지...?

최종적으로 "PostHeader"

곳에 Submit button이 존재하고, 여기서 "유저"가 Submit Button을 누르면 PostEventSlice에 저장되어 있는 정보를 APIServer에 POST요청을 하게 된다.

## 이렇게 Redux를 사용하면 뭐가 좋을까?

1. 반복된 코드의 양을 줄일 수 있다.
2. 상위 또는 전혀 다른 Component에게도 현재의 state를 공유할 수 있다.

- 그렇다면 단점은??

1. 다른 개발자가 잘못된 데이터를 던져줄 수 있다.
   이 부분은 사실 전역이라는 상태에 대한 문제점인 것 같다.
2. 초보자라면 비동기에 대한 이해가 어렵다.

---

<br>

    개인 공부 기록용 블로그입니다.
    잘못된 내용이 있다면 꼭 알려주세요!

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
