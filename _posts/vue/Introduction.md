## What is Vue?

Vue는 유저 인터페이스를 빌드 하기 위한 자바스크립트 `프레임워크`이다. Vue는 다음 핵심 기능을 내포하고 있다.

- 선언적 렌더링(Declarative Rendering): Vue는 표준 HTML을 템플릿 문법으로 확장하여 JavaScript 상태를 기반으로 화면에 출력될 HTML을 [선언적(declaratively)](../etc/선언적(%20프로그래밍.md)으로 작성할 수 있습니다.
- 반응성(Reactivity): Vue는 JavaScript의 상태 변경을 추적하고, 변경이 발생하면 DOM을 자동으로 효율적으로 업데이트 한다.

## The Progressive Framework

Vue는 프론트엔드 개발에 필요한 대부분의 공통 기능을 다루는 프레임워크이다. 하지만 웹은 매우 다양하고 구축하려는 형태나 규모가 크게 다를 수 있다. Vue는 이를 염두에 두고 유연하고 점진적으로 채택할 수 있도록 설계돼있다.

- 빌드 없이 정적 HTML에 적용
- 모든 페이지에 웹 컴포넌트로 추가
- 싱글 페이지 어플리케이션
- Fullstack/ Server-Side-Rendering
- Jamstack/ Static-Site-Generation

어떤 환경에서 Vue를 적용하든, Vue의 핵심 기능들은 위의 모든 사례에서 공유되어 같은 생산성을 가질 수 있다. 이러한 이유로 Vue를 Progressive Framework라고 부른다.

## Single-File Component

빌드 도구를 사용하는 대부분의 Vue 프로젝트에서는 HTML과 유사한 싱글 파일 컴포넌트(Single-File Component: SFC, `*.vue` 파일)라는 파일 형식을 사용하여 Vue 컴포넌트를 작성한다. Vue SFC는 컴포넌트의 로직(JavaScript), 템플릿(HTML) 및 스타일(CSS)을 하나의 파일에 캡슐화 한다.

```vue
<script setup>
import { ref } from 'vue' const count = ref(0)
</script>

<template>
	<button @click="count++">Count is: {{ count }}</button>
</template>

<style scoped>
button { font-weight: bold; }
</style>
```

## API Style

Vue 컴포넌트는 Options API와 Composition API 두 가지 스타일로 작성할 수 있다.

### Option API

Option API는 Option의 `data`, `methods` 및 `mounted` 같은 객체를 사용하여 컴포넌트의 로직을 정의한다. Option으로 정의된 속성은 컴포넌트 인스턴스를 가리키는 함수 내부의 `this`에 노출된다.

```vue
<script>
export default {
	// data()에서 반환된 속성들은 반응적인 상태가 되어
	// `this`에 노출됩니다.
	data() {
		return {
			count: 0,
		};
	},

	// methods는 속성 값을 변경하고 업데이트 할 수 있는 함수.
	// 템플릿 내에서 이벤트 헨들러로 바인딩 될 수 있음.
	methods: {
		increment() {
			this.count++;
		},
	},

	// 생명주기 훅(Lifecycle hooks)은 컴포넌트 생명주기의
	// 여러 단계에서 호출됩니다.
	// 이 함수는 컴포넌트가 마운트 된 후 호출됩니다.
	mounted() {
		console.log(`숫자 세기의 초기값은 ${this.count} 입니다.`);
	},
};
</script>

<template>
	<button @click="increment">숫자 세기: {{ count }}</button>
</template>
```

### Composition API

Composition API를 사용하는 경우, `import`해서 가져온 API 함수들을 사용하여 컴포넌트의 로직을 정의한다. SFC에서 Composition API는 일반적으로 `<script setup>` 과 함께 사용된다. `setup`속성은 컴포넌트의 script 부분을 더 간결하게 작성할 수 있게 한다. `<script setup>` 구문은 컴포넌트의 기본 설정을 미리 컴파일 단계에서 처리한다. 따라서 `<script setup>`에 `import` 되어 가져온 객체들과 선언된 최상위 변수 및 함수는 템플릿에서 직접 사용할 수 있다.

```vue
<script setup>
import { ref, onMounted } from "vue";

// 반응적인 상태의 속성
const count = ref(0);

// 속성 값을 변경하고 업데이트 할 수 있는 함수.
function increment() {
	count.value++;
}

// 생명 주기 훅
onMounted(() => {
	console.log(`숫자 세기의 초기값은 ${count.value} 입니다.`);
});
</script>

<template>
	<button @click="increment">숫자 세기: {{ count }}</button>
</template>
```

### 선택
