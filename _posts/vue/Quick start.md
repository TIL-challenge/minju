## Vue Application 만들기

Vue Single Page Application을 만들어보자.

최신버전의 Node.js가 있는 컴퓨터에서 해당 명령어를 치기만 하면 된다.

```sh
npm create vue@latest
```

몇 가지 기능에 대해 질문을 하는데, 필요한 기능이 있다면 Yes를 체크하면 된다.
![](../../_assets/images/vue/Quick%20start/img-Quick%20start%201.png)

여기서 생성된 프로젝트는 `Vite`를 기반으로한 빌드 설정을 사용하고 Vue Single-File Components(SFCs) 를 사용한다.

## CDN에서 Vue 사용

다음 스크립트 태그를 통해 CDN에서 직접 Vue를 사용할 수 있다.

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

CDN에서 Vue를 사용하는 경우에는 빌드 단계가 필요하지 않다. 따라서 설정이 훨씬 간단해지고 정적 HTML을 향상시키거나 백엔드 프레임워크와 통합하는데 적합하다. 하지만 SFC구문은 사용할 수 없다는 단점이 있다.

위 링크를 사용하게 되면 Vue의 global build를 불러오게 된다. 이 빌드에서는 모든 최상위 API가 전역 `Vue`객체의 속성으로 노출된다.
