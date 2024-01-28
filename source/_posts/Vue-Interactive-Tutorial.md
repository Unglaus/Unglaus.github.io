---
title: Vue互动教程学习
date: 2023-03-16 20:02:38
tags: Vue
category: 前端技术学习
---

# 前言

Vue，易学易用，性能出色，适用场景丰富的 Web 前端框架。 

以上为官网给出的精炼概括，之前本科实习期间的项目是用Vue+SpringBoot来前后端分离地开发一个项目，就是那会儿接触到原来还有这么个东西。但是那会儿在忙考研，对搞前端又没有兴趣，所以当时分工的时候选择了后端开发，稍微学了学SpringBoot。而对前端开发技术Vue便是毫不关心，一点没学，现在想想也有点可惜，毕竟当时实习期间那个教程我感觉挺好的，应该是有很多干货的。

现在之所以想学Vue了，是发现想自己搞点Web项目的时候，只会后端技术完全不够，前端没有人给你写，只能去找别人的模板，然后用Thymeleaf来前后端交互，感觉不够自由，不够灵活。前端嘛，感觉还是根据自己的需求来设计比较好，到时候跟自己写的后端搭配应该也更方便些。

当然，以上还是我的幻想，Vue还没开始学，不知道到时候设计前端的这个难度具体到底如何。美好的幻想：想要个什么样的前端界面，都能给他弄出来，不求那种花里胡哨的，就基本功能能实现，界面设计得能好看点也就心满意足了。

下面开始Vue的学习，主要是看Vue的官网 https://cn.vuejs.org/

里面有比较详细的介绍了Vue的基本组件等。。。应该是吧，我也还没仔细看

这里主要是想介绍一下官网提供的一个互动教程https://cn.vuejs.org/tutorial/#step-1

该教材支持边教边实践，左边教着内容，右边给你地方写代码让你试。下面的内容主要围绕跟着这个互动教程学习过程的心得。

***



**下面笔记记的代码、代码解释，最好是拿到互动教程的页面，对照着实际页面生成的效果来看，更容易有深刻的理解。**



***

# 互动教程

## 声明式渲染(reactive、ref)

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

## Attribute绑定(v-bind " : ")

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

## 事件监听(v-on " @ ")

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

## 表单绑定 (v-model)

我们可以同时使用 `v-bind` 和 `v-on` 来在表单的输入元素上创建双向绑定：

```vue
<input :value="text" @input="onInput">
```

```js
methods: {
  onInput(e) {
    // v-on 处理函数会接收原生 DOM 事件
    // 作为其参数。
    this.text = e.target.value
  }
}
```

试着在文本框里输入——你会看到 `<p>` 里的文本也随着你的输入更新了。

为了简化双向绑定，Vue 提供了一个 `v-model` 指令，它实际上是上述操作的语法糖：

```vue
<input v-model="text">
```

`v-model` 会将被绑定的值与 `<input>` 的值自动同步，这样我们就不必再使用事件处理函数了。

`v-model` 不仅支持文本输入框，也支持诸如多选框、单选框、下拉框之类的输入类型。我们在[指南 - 表单绑定](https://cn.vuejs.org/guide/essentials/forms.html)中讨论了更多的细节。

现在，试着用 `v-model` 把代码重构一下吧。

```vue
<script>
export default {
  data() {
    return {
      text: ''
    }
  },
  //methods: {
  //  onInput(e) {
  //    this.text = e.target.value
  //  }
  //}
}
</script>

<template>
<!--   <input :value="text" @input="onInput" placeholder="Type here"> -->
  <input v-model= "text" placeholder="Type here">
  <p>{{ text }}</p>
</template>
```

我们注意到当使用`v-model`关键字时，就不需要使用`methods`中的`onInput(e)`函数来控制`text`的变化了。

因为text已经使用了v-model关键字，将`data(){return{text: ''} }`中的`text`变量与`<input>`块中输入的`value`值进行了双向绑定，即在`input`中输入一个值就会直接改变`text`的值，而且是动态进行的

如果使用上面`<input :value="text" @input="onInput" placeholder="Type here">`这种传统绑定发放，就还是需要上面注释掉的`methods`中的`onInput(e)`方法

## 条件渲染 (v-if)

我们可以使用 `v-if` 指令来有条件地渲染元素：

```vue
<h1 v-if="awesome">Vue is awesome!</h1>
```

这个 `<h1>` 标签只会在 `awesome` 的值为[真值 (Truthy)](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy) 时渲染。若 `awesome` 更改为[假值 (Falsy)](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)，它将被从 DOM 中移除。

我们也可以使用 `v-else` 和 `v-else-if` 来表示其他的条件分支：

```vue
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

现在，示例程序同时展示了两个 `<h1>` 标签，并且按钮不执行任何操作。尝试给它们添加 `v-if` 和 `v-else` 指令，并实现 `toggle()` 方法，让我们可以使用按钮在它们之间切换。

更多细节请查阅 `v-if`：[指南 - 条件渲染](https://cn.vuejs.org/guide/essentials/conditional.html)

简单示例：

```vue
<script>
export default {
  data() {
    return {
      awesome: true
    }
  },
  methods: {
    toggle() {
      this.awesome = !this.awesome
    }
  }
}
</script>

<template>
  <button @click="toggle">toggle</button>
  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>
</template>
```

### data()属性的用法

在Vue中，`data`属性用于定义组件实例的数据。它是一个函数，返回一个包含数据属性的对象。这些数据属性可以在组件的模板或方法中使用。

以下是使用`data`属性的示例：

```javascript
export default {
  data() {
    return {
      message: 'Hello, Vue!',
      count: 0
    };
  }
};
```

在上述示例中，`data`属性是一个函数，返回一个对象。该对象包含两个属性：`message`和`count`。这些属性可以在组件的模板中绑定数据，或在组件的方法中进行读取和修改。

在模板中使用数据属性时，可以通过双大括号插值语法（`{{ }}`）将其绑定到HTML内容中：

```html
<template>
  <div>
    <p>{{ message }}</p>
    <p>Count: {{ count }}</p>
  </div>
</template>
```

在上述示例中，`message`属性和`count`属性被绑定到两个`<p>`元素中的文本内容。当组件渲染时，模板中的插值表达式将被实际的属性值替换。

在组件的方法中，可以通过`this`关键字访问数据属性：

```javascript
export default {
  data() {
    return {
      message: 'Hello, Vue!',
      count: 0
    };
  },
  methods: {
    incrementCount() {
      this.count++;
    }
  }
};
```

在上述示例中，`incrementCount`方法通过`this.count`访问和修改`count`属性的值。通过这种方式，你可以在方法中操作数据属性。

需要注意的是，Vue的响应式系统会跟踪数据属性的变化，并在其发生变化时自动更新相关的视图。这意味着，如果你修改了数据属性的值，与之相关的模板将自动更新以反映这些变化。



## 列表渲染 (v-for)

我们可以使用 `v-for` 指令来渲染一个基于源数组的列表：

```vue
<ul>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
  </li>
</ul>
```

这里的 `todo` 是一个局部变量，表示当前正在迭代的数组元素。它只能在 `v-for` 所绑定的元素上或是其内部访问，就像函数的作用域一样。

注意，我们还给每个 todo 对象设置了唯一的 `id`，并且将它作为[特殊的 `key` attribute](https://cn.vuejs.org/api/built-in-special-attributes.html#key) 绑定到每个 `<li>`。`key` 使得 Vue 能够精确的移动每个 `<li>`，以匹配对应的对象在数组中的位置。

更新列表有两种方式：

1. 在源数组上调用[变更方法](https://stackoverflow.com/questions/9009879/which-javascript-array-functions-are-mutating)：

```js
this.todos.push(newTodo)
```

2. 使用新的数组替代原数组：

```js
this.todos = this.todos.filter(/* ... */)
```

这里有一个简单的 todo 列表——试着实现一下 `addTodo()` 和 `removeTodo()` 这两个方法的逻辑，使列表能够正常工作！

关于 `v-for` 的更多细节：[指南 - 列表渲染](https://cn.vuejs.org/guide/essentials/list.html)

```Vue
<script>
// 给每个 todo 对象一个唯一的 id
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      todos: [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue' }
      ]
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo }) //按照{ }中的格式更新todos
      this.newTodo = '' //更新完todos之后，初始化newTodo，为下一次输入做准备
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo) //注2
    }
  }
}
</script>

<template>
  <form @submit.prevent="addTodo"> <!-- 注1-->
    <input v-model="newTodo">  <!-- 使用v-model将input的值与变量newTodo双向绑定 -->
    <button>Add Todo</button>    
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
```

- `<form @submit.prevent="addTodo">` ：这是一个Vue.js中的模板语法，用于在表单提交时触发`addTodo`方法，并阻止表单默认的提交行为。

  在这个模板中，`@submit`是Vue.js的事件绑定语法，表示监听表单的提交事件。`.prevent`是一个修饰符，用于阻止表单的默认提交行为，即防止页面刷新。

  `addTodo`是一个在Vue实例中定义的方法，它会在表单提交时被调用。通过`@submit.prevent`绑定到表单的提交事件，可以在调用`addTodo`方法之前阻止表单的默认提交行为。

- `this.todos = this.todos.filter((t) => t !== todo)`：这段代码是一个在Vue.js中使用的数组过滤操作，它会从`this.todos`数组中移除与指定的`todo`对象相等的元素。在这段代码中，`this.todos`是一个数组，`.filter()`是JavaScript数组的方法之一，它用于遍历数组并返回一个新的数组，该新数组包含满足指定条件的元素。在这里，`.filter((t) => t !== todo)`表示使用一个箭头函数作为过滤条件。箭头函数中的`(t) => t !== todo`是一个回调函数，它接收数组中的每个元素作为参数`t`，并返回一个布尔值，用于确定是否保留该元素。具体到这段代码中，`(t) => t !== todo`表示只保留与`todo`对象不相等的元素。如果元素与`todo`对象相等，它将被过滤掉，不包含在最终的过滤结果中。最后，通过将过滤结果赋值给`this.todos`，实现了从`this.todos`数组中移除与指定的`todo`对象相等的元素。请注意，这段代码中的`this`指的是Vue实例或组件的上下文，在Vue组件中可以使用`this`来访问组件的数据和方法。



## 计算属性 (computed)

让我们在上一步的 todo 列表基础上继续。现在，我们已经给每一个 todo 添加了切换功能。这是通过给每一个 todo 对象添加 `done` 属性来实现的，并且使用了 `v-model` 将其绑定到复选框上：

```vue
<li v-for="todo in todos">
  <input type="checkbox" v-model="todo.done">
  ...
</li>
```

下一个可以添加的改进是隐藏已经完成的 todo。我们已经有了一个能够切换 `hideCompleted` 状态的按钮。但是应该如何基于状态渲染不同的列表项呢？

介绍一个新概念：[计算属性](https://cn.vuejs.org/guide/essentials/computed.html)。我们可以使用 `computed` 选项声明一个响应式的属性，它的值由其他属性计算而来：

```js
export default {
  // ...
  computed: {
    filteredTodos() {
      // 根据 `this.hideCompleted` 返回过滤后的 todo 项目
    }
  }
}
```

```diff
- <li v-for="todo in todos">
+ <li v-for="todo in filteredTodos">
```

计算属性会自动跟踪其计算中所使用的到的其他响应式状态，并将它们收集为自己的依赖。计算结果会被缓存，并只有在其依赖发生改变时才会被自动更新。

现在，试着添加 `filteredTodos` 计算属性并实现计算逻辑！如果实现正确，在隐藏已完成项目的状态下勾选一个 todo，它也应当被立即隐藏。

```vue
<script>
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Learn HTML', done: true },
        { id: id++, text: 'Learn JavaScript', done: true },
        { id: id++, text: 'Learn Vue', done: false }
      ]
    }
  },
  computed: {
    filteredTodos() {
      //... ...
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    }
  }
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <!-- <li v-for="todo in todos" :key="todo.id"> -->
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```

- `return this.hideCompleted ? this.todos.filter((t) => !t.done) : this.todos`：由后面`html`部分中`<button @click="hideCompleted = !hideCompleted">`可知该按钮根据按下次数在两种形态切换，根据`hideCompleted`的值判断是否进行隐藏，若不需要隐藏，`filteredTodos`的值就等于`todos`的值，若要隐藏，使用`vue`的数组过滤操作，滤除`todos`中`done`属性为`true`的值，`this.todos.filter((t) => !t.done)`仅允许`!t.done`为`ture`，即`t.done`为`false`的值通过过滤器，保留下来，成为`filteredTodos`的成员。其中`t.done`属性是根据下面`html`部分中`<input type="checkbox" v-model="todo.done">`选择框是否勾选来决定的，勾选即表示完成，因为通过`v-model`进行了绑定，会将与其绑定的值置为`true`，这里与`todo.done`绑定，所以勾选时会将`todo.done`置为`true`，取消勾选时会将`todo.done`置为`false`
- `<li v-for="todo in filteredTodos" :key="todo.id">`：将要显示的数组由静态的`todos`换成可变化的`filteredTodos`，以实现要求的功能



## 生命周期和模板引用 (mounted)

目前为止，Vue 为我们处理了所有的 DOM 更新，这要归功于响应性和声明式渲染。然而，有时我们也会不可避免地需要手动操作 DOM。

这时我们需要使用**模板引用**——也就是指向模板中一个 DOM 元素的 ref。我们需要通过[这个特殊的 `ref` attribute](https://cn.vuejs.org/api/built-in-special-attributes.html#ref) 来实现模板引用：

```vue
<p ref="pElementRef">hello</p>
```

此元素将作为 `this.$refs.pElementRef` 暴露在 `this.$refs` 上。然而，你只能在组件**挂载**之后访问它。

要在挂载之后执行代码，我们可以使用 `mounted` 选项：

```js
export default {
  mounted() {
    // 此时组件已经挂载。
  }
}
```

这被称为**生命周期钩子**——它允许我们注册一个在组件的特定生命周期调用的回调函数。还有一些其他的钩子如 `created` 和 `updated`。更多细节请查阅[生命周期图示](https://cn.vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)。

现在，尝试添加一个 `mounted` 钩子，然后通过 `this.$refs.pElementRef` 访问 `<p>`，并直接对其执行一些 DOM 操作。(例如修改它的 `textContent`)。

```vue
<script>
export default {
  // ...
  mounted(){
    const element = this.$refs.pElementRef;
    element.textContent = 'aaa'
  }
}
</script>

<template>
  <p ref="pElementRef">hello</p>
</template>
```

这个例子中，给`<p>`添加了一个`ref`属性(?)，`ref="pElementRef"`，这样我们就可以通过`this.$refs.pElementRef`来将它锁定，并可以对他进行一些操作。

不过就跟上面说的，需要在组件**挂载**之后才能访问，而要在挂载之后执行代码，就要使用`mounted`选项，在这里面写具体的代码。

说一下上面例子的结果，本来`<p>`跟着hello，网页上显示的也就是hello，而通过`this.$refs.pElementRef`锁定了`<p>`，并对它的`textContent`进行了修改，令其`textContent = 'aaa'`，所以最后网页上`<p>`的内容也就变成了`aaa`

上面的写法可以直接改成`this.$refs.pElementRef.textContent = 'aaa'`，效果是一样的。

另外`const element = this.$refs.pElementRef;`要注意前面的**`const`**，将`element`声明为了静态变量，这是必须的，如果不加这个关键字将其声明为静态变量，则声明的这个`element`相当于是`<p>`的一个副本，不会真正与下面`<p>`绑定，后续的`element.textContent = 'aaa'`也不会改变`hello`为`aaa`。

而添加`const`关键字，声明成静态变量，则这个`element`才是真正跟下面的`<p>`进行了绑定，`element.textContent = 'aaa'`也就能够改变`hello`为`aaa`





# 知识补充

### 关于export default

`export default` 是 ES6（ECMAScript 2015）模块系统中用于导出默认值的语法。

在 JavaScript 中，模块系统可以帮助我们将代码分割为不同的模块，以便更好地组织、复用和维护代码。ES6 引入了一种新的模块语法，其中 `export` 关键字用于将值、函数或类等从模块中导出，而 `import` 关键字用于在其他模块中导入这些导出的内容。

`export default` 的作用是导出模块的默认值。一个模块只能有一个默认导出，而且默认导出可以是任何合法的 JavaScript 值，例如对象、函数、类等。通过使用 `export default`，我们可以在导入该模块时，直接获取默认导出的值，而无需使用具体的名称。

以下是一个示例，展示了如何使用 `export default` 导出和导入默认值：

```js
// module.js
const myDefault = {
  name: 'John',
  age: 30
};

export default myDefault;

// main.js
import myDefault from './module.js';

console.log(myDefault); // 输出: { name: 'John', age: 30 }
```

在上述示例中，`module.js` 文件中使用 `export default` 导出了一个对象 `myDefault`，它作为模块的默认导出。然后，在 `main.js` 文件中使用 `import myDefault from './module.js'` 导入了该默认导出，并将其赋值给了 `myDefault` 变量。此后，我们可以直接使用 `myDefault` 变量来访问和操作模块的默认导出值。

需要注意的是，使用 `export default` 导出的默认值在导入时可以使用任意的名称，因为它是默认导出。但是，可以通过 `import { ... } from './module.js'` 的语法导入模块中其他被具名导出的成员。

#### export default中的属性

以下是一些常见的 Vue 组件属性：

- `props`: 用于接收父组件传递的数据，可以通过属性传递给子组件。
- `computed`: 用于定义基于组件的响应式数据计算得出的属性。可以根据其他数据的变化自动更新。
- `watch`: 用于监听一个或多个数据的变化，并在数据发生变化时执行相应的操作。
- `components`: 用于注册子组件，使其在当前组件中可用。
- `template`: 定义组件的模板，包含 HTML 结构和 Vue 模板语法。
- `created`: 组件生命周期钩子，表示组件实例被创建后立即调用的钩子函数。
- `mounted`: 组件生命周期钩子，表示组件挂载到 DOM 后调用的钩子函数。
- `beforeDestroy`: 组件生命周期钩子，表示组件销毁之前调用的钩子函数。
- `computed`: 用于定义计算属性，可以根据响应式数据的变化动态计算出新的值。
- `methods`: 定义组件的方法，用于处理事件、执行业务逻辑等。
- `v-model`: 用于实现双向数据绑定，将组件的数据绑定到表单元素或自定义组件上。



# Vue脚手架

写这个blog另一个很大的原因是，就是想找个地方感慨一下这个事儿。

当时本科实习期间老师还是教着我们用Vue Cli这个脚手架，到现在我再回头想学Vue想着看看Cli脚手架的时候发现它已经进入维护状态，官方不再推荐了。现在官方推荐了新的Vue脚手架Vite，该脚手架也是Vue的作者写的。

就是想感慨一下这技术发展是真快啊感觉，不过前面也说了，实习那会儿Vue我就基本没学，更不用说这个Vue Cli脚手架了，直接转去学新的脚手架Vite毫无负担，血赚，哎嘿。但没仔细学当时的Vue教程，血亏，嘤。

话说这样我之前搭的Vue Cli脚手架就白搭了，等着看看Vite脚手架的搭建有没有什么主意的地方，有的好也可以写个Blog，写写使用心得之类的，到时候就把这部分内容移过去。
