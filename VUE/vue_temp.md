created:在模板渲染成html前调用，即通常初始化某些属性值，然后再渲染成视图。
mounted:在模板渲染成html后调用，通常是初始化页面完成后，再对html的dom节点进行一些需要的操作。



==ref==  被用来给元素或子组件注册引用信息。引用信息将会注册在父组件的 `$refs` 对象上。如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例: （引用）

```html
<!-- `vm.$refs.p` will be the DOM node -->
<p ref="p">hello</p>
```

==prop==  在组件上注册的一些自定义 attribute。当一个值传递给一个 prop attribute 的时候，它就变成了那个组件实例的一个 property(性质)。

> 组件实例的作用域是孤立的。这意味着不能 (也不应该) 在子组件的模板内直接引用父组件的数据。父组件的数据需要通过 prop 才能下发到子组件中。

```html
<div>
    <el-table :data='posts'>
    	<el-table-column prop='id'></el-table-column>
        <el-table-column prop='title'></el-table-column>
    </el-table>
</div>

<script>
data: {
    posts: [
      { id: 1, title: 'My journey with Vue' },
      { id: 2, title: 'Blogging with Vue' },
      { id: 3, title: 'Why Vue is so fun' }
    ]
  }
</script>
```

props是子组件访问父组件数据的唯一接口。单向数据流： props是单向绑定的。

详细一点解释就是：
一个组件可以直接在模板里面渲染data里面的数据（双大括号）。
子组件不能直接在模板里面渲染父元素的数据。
如果子组件想要引用父元素的数据，那么就在prop里面声明一个变量（比如a），这个变量就可以引用父元素的数据。然后在模板里渲染这个变量（前面的a），这时候渲染出来的就是父元素里面的数据。

```html
<!--父组件-->
<template>
  <div>
      <hello-world2 :good = "good"></hello-world2> //向子组件传值
  </div>
</template>

<script>
  import helloWorld2 from "./HelloWorld2"  //引用子组件页面

  export default {
    name: "HelloWorld3",
    data() {
      return {
        good: "我是从hello word3传递过来的"
      }
    },
    components: {
      'hello-world2': helloWorld2   //注册子组件
    },
  }
</script>
```

```html
<!--子组件-->
<template>
    <div>{{good}}</div>
</template>

<script>
  export default {
    props: ['good'], //通过props获取父组件传递过来的值
    data: function () {
      return {}
    },
    methods: {}
  }
</script>
```

**总结**：父组件通过v-bind向子组件传值，子组件通过props来获取父组件传递过来的值，被引用的就是子组件。

#### `v-if` vs `v-show`

`v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。

`v-if` 也是**惰性的**：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

相比之下，`v-show` 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说，`v-if` 有更高的切换开销，而 `v-show` 有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。

#### splice

`splice()` 方法向/从数组中添加/删除项目，然后返回被删除的项目。

```
arrayObject.splice(index,howmany,item1,.....,itemX)
```

| 参数              | 描述                                                         |
| :---------------- | :----------------------------------------------------------- |
| index             | 必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。 |
| howmany           | 必需。要删除的项目数量。如果设置为 0，则不会删除项目。       |
| item1, ..., itemX | 可选。向数组添加的新项目。                                   |

#### vue-router传递参数

1、path 不能和 params 一起用。

```js
this.$router.push({ name: 'news', params: { userId: 123 }})
```

2、可以和 query 一起用

```js
this.$router.push({ path: '/news', query: { userId: 123 }});
```

另一个页面在create方法里接收变量：

```js
this.$route.params
```

#### trigger 触发方式

blur失去焦点，change数据改变



### Vue CLI

基于Vue.js进行快速开发的完整系统，通过`@vue/cli`实现的交互式项目脚手架。

#### 创建项目

```shell
#vue create project-name
```

#### 插件

如果想在一个已经创建好的项目中安装一个插件，可以使用 `vue add` 命令：

```sh
#vue add eslint
```

Preset 是一个包含在创建新项目所需预定义选项和插件的 JSON 对象。

```json
{
  "useConfigFiles": true,
  "plugins": {...},
  "configs": {
    "vue": {...},
    "postcss": {...},
    "eslintConfig": {...},
    "jest": {...}
  }
}
```

#### HTML和静态资源

`public/index.html` 文件是一个会被 [html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin) 处理的模板。在构建过程中，资源链接会被自动注入。另外，Vue CLI 也会自动注入 resource hint (`preload/prefetch`、manifest 和图标链接 (当用到 PWA 插件时) 以及构建过程中处理的 JavaScript 和 CSS 文件的资源链接。

静态资源在文件中使用相对路径 (必须以 `.` 开头) ，该资源会被包含进入webpack 的依赖图中。例如，`url(./image.png)` 会被翻译为 `require('./image.png')`，而：

```html
<img src="./image.png">
```

将会被编译到：

```js
h('img', { attrs: { src: require('./image.png') }})
```

在其内部，我们通过 `file-loader` 用版本哈希值和正确的公共基础路径来决定最终的文件路径，再用 `url-loader` 将小于 4kb 的资源内联，以减少 HTTP 请求的数量。

##### `public` 文件夹

任何放置在 `public` 文件夹的静态资源都会被简单的复制，而不经过 webpack。你需要通过绝对路径来引用它们。