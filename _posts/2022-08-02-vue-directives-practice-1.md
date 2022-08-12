---
layout: post
title: vue.js 공부
subtitle: v-bind, v-on, v-for, props, emit
categories: jekyll
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

```practice.vue(양방향)
<template>
  <input type="text" v-model="inputText">
</template>

<seript>
export default {
  data() {
    return {
      inputText: ''
    }
  }
}
</script>
```

```practice.vue(단방향)
<template>
  <input type="text" v-bind="inputText"  v-on="updateInput">
</template>

<seript>
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
