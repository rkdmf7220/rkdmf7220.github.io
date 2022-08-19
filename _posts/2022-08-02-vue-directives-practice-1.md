---
layout: post
title: vue.js 공부
subtitle: v-bind, v-on, v-for, props, emit
categories: vue.js
tags: [vue.js, practice]
---

## 데이터 바인딩(Data-Binding)이란?
바인딩이란 **묶는다**는 의미로, 웹 프로그래밍에선 UI를 통해 **보여주고자 하는 데이터**와 **실제 데이터**를 **연결**해 주는 것을 의미합니다.

즉, 사용자가 input에 입력한 값을 바로 데이터로 가져와 일치시키는 것이 데이터 바인딩이며,\
제이쿼리 처럼 event를 통해 가져오는 경우를 **단방향 바인딩**, 사용자의 입력 값이 바로 코드 상의 변수에 담기는 것을 **양방향 바인딩**이라고 합니다.

![데이터 바인딩 방식]({{ site.url }}/assets/images/posts/vuejs/vue-directives-practice-1/data-binding.png)

[출처 - https://authorkim0921.tistory.com/13](https://authorkim0921.tistory.com/13)

## v-model이란?

**폼 입력 바인딩**. input 태그와 textarea 엘리먼트에 양방향 데이터 바인딩을 생성합니다.
- text, textarea - value 속성과 input 이벤트를 사용합니다.
- checkbox, radio - checked 속성과 change 이벤트를 사용합니다.
- select(dropbox) - value를 props로,change 이벤트를 사용합니다. 

>'v-model'은 모든 form 요소의 초기 value, checked, selected를 무시하고 vue 데이터를 원본 소스로 취급합니다.
그래서, 컴포넌트의 'data' 옵션 안에 있는 js에서 초기값을 선언해야 합니다.

v-model의 동작 방식은 v-bind와 v-on의 기능 조합으로 동작합니다.\
매번 일일이 v-bind와 v-on 속성을 지정하지 않아도 작동 하도록 고안된 문법입니다.

```Practice.vue(양방향)
<template>
  <input type="text" v-model="inputText">
</template>

<script>
export default {
  data() {
    return {
      inputText: ''
    }
  }
}
</script>
```

```Practice.vue(단방향)
<template>
  <input type="text" v-bind="inputText"  v-on="updateInput">
</template>

<script>
export default {
  data() {
    return {
      inputText: ''
    }
  },
  methods: {
    updateInput(event) {
      let updatedText = event.target.value;
      this.inputText - updatedText; 
    }
  }
}
```

## v-on이란?
**이벤트 핸들링** 할 때 사용하는 디렉티브 입니다. 이를 사용해 간단한 이벤트나 methods의 함수를 호출 할 수 있습니다./
v-on 뒤에 :트리거 형식으로 작성하여 설정합니다. → v-on:click="onClickEvent"
click 뿐만 아니라 keyup, change 등 다양한 트리거를 지원하고 있습니다.

트리거 뒤에 .수식어 형식으로 **이벤트 수식어**를 추가할 수 있습니다. → v-on:click.once="onClickEvent"/
stop(이벤트가 중단됩니다), once(이벤트가 딱 한번만 일어납니다), self(이벤트 대상이 자신일때만 실행합니다) 등의 여러 수식어가 있습니다.

v-on은 **@**로 축약하여 작성할 수 있습니다. → @click="onClickEvent"

## v-for이란?
**리스트 렌더링**. 엘리먼트에 배열을 연결할 때 사용하며, 지정한 배열을 반복문 형식으로 리스트를 렌더링합니다.
v-for="item in items" 형식의 문법으로 작성하며, **item**은 이 반복되는 배열 엘리먼트의 **별칭**이며, **items**는 **원본 데이터의 배열**입니다.

```Practice.vue
<template>
  <ul>
    <li v-for="itemData in myList" :key="itemData.id">
  </ul>
</template>

<script>
export default {
  data() {
    return {
      myData: [
        {
          "id": "A",
          "name": "alpha"
        },
        {
          "id": "B",
          "name": "bravo"
        },
        {
          "id": "C",
          "name": "charlie"
        }
      ]
    }
  }
}
</script>
```
위 코드를 분석해보면
1. myData 배열을 기반으로 삼습니다.
2. 배열 안의 값을 itemData라는 이름으로 가져옵니다.
3. 마지막으로, key에 고유한 값을 동적으로 넣어줍니다. 여기선 요소 안의 id를 키로 잡았습니다.

### key를 넣는 이유는?
배열의 속성을 지정하거나 길이를 수정하는 등의 변화를 vue가 감지하지 못하는 경우도 있고,\
컴포넌트는 자체 범위가 분리되어 있어 데이터가 변경되어도 자동으로 전달되지 않습니다.

이럴 때 key를 지정해주면 데이터의 변경을 감지하고 재렌더링을 진행할 수 있습니다.

**※ vue3부터는 :key가 필수가 되었으며, 누락될 경우 에러를 띄우며 페이지가 로딩되지 않습니다.**

## vue 컴포넌트간의 데이터를 주고받기
vue는 컴포넌트를 이용해 화면을 구성하고 각 컴포넌트마다 고유한 범위를 가지고 있습니다.\
때문에, 같은 웹 페이지 안이라고 해도 컴포넌트가 다르면 그 데이터를 직접적으로 참조할 수 없습니다.

이를 해결하기 위해 컴포넌트 통신 방법인 **props**와 **emit**을 사용해야 합니다.\
props는 **부모**에서 **자식**으로 **props**라는 속성으로 전달하며,\
emit은 **자식**에서 **부모**로 **이벤트**를 전달합니다.

### props로 자식에게 데이터 전달
기본 작성 방식은 부모 컴포넌트에서 **v-bind**를 이용해 **프룹스 명**을 지정하고 데이터를 내려줍니다.\
`<child-component v-bind:프룹스 속성 명="현재(부모) 컴포넌트의 데이터 속성 명"/>`\
자식 컴포넌트에선 props에서 내려준 **속성 명**에 **형**을 **지정**해주면 됩니다.\
`props: {프룹스 속성 명: 데이터의 형}`\
**※ v-bind는 :로 축약시켜 쓸 수 있습니다.**


```ParentComponent.vue
<template>
  <div>
    <child-component :item-data="myData"/>
  </div>
</template>

<script>
export default {
  data() {
    return {
      myData: [
        {
          "id": "A",
          "name": "alpha"
        },
        {
          "id": "B",
          "name": "bravo"
        },
        {
          "id": "C",
          "name": "charlie"
        }
      ]
    }
  }
}
</script>
```
```ChildComponent.vue
<template>
  <div> ｛{ itemData }} </div>
</template>

<script>
export default {
  props: {
    itemData: Object
  }
}
</script>
```

### emit으로 부모에게 데이터 전달
emit은 이벤트에 인자를 담아 부모 컴포넌트에게 전달하며, 이것을 부모 컴포넌트의 해당 이벤트에서 매개변수로 사용할 수 있습니다.
