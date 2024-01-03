---
title: Vue互动教程学习
date: 2023-03-16 20:02:38
tags: Vue
category: 前端技术学习
---

## 前言

Vue，易学易用，性能出色，适用场景丰富的 Web 前端框架。 

以上为官网给出的精炼概括，之前本科实习期间的项目是用Vue+SpringBoot来前后端分离地开发一个项目，就是那会儿接触到原来还有这么个东西。但是那会儿在忙考研，对搞前端又没有兴趣，所以当时分工的时候选择了后端开发，稍微学了学SpringBoot。而对前端开发技术Vue便是毫不关心，一点没学，现在想想也有点可惜，毕竟当时实习期间那个教程我感觉挺好的，应该是有很多干货的。

现在之所以想学Vue了，是发现想自己搞点Web项目的时候，只会后端技术完全不够，前端没有人给你写，只能去找别人的模板，然后用Thymeleaf来前后端交互，感觉不够自由，不够灵活。前端嘛，感觉还是根据自己的需求来设计比较好，到时候跟自己写的后端搭配应该也更方便些。

当然，以上还是我的幻想，Vue还没开始学，不知道到时候设计前端的这个难度具体到底如何。美好的幻想：想要个什么样的前端界面，都能给他弄出来，不求那种花里胡哨的，就基本功能能实现，界面设计得能好看点也就心满意足了。

下面开始Vue的学习，主要是看Vue的官网 https://cn.vuejs.org/

里面有比较详细的介绍了Vue的基本组件等。。。应该是吧，我也还没仔细看

这里主要是想介绍一下官网提供的一个互动教程https://cn.vuejs.org/tutorial/#step-1

该教材支持边教边实践，左边教着内容，右边给你地方写代码让你试。下面的内容主要围绕跟着这个互动教程学习过程的心得。

## 互动教程

### 声明式渲染

Vue 的核心功能是**声明式渲染**：通过扩展于标准 HTML 的模板语法，我们可以根据 JavaScript 的状态来描述 HTML 应该是什么样子的。当状态改变时，HTML 会自动更新。

能在改变时触发更新的状态被称作是**响应式**的。我们可以使用 Vue 的 `reactive()` API 来声明响应式状态。由 `reactive()` 创建的对象都是 JavaScript [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)，其行为与普通对象一样：


```js
import { reactive } from 'vue'

const counter = reactive({
  count: 0
})

console.log(counter.count) // 0
counter.count++
```

其中reactive中可以定义有多个属性，属性之间用逗号“，”分隔

```js
const student = reactive({
    name: 'SJH',
    age: 24,
    wages: 200
})
```

`reactive()` 只适用于对象 (包括数组和内置类型，如 `Map` 和 `Set`)。而另一个 API `ref()` 则可以接受任何值类型。`ref` 会返回一个包裹对象，并在 `.value` 属性下暴露内部值。


```js
import { ref } from 'vue'

const message = ref('Hello World!')

console.log(message.value) // "Hello World!"
message.value = 'Changed'
```

`reactive()` 和 `ref()` 的细节在[指南 - 响应式基础](https://cn.vuejs.org/guide/essentials/reactivity-fundamentals.html)一节中有进一步讨论。

在组件的 `<script setup>` 块中声明的响应式状态，可以直接在模板中使用。下面展示了我们如何使用双花括号语法，根据 `counter` 对象和 `message` ref 的值渲染动态文本：

```html
<h1>{{ message }}</h1>
<p>count is: {{ counter.count }}</p>
```

注意我们在模板中访问的 `message` ref 时不需要使用 `.value`：它会被自动解包，让使用更简单。

在双花括号中的内容并不只限于标识符或路径——我们可以使用任何有效的 JavaScript 表达式。

```html
<h1>{{ message.split('').reverse().join('') }}</h1>
```

### Attribute绑定

Attribute绑定，`v-bind`指令，拿`div`举例`<div v-bind:id="dynamicID"></div>`，其中的`v-bind`一简写，就变成了`<div :id="dynamicID"></div>`，就剩个冒号了，这一般还真不知道是个什么意思，也没法查起。



在 Vue 中，mustache 语法 (即双大括号) 只能用于文本插值。为了给 attribute 绑定一个动态值，需要使用 `v-bind` 指令：

```html
<div v-bind:id="dynamicId"></div>
```

**指令**是由 `v-` 开头的一种特殊 attribute。它们是 Vue 模板语法的一部分。和文本插值类似，指令的值是可以访问组件状态的 JavaScript 表达式。关于 `v-bind` 和指令语法的完整细节请详阅[指南 - 模板语法](https://cn.vuejs.org/guide/essentials/template-syntax.html)。

冒号后面的部分 (`:id`) 是指令的“参数”。此处，元素的 `id` attribute 将与组件状态里的 `dynamicId` 属性保持同步。

由于 `v-bind` 使用地非常频繁，它有一个专门的简写语法：

```html
<div :id="dynamicId"></div>
```

现在，试着把一个动态的 `class` 绑定添加到这个 `<h1>` 上，并使用 `titleClass` 的 ref 作为它的值。如果绑定正确，文字将会变为红色。

```vue
<script setup>
import { ref } from 'vue'

const titleClass = ref('title')
</script>

<template>
  <h1 :class = titleClass>Make me red</h1> <!-- 此处添加一个动态 class 绑定 -->
</template>

<style>
.title {
  color: red;
}
</style>
```

使用 **`<script setup>`** 标签来编写 Vue 3 的组合式 API 代码。

在 `<style>` 标签中，定义了 `.title` 类选择器，将文本颜色设置为红色。

在渲染时将 `<h1>` 元素的 class 设置为 `'title'`，从而应用 `.title` 类的样式，使文本颜色变为红色。

设置的时候用到的是动态绑定，让`<h1>`的`class`设为`titleClass`，而`titleClass`的值为`title`，从而实现`class = title`的赋值

### 事件监听

事件监听，`v-on`指令，拿`button`举例`<button v-on:click="increment">{{ count }}</button>`，可以简写为`<button @click="increment">{{ count }}</button>`，这种@的写法我感觉还真见过不少，当时没学不知道是什么意思，原来是事件监听`v-on`的缩写。



我们可以使用 `v-on` 指令监听 DOM 事件：

```vue
<button v-on:click="increment">{{ count }}</button>
```

因为其经常使用，`v-on` 也有一个简写语法：

```vue
<button @click="increment">{{ count }}</button>
```

此处，`increment` 引用了一个在 `<script setup>` 中声明的函数：

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  // 更新组件状态
  count.value++
}
</script>
```

在函数中，我们可以通过修改 ref 来更新组件状态。

事件处理函数也可以使用内置表达式，并且可以使用修饰符简化常见任务。这些细节包含在[指南 - 事件处理](https://cn.vuejs.org/guide/essentials/event-handling.html)。

现在，尝试自行实现 `increment` 函数并通过使用 `v-on` 将其绑定到按钮上。

```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)
function sub(){
  count.value--
}
</script>

<template>
  <!-- 使此按钮生效 -->
  <button @click="sub">count is: {{ count }}</button>
</template>
```



## Vue脚手架

写这个blog另一个很大的原因是，就是想找个地方感慨一下这个事儿。

当时本科实习期间老师还是教着我们用Vue Cli这个脚手架，到现在我再回头想学Vue想着看看Cli脚手架的时候发现它已经进入维护状态，官方不再推荐了。现在官方推荐了新的Vue脚手架Vite，该脚手架也是Vue的作者写的。

就是想感慨一下这技术发展是真快啊感觉，不过前面也说了，实习那会儿Vue我就基本没学，更不用说这个Vue Cli脚手架了，直接转去学新的脚手架Vite毫无负担，血赚，哎嘿。但没仔细学当时的Vue教程，血亏，嘤。

话说这样我之前搭的Vue Cli脚手架就白搭了，等着看看Vite脚手架的搭建有没有什么主意的地方，有的好也可以写个Blog，写写使用心得之类的，到时候就把这部分内容移过去。
