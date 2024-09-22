<h1> **3주차: Vue.js 기초**</h1>

Vue.js 소개 및 설치  
Vue CLI를 이용한 프로젝트 생성  
Vue 인스턴스, 데이터 바인딩  
컴포넌트, 템플릿  
디렉티브 (v-if, v-for, v-bind 등)  
실습: 간단한 Vue.js 애플리케이션 작성  



<h2> Vue.js 소개 및 설치 </h2>  

![alt text](image.png)

>>웹 사용자 인터페이스를 구축하기 위한 접근성, 성능, 다재다능함을 겸비한 프레임워크입니다.  


>>Vue(발음은 /vjuː/, view 와 유사 )는 사용자 인터페이스를 구축하기    
>>위한 JavaScript 프레임워크입니다. 표준 HTML, CSS, JavaScript를  
>>기반으로 구축되며, 모든 복잡성의 사용자 인터페이스를 효율적으로   
>>개발하는 데 도움이 되는 선언적 구성 요소 기반 프로그래밍 모델을
>>제공합니다.


>>단일 파일 구성 요소​
대부분의 빌드 도구 사용 Vue 프로젝트에서 우리는 Single-File Component*.vue ( 파일 이라고도 하며 SFC 로 약칭 )라는 HTML과 유사한 파일 형식을 사용하여 Vue 구성 요소를 작성합니다. 이름에서 알 수 있듯이 Vue SFC는 구성 요소의 로직(JavaScript), 템플릿(HTML), 스타일(CSS)을 단일 파일에 캡슐화합니다. 다음은 SFC 형식으로 작성된 이전 예입니다.  
  

```
// 스크립트 구문
<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>

// 보여지는 웹HTML 부분
<template>
  <button @click="count++">Count is: {{ count }}</button>
</template>

// CSS 스타일 구조를 보여주는 구문
<style scoped>
button {
  font-weight: bold;
}
</style>
```

<h3>설치</h3>  

![alt text](image-1.png)  

다운로드 Node.js. 다운로드 및 설치를 한다.  

설치를하고 CMD 창에서 node 를 치면  

![alt text](image-2.png)    

다음과 같이 노드에접속을 할수 있다.
이제 VUE를 설치를 해보자.

<h3>Vue 설치하기</h3>

```
npm install -g @vue/cli
// 인스톨

npm update -g @vue/cli
// 업데이트
```  

npm 이란?  
npm은 Node Packaged Manager의 약자입니다.  
말그대로 패캐지를 관리를 해주는 프로그램 입니다.



<h2> Vue CLI를 이용한 프로젝트 생성</h2>      

```  
vue create hello-world  

// 다음과같은 cmd 창에서 명령어를 확인한다.

```  
![alt text](image-3.png)

vue 2개 설치가 되어서 2개가 보인다.
vue3 을 선택을한다.

![alt text](image-4.png)

다음과 같은 설치가 완료되어서
맨마지막은 cd heellp-world  
폴더를 확인하고 이동을 한다.
npm run serve -> 실행시

![alt text](image-5.png)

정상적으로 주소를 볼수 있다.


![alt text](image-6.png)

브라우져 창에서 확인가능하다.
 ![alt text](image-7.png)



<h2> Vue 인스턴스, 데이터 바인딩</h2>    
  


<h3>Vue 인스턴스 </h3>

모든 Vue 앱은 Vue 함수로 새 Vue 인스턴스를 만드는 것부터 시작합니다.

```
var vm = new Vue({
  // 옵션
})
```

 MVVM 패턴과 관련이 없지만 Vue의 디자인은 부분적으로 그것에 영감을 받았습니다.  
 관례적으로, Vue 인스턴스를 참조하기 위해 종종 변수 vm(ViewModel의 약자)을 사용합니다.  

Vue 인스턴스를 생성할 때는 options 객체를 전달해야 합니다.   
이 가이드는 대부분 원하는 생성을 구현할 때 이런 옵션들을 사용하여 원하는 동작을   
구현하는 방법에 대해 다룹니다.   
전체 옵션 목록은 API reference에서 확인할 수 있습니다.

---
<h3>데이터 바인딩</h3>

데이터 바인딩을 하기위한 기본 약속  

```
v-bind:속성명="데이터 혹은 함수"
      :속성명="데이터 혹은 함수"


<div id="vue">
    <input v-bind:value="name">
</div>

<div id="vue">
     <input :value="name">
</div>
```

```  
<script >
// 데이터 바인딩
export default {
  name : 'App',
  data(){
    return{
      title: "노랑",
      year : 2019,
      category : "액션, 드라마",
      textRed : "color: red",

    }
  }
}
</script>

<template>
  영화정보
  <div>
    <h3 class="bg-yellow" :style="textRed">{{ title }}</h3>
    <p>개봉:{{year}}</p>
    <p>장르:{{category}}</p>
  </div>
</template>


<style scoped>
//스타일 클래스
.bg-yellow {
  background-color: gold;
  padding: 10px;
}

</style>
```




<h2> 컴포넌트, 템플릿</h2>    

<h3>컴포넌트</h3>
컴포넌트를 사용하면 UI를 독립적이고 재사용 가능한 일부분으로 분할하고 각 부분을 개별적으로 다룰 수 있습니다. 따라서 앱이 중첩된 컴포넌트의 트리로 구성되는 것은 일반적입니다  

![alt text](image-8.png)  

컴포넌트 정의

빌드 방식을 사용할 때 일반적으로 싱글 파일 컴포넌트(줄여서 SFC)라고 하는 .vue 확장자를 사용하는 전용 파일에 각 Vue 컴포넌트를 정의합니다  
```
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">당신은 {{ count }} 번 클릭했습니다.</button>
</template>
```

빌드 방식을 사용하지 않을 때, Vue 컴포넌트는 Vue 관련 옵션을 포함하는 일반 JavaScript 객체로 정의할 수 있습니다:
```
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)
    return { count }
  },
  template: `
    <button @click="count++">
      당신은 {{ count }} 번 클릭했습니다.
    </button>`
  // DOM 내의 템플릿을 대상으로 할 수도 있습니다:
  // template: '#my-template-element'
}
```  
---  


<h3>템플릿</h3>


<h4>텍스트 보간법</h4>  

데이터 바인딩의 가장 기본적인 형태는 "Mustache"(이중 중괄호) 문법을 사용한 텍스트 보간법입니다.
  

이중 중괄호 태그 내 msg는 해당 컴포넌트 인스턴스의 msg 속성의 값으로 대체됩니다. 또한 msg 속성이 변경될 때마다 업데이트됩니다.

```
<span>메세지: {{ msg }}</span>  
```
<h4>HTML 출력</h4>  
이중 중괄호는 데이터를 HTML이 아닌 일반 텍스트로 해석합니다. 실제 HTML을 출력하려면 v-html 디렉티브을 사용해야 합니다:


```
<p>텍스트 보간법 사용: {{ rawHtml }}</p>
<p>v-html 디렉티브 사용: <span v-html="rawHtml"></span></p>

```  
<h4>속성 바인딩</h4>  
이중 중괄호는 HTML 속성(attribute) 내에서 사용할 수 없습니다. 대신 v-bind 디렉티브를 사용하세요.  

v-bind 디렉티브는 엘리먼트의 id 속성을 컴포넌트의 dynamicId 속성과 동기화된 상태로 유지하도록 Vue에 지시합니다. 바인딩된 값이 null 또는 undefined이면 엘리먼트의 속성이 제거된 상태로 렌더링 됩니다.


```
<div v-bind:id="dynamicId"></div>

단축 문법
<div :id="dynamicId"></div>
```


---
<h2> 디렉티브 (v-if, v-for, v-bind 등)</h2>    

디렉티브란 v- 접두가사 있는 특수 속성
![alt text](image-14.png)

  
디렉티브(directives) : v- 접두사가 있는 특수 속성으로 디렉티브의 값(value)이 변경될 때 특정 효과를 반응적으로 DOM에 적용하는 것을 말한다. 
```
문서 객체 모델(The Document Object Model, 이하 DOM) 은 HTML, XML 문서의 프로그래밍 interface 이다.

DOM 은 프로그래밍 언어와 독립적으로 디자인되었다. 때문에 문서의 구조적인 표현은 단일 API 를 통해 이용가능하다.
``` 

전달인자(Argument) : 일부 디렉티브는 디렉티브명 뒤에 콜론(:)으로 표기되는 전달인자를 가질 수 있다. 예를 들어, v-bind 디렉티브는 반응적으로 HTML 속성을 갱신하는 데 사용한다.    

```
<a v-bind:href="url"> ... </a>

<!-- 단축 문법 -->
<a :href="url"> ... </a>
```

수식어(Modifiers) : 수식어는 점(.)으로 표시되는 특수 접미사로 디렉티브가 특별한 방식으로 바인딩되어야 함을 나타낸다.
```
<form @submit.prevent="onSubmit">...</form>
```



---  


v-text : string
텍스트 컨텐츠 업데이트
```
<span v-text="msg"></span>
<!-- 아래와 같음 -->
<span>{{msg}}</span>
```
 
v-html : string  
innerHTML을 업데이트합니다.
엘리먼트의 innerHTML을 업데이트합니다.
(특징 )
```
<div v-html="html"></div>
```  
보안 참고 사항
웹사이트에서 임의의 HTML을 동적으로 렌더링하는 것은 XSS 공격으로 쉽게 이어질 수 있기 때문에 매우 위험할 수 있습니다. 신뢰할 수 있는 컨텐츠에만 v-html을 사용하고, 사용자가 제공하는 컨텐츠에는 절대 사용하면 안됩니다.

v-show : any
```
<h1 v-show="ok">안녕!</h1>
```
차이점은 v-show가 있는 엘리먼트는 항상 렌더링되고 DOM에 남아 있다는 것입니다. v-show는 엘리먼트의 display CSS 속성만 전환합니다.


v-show는 `<template>` 엘리먼트를 지원하지 않으며 v-else와 상호작용하지 않습니다.
(엘리먼트는 CSS 기반으로 전환 되므로, 초기 조건과 관계없이 항상 렌더링 됩니다.  
)

v-if : any  

v-if 디렉티브는 조건부로 블록을 렌더링하는 데 사용됩니다. 블록은 디렉티브 표현식이 truthy 값을 반환하는 경우에만 렌더링됩니다.
```
<h1 v-if="awesome">Vue는 정말 멋지죠!</h1>
```  
--- 

v-else
```
<button @click="awesome = !awesome">전환</button>

<h1 v-if="awesome">Vue는 정말 멋지죠!</h1>
<h1 v-else>아닌가요? 😢</h1>
```
![alt text](image-10.png)  
![alt text](image-11.png)  
--- 
v-else-if  
v-else-if는 이름에서 알 수 있듯이 v-if에 대한 "else if 블록" 역할을 합니다. 여러 번 연결될 수도 있습니다:
```
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  A/B/C 아님
</div>
```
---  

v-for  
v-for 디렉티브를 사용하여 배열을 리스트로 렌더링할 수 있습니다. v-for 디렉티브는 item in items 형식의 특별한 문법이 필요합니다. 여기서 items는 배열이고, item(이하 아이템)은 배열 내 반복되는 앨리먼트의 `**별칭(alias)**`입니다.

```
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
``` 

```
<li v-for="item in items">
  {{ item.message }}
</li>
```  
v-for 범위 내 템플릿 표현식은 모든 상위 범위 속성에 접근할 수 있습니다. 또한 v-for는 현재 아이템의 인덱스를 가리키는 선택적 두 번째 별칭도 지원합니다.

```
const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])
```
```
<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>
```
![alt text](image-12.png)

---  

v-on
엘리먼트에 이벤트 리스너를 연결합니다.


```
.stop - event.stopPropagation() 호출.
.prevent - event.preventDefault() 호출.
.capture - 캡처 모드로 이벤트 등록.
.self - 이벤트가 이 엘리먼트에서 전달된 경우에만 트리거 됨.
.{keyAlias} - 이벤트가 특정 키에 대해서만 트리거 됨.
.once - 이벤트가 한 번만 트리거 됨(일회용처럼).
.left - 마우스 왼쪽 버튼으로만 이벤트가 트리거 됨.
.right - 마우스 오른쪽 버튼으로만 이벤트가 트리거 됨.
.middle - 마우스 중앙(힐 클릭) 버튼으로만 이벤트가 트리거 됨.
.passive - { passive: true } 옵션으로 DOM 이벤트를 등록.
```
예제
```
<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <button @click="count++">1 추가</button>
  <p>숫자 값은: {{ count }}</p>
</template>
```  
![alt text](image-13.png)

---  

v-bind
하나 이상의 속성 또는 컴포넌트 prop을 표현식에 동적으로 바인딩합니다.

```
.camel - kebab-case 속성 이름을 camelCase로 변환.
.prop - 바인딩을 DOM 속성(property: 이하 프로퍼티)으로 강제 설정. 3.2+
.attr - 바인딩을 DOM 속성(attribute)으로 강제 설정. 3.2+
```  

  
```  
<!-- 속성 바인딩 -->
<img v-bind:src="imageSrc" />

<!-- 동적인 속성명 -->
<button v-bind:[key]="value"></button>

<!-- 단축 문법 -->
<img :src="imageSrc" />

<!-- 같은 이름 생략 가능 (3.4+), 오른쪽과 같음 :src="src" -->
<img :src />

<!-- 단축 문법과 동적 속성명 -->
<button :[key]="value"></button>

<!-- 인라인으로 문자열 결합 -->
<img :src="'/path/to/images/' + fileName" />

<!-- class 바인딩 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]"></div>

<!-- style 바인딩 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>

<!-- 속성을 객체로 바인딩 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>

<!-- prop 바인딩. "prop"은 자식 컴포넌트에서 선언되어 있어야 함 -->
<MyComponent :prop="someThing" />

<!-- 자식 컴포넌트와 공유될 부모 props를 전달 -->
<MyComponent v-bind="$props" />

<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>

```  


---



<h2> 실습: 간단한 Vue.js 애플리케이션 작성</h2>  


  
  
<h2>퍼미션 에러</h2>  

<h2>$ net stop winnat / net start winnat </h2>
