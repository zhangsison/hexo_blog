---

title: vue 安装
date: 2019-12-06
categories: [web]
tags: [vue]

---



## vue 安装

安装npm install webpack -g

卸载 npm uninstall webpack --save-dev

#### 安装vue脚手架
```vue
1. npm install vue-cli webpack -g （全局安装vue脚手架和webpack）

2. 进入工程目录 vue init webpack my-project （进入目录项目名称）

3. cd my-project

4. npm install （安装项目依赖，一定要用npm，会比较慢）

5. npm install vue-router vue-resource --save-dev（安装 vue 路由模块vue-router和网络请求模块vue-resource）

6. npm run dev（本地运行）

7. npm run build（生成服务器build）

```



http://doc.liangxinghua.com/vue-family/1.3.html

![image-20201121154027418](https://i.loli.net/2020/11/21/VuJmTjK9BIpaLOH.png)

```
<script>
export default {
  name: "Home",
  data() {
    return {};
  },
  methods: {
    // 组件的方法
  },
  watch: {
    // watch擅长处理的场景：一个数据影响多个数据
  },
  computed: {
    // computed擅长处理的场景：一个数据受多个数据影响
  },
  beforeCreate: function() {
    // 在实例初始化之后，数据观测(data observer) 和 event/watcher 事件配置之前被调用。
  },
  created: function() {
    // 实例已经创建完成之后被调用。在这一步，实例已完成以下的配置：数据观测(data observer)，属性和方法的运算， watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
  },
  beforeMount: function() {
    // 在挂载开始之前被调用：相关的 render 函数首次被调用。
  },
  mounted: function() {
    // 编译好的HTML挂载到页面完成后执行的事件钩子
    // el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。
    // 此钩子函数中一般会做一些ajax请求获取数据进行数据初始化
    console.log("Home done");
  },
  beforeUpdate: function() {
    // 数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。
  },
  updated: function() {
    // 由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。
    // 当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。
    // 该钩子在服务器端渲染期间不被调用。
  },
  beforeDestroy: function() {
    // 实例销毁之前调用。在这一步，实例仍然完全可用。
  },
  destroyed: function() {
    // Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。 该钩子在服务器端渲染期间不被调用。
  }
};
</script>
```

#### v- 指令是带有v-的特殊属性

```

    v-if 条件渲染
    v-show
    v-else (必须在v-if/v-else-if/v-show指令后)
    v-else-if (v-if/v-else-if后)
    v-for (遍历)
    v-html (绑定HTML属性中的值)   (本篇先讲这6个)
    v-bind (响应更新HTML特性，绑定自定义属性，如绑定某个class元素或style)
    v-on (监听指定元素的dom事件)
    v-model (内置的双向数据绑定，用在表单控件，绑定的value通常是静态字符串)
    v-cloak 关于vuejs页面闪烁{{message}}
    v-once 只渲染元素和组件一次，随后的重新渲染,元素/组件及其所有的子节点将被视为静态内容并跳过

```



```js
let index = arr.findIndex(item => item.id == this.a_id); //根据 已知id（this.a_id） 获取在数组中的位置(index)；

const obj = response.list.find(function(obj) {
    return obj.id === that.form.adminCourseId
})
```

vue日期转时间戳

```
console.log((new Date(this.form.startTime)).getTime() / 1000)

当前时间戳
Math.round(new Date() / 1000)
```