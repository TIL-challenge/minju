## 앱 인스턴스

모든 Vue 앱은 `createApp` 함수를 사용하여 새로운 앱 인스턴스를 생성하는 것으로 시작한다.

```js
import { createApp } from "vue";

const app = createApp({
	/* 최상위 컴포넌트 옵션 */
});
```

## 최상위 컴포넌트

`createApp`에 전달하는 객체는 컴포넌트이다. 모든 앱에는 다른 컴포넌트를 자식으로 포함하는 *최상위 컴포넌트*가 있는데, 이 최상위 컴포넌트를 전달하면 된다. 아래 예를 통해 살펴보자.

하나의 Vue 앱에는 여러 컴포넌트들이 있는데, 계층구조로 되어있어 수 많은 부모 컴포넌트와 자식 컴포넌트로 이루어져 있다.

```
App (최상위 컴포넌트)
├─ TodoList
│  └─ TodoItem
│     ├─ TodoDeleteButton
│     └─ TodoEditButton
└─ TodoFooter
   ├─ TodoClearButton
   └─ TodoStatistics
```

이런 컴포넌트를 가진 앱은 `createApp` 에 최상위 컴포넌트(App)를 넘겨주면된다.

싱글 파일 컴포넌트를 사용하는 경우에는 다른 파일에서 루트 컴포넌트를 가져온다.

```js
import { createApp } from "vue"; // 싱글 파일 컴포넌트에서 최상위 컴포넌트 앱을 가져옵니다.

import App from "./App.vue";

const app = createApp(App);
```

## 앱 마운트하기

앱 인스턴스는 `.mount()`메서드가 호출될 때까지 아무 것도 렌더링 하지 않는다. *컨테이너*가 될 실제 DOM 엘리먼트 또는 셀렉터 문자열을 인자로 넣어줘야 한다.

```html
<div id="app"></div>
```

```js
app.mount("#app");
```

앱의 최상위 컴포넌트 컨텐츠는 컨테이너 엘리먼트 내에서 렌더링된다. <span style="background:#ff4d4f">컨테이너 엘리먼트 자체는 앱의 일부로 간주되지 않는다.</span>

`.mount()`메서드는 반드시 앱의 환경설정 및 asset이 모두 등록 완료된 후에 호출되야 하고 최상위 컴포넌트 인스턴스(!= 앱 인스턴스)를 반환한다.

### DOM 내부의 최상위 컴포넌트 템플릿

빌드 과정 없이 Vue를 사용할 때, 마운트 컨테이너 내부에 직접 최상위 컴포넌트의 템플릿을 작성할 수 있다.

```html
<div id="app">
	<button @click="count++">{{ count }}</button>
</div>
```

```js
import { createApp } from "vue";

const app = createApp({
	data() {
		return {
			count: 0,
		};
	},
});

app.mount("#app");
```

최상위 컴포넌트에 아직 `template` 옵션이 없으면 Vue는 자동으로 컨테이너의 `innerHTML` 을 템플릿으로 사용한다.

## 앱 환경설정

앱 인스턴스는 몇 가지 앱 레벨의 옵션을 구성할 수 있는 `.config` 객체를 노출한다. 예를 들어 모든 자식 컴포넌트에서 에러를 캡처하는 앱 레벨의 에러 핸들러를 정의할 수 있다.

```js
app.config.errorHandler = (err) => {
	/* 에러 처리 */
};
```

앱 인스턴스는 앱 범위의 에셋을 등록하기 위한 몇 가지 방법도 제공한다. 예를 들어 컴포넌트를 전역으로 등록할 수 있다.

```js
app.component("TodoDeleteButton", TodoDeleteButton);
```

### 멀티 앱 인스턴스

앱 인스턴스는 동일한 페이지 내 하나로 제한되지 않는다. `createApp` 을 사용해서 여러 Vue 앱이 동일한 페이지에 공존할 수 있고, 각각은 구성 및 전역 resource에 대한 고유한 범위를 갖는다.

```js
const app1 = createApp({
	/* ... */
});
app1.mount("#container-1");

const app2 = createApp({
	/* ... */
});
app2.mount("#container-2");
```

서버에서 렌더링 된 대규모 페이지의 HTML을 개선하고 특정 부분을 제어하기 위해 Vue가 필요한 경우, 페이지 전체를 단일 Vue 앱 인스턴스로 마운트하기 보다는, 여러 개의 작은 앱 인스턴스를 만들고 담당하는 엘리먼트에 마운트 하는 것이 좋다.
