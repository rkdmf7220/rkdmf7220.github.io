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

## Lists

### Ordered list

1. Item 1
2. A second item
3. Number 3
4. Ⅳ

*Note: the fourth item uses the Unicode character for [Roman numeral four][2].*

### Unordered list

* An item
* Another item
* Yet another item
* And there's more...

## Paragraph modifiers

### Code block

    Code blocks are very useful for developers and other people who look at code or other things that are written in plain text. As you can see, it uses a fixed-width font.

You can also make `inline code` to add code into other things.

### Quote

> Here is a quote. What this is should be self explanatory. Quotes are automatically indented when they are used.

## Headings

There are six levels of headings. They correspond with the six levels of HTML headings. You've probably noticed them already in the page. Each level down uses one more hash character.

### Headings *can* also contain **formatting**

### They can even contain `inline code`

Of course, demonstrating what headings look like messes up the structure of the page.

I don't recommend using more than three or four levels of headings here, because, when you're smallest heading isn't too small, and you're largest heading isn't too big, and you want each size up to look noticeably larger and more important, there there are only so many sizes that you can use.

## URLs

URLs can be made in a handful of ways:

* A named link to [MarkItDown][3]. The easiest way to do these is to select what you want to make a link and hit `Ctrl+L`.
* Another named link to [MarkItDown](https://www.markitdown.net/)
* Sometimes you just want a URL like <https://www.markitdown.net/>.

## Horizontal rule

A horizontal rule is a line that goes across the middle of the page.

---

It's sometimes handy for breaking things up.

## Images

Markdown can also contain images. I'll need to add something here sometime.

## Finally

There's actually a lot more to Markdown than this. See the official [introduction][4] and [syntax][5] for more information. However, be aware that this is not using the official implementation, and this might work subtly differently in some of the little things.


[1]: https://daringfireball.net/projects/markdown/
[2]: https://www.fileformat.info/info/unicode/char/2163/index.htm
[3]: https://www.markitdown.net/
[4]: https://daringfireball.net/projects/markdown/basics
[5]: https://daringfireball.net/projects/markdown/syntax
