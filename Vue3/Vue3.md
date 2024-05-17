> vite: https://github.com/vitejs/vite
>
> 面试题：谈谈你对vite的理解，最好对比webpack说明

# 使用vite创建vue3

```
npm create vite@latest
```

webpack 原理图

<img src="http://mdrs.yuanjin.tech/img/20200929144416.png" alt="image-20200929144416064" style="zoom:50%;" />

vite 原理图

<img src="http://mdrs.yuanjin.tech/img/20200929144957.png" alt="image-20200929144957808" style="zoom:50%;" />

> 面试题答案：
>
> webpack会先打包，然后启动开发服务器，请求服务器时直接给予打包结果。
> 而vite是直接启动开发服务器，请求哪个模块再对该模块进行实时编译。
> 由于现代浏览器本身就支持ES Module，会自动向依赖的Module发出请求。vite充分利用这一点，将开发环境下的模块文件，就作为浏览器要执行的文件，而不是像webpack那样进行打包合并。
> 由于vite在启动的时候不需要打包，也就意味着不需要分析模块的依赖、不需要编译，因此启动速度非常快。当浏览器请求某个模块时，再根据需要对模块内容进行编译。这种按需动态编译的方式，极大的缩减了编译时间，项目越复杂、模块越多，vite的优势越明显。
> 在HMR方面，当改动了一个模块后，仅需让浏览器重新请求该模块即可，不像webpack那样需要把该模块的相关依赖模块全部编译一次，效率更高。
> 当需要打包到生产环境时，vite使用传统的rollup进行打包，因此，vite的主要优势在开发阶段。另外，由于vite利用的是ES Module，因此在代码中不可以使用CommonJS

> 客户端渲染效率比vue2提升了1.3~2倍
>
> SSR渲染效率比vue2提升了2~3倍

> 面试题：vue3的效率提升主要表现在哪些方面？

# 静态提升

下面的静态节点会被提升

- 元素节点
- 没有绑定动态内容

```js
// vue2 的静态节点
render(){
  createVNode("h1", null, "Hello World")
  // ...
}

// vue3 的静态节点
const hoisted = createVNode("h1", null, "Hello World")
function render(){
  // 直接使用 hoisted 即可
}
```

静态属性会被提升

```html
<div class="user">
  {{user.name}}
</div>
```

```js
const hoisted = { class: "user" }

function render(){
  createVNode("div", hoisted, user.name)
  // ...
}
```

# 预字符串化

```html
<div class="menu-bar-container">
  <div class="logo">
    <h1>logo</h1>
  </div>
  <ul class="nav">
    <li><a href="">menu</a></li>
    <li><a href="">menu</a></li>
    <li><a href="">menu</a></li>
    <li><a href="">menu</a></li>
    <li><a href="">menu</a></li>
  </ul>
  <div class="user">
    <span>{{ user.name }}</span>
  </div>
</div>
```

当编译器遇到大量连续的静态内容，会直接将其编译为一个普通字符串节点

```js
const _hoisted_2 = _createStaticVNode("<div class=\"logo\"><h1>logo</h1></div><ul class=\"nav\"><li><a href=\"\">menu</a></li><li><a href=\"\">menu</a></li><li><a href=\"\">menu</a></li><li><a href=\"\">menu</a></li><li><a href=\"\">menu</a></li></ul>")
```

<img src="http://mdrs.yuanjin.tech/img/20200929170205.png" alt="image-20200929170205828" style="zoom:50%;" />

<img src="http://mdrs.yuanjin.tech/img/20200929170304.png" alt="image-20200929170304873" style="zoom:50%;" />

# 缓存事件处理函数

```html
<button @click="count++">plus</button>
```

```js
// vue2
render(ctx){
  return createVNode("button", {
    onClick: function($event){
      ctx.count++;
    }
  })
}

// vue3
render(ctx, _cache){
  return createVNode("button", {
    onClick: cache[0] || (cache[0] = ($event) => (ctx.count++))
  })
}
```

# Block Tree

vue2在对比新旧树的时候，并不知道哪些节点是静态的，哪些是动态的，因此只能一层一层比较，这就浪费了大部分时间在比对静态节点上

```html
<form>
  <div>
    <label>账号：</label>
    <input v-model="user.loginId" />
  </div>
  <div>
    <label>密码：</label>
    <input v-model="user.loginPwd" />
  </div>
</form>
```

<img src="http://mdrs.yuanjin.tech/img/20200929172002.png" alt="image-20200929172002761" style="zoom:50%;" />

<img src="http://mdrs.yuanjin.tech/img/20200929172555.png" alt="image-20200929172555681" style="zoom:50%;" />

# PatchFlag

vue2在对比每一个节点时，并不知道这个节点哪些相关信息会发生变化，因此只能将所有信息依次比对

```html
<div class="user" data-id="1" title="user name">
  {{user.name}}
</div>
```

<img src="http://mdrs.yuanjin.tech/img/20200929172805.png" alt="image-20200929172805674" style="zoom:50%;" />

> 面试题1：为什么vue3中去掉了vue构造函数？
>
> 面试题2：谈谈你对vue3数据响应式的理解

# 去掉了Vue构造函数

在过去，如果遇到一个页面有多个`vue`应用时，往往会遇到一些问题

```html
<!-- vue2 -->
<div id="app1"></div>
<div id="app2"></div>
<script>
  Vue.use(...); // 此代码会影响所有的vue应用
  Vue.mixin(...); // 此代码会影响所有的vue应用
  Vue.component(...); // 此代码会影响所有的vue应用
                
	new Vue({
    // 配置
  }).$mount("#app1")
  
  new Vue({
    // 配置
  }).$mount("#app2")
</script>
```

在`vue3`中，去掉了`Vue`构造函数，转而使用`createApp`创建`vue`应用

```html
<!-- vue3 -->
<div id="app1"></div>
<div id="app2"></div>
<script>  
	createApp(根组件).use(...).mixin(...).component(...).mount("#app1")
  createApp(根组件).mount("#app2")
</script>
```

> 更多vue应用的api：https://v3.vuejs.org/api/application-api.html

# 组件实例中的API

在`vue3`中，组件实例是一个`Proxy`，它仅提供了下列成员，功能和`vue2`一样

属性：https://v3.vuejs.org/api/instance-properties.html

方法：https://v3.vuejs.org/api/instance-methods.html

# 对比数据响应式

vue2和vue3均在相同的生命周期完成数据响应式，但做法不一样

<img src="http://mdrs.yuanjin.tech/img/20201014155433.png" alt="image-20201014155433311" style="zoom:50%;" />

# 面试题参考答案

面试题1：为什么vue3中去掉了vue构造函数？

```
vue2的全局构造函数带来了诸多问题：
1. 调用构造函数的静态方法会对所有vue应用生效，不利于隔离不同应用
2. vue2的构造函数集成了太多功能，不利于tree shaking，vue3把这些功能使用普通函数导出，能够充分利用tree shaking优化打包体积
3. vue2没有把组件实例和vue应用两个概念区分开，在vue2中，通过new Vue创建的对象，既是一个vue应用，同时又是一个特殊的vue组件。vue3中，把两个概念区别开来，通过createApp创建的对象，是一个vue应用，它内部提供的方法是针对整个应用的，而不再是一个特殊的组件。
```

面试题2：谈谈你对vue3数据响应式的理解

```
vue3不再使用Object.defineProperty的方式定义完成数据响应式，而是使用Proxy。
除了Proxy本身效率比Object.defineProperty更高之外，由于不必递归遍历所有属性，而是直接得到一个Proxy。所以在vue3中，对数据的访问是动态的，当访问某个属性的时候，再动态的获取和设置，这就极大的提升了在组件初始阶段的效率。
同时，由于Proxy可以监控到成员的新增和删除，因此，在vue3中新增成员、删除成员、索引访问等均可以触发重新渲染，而这些在vue2中是难以做到的。
```

# v-model

`vue2`比较让人诟病的一点就是提供了两种双向绑定：`v-model`和`.sync`，在`vue3`中，去掉了`.sync`修饰符，只需要使用`v-model`进行双向绑定即可。

为了让`v-model`更好的针对多个属性进行双向绑定，`vue3`作出了以下修改

- 当对自定义组件使用`v-model`指令时，绑定的属性名由原来的`value`变为`modelValue`，事件名由原来的`input`变为`update:modelValue`

  ```html
  <!-- vue2 -->
  <ChildComponent :value="pageTitle" @input="pageTitle = $event" />
  <!-- 简写为 -->
  <ChildComponent v-model="pageTitle" />
  
  <!-- vue3 -->
  <ChildComponent
    :modelValue="pageTitle"
    @update:modelValue="pageTitle = $event"
  />
  <!-- 简写为 -->
  <ChildComponent v-model="pageTitle" />
  ```

- 去掉了`.sync`修饰符，它原本的功能由`v-model`的参数替代

  ```html
  <!-- vue2 -->
  <ChildComponent :title="pageTitle" @update:title="pageTitle = $event" />
  <!-- 简写为 -->
  <ChildComponent :title.sync="pageTitle" />
  
  <!-- vue3 -->
  <ChildComponent :title="pageTitle" @update:title="pageTitle = $event" />
  <!-- 简写为 -->
  <ChildComponent v-model:title="pageTitle" />
  ```

- `model`配置被移除

- 允许自定义`v-model`修饰符

  vue2 无此功能

  <img src="http://mdrs.yuanjin.tech/img/20201008163022.png" alt="image-20201008163021918" style="zoom:50%;" />

# v-if v-for

`v-if` 的优先级 现在高于 `v-for`

# key

- 当使用`<template>`进行`v-for`循环时，需要把`key`值放到`<template>`中，而不是它的子元素中

- 当使用`v-if v-else-if v-else`分支的时候，不再需要指定`key`值，因为`vue3`会自动给予每个分支一个唯一的`key`

  即便要手工给予`key`值，也必须给予每个分支唯一的`key`，**不能因为要重用分支而给予相同的 key**

# Fragment

`vue3`现在允许组件出现多个根节点

# Teleport

# asyncComponent

> reactivity api: https://v3.vuejs.org/api/reactivity-api

# 获取响应式数据

| API        | 传入                      | 返回             | 备注                                                         |
| :--------- | ------------------------- | ---------------- | ------------------------------------------------------------ |
| `reactive` | `plain-object`            | `对象代理`       | 深度代理对象中的所有成员                                     |
| `readonly` | `plain-object` or `proxy` | `对象代理`       | 只能读取代理对象中的成员，不可修改                           |
| `ref`      | `any`                     | `{ value: ... }` | 对value的访问是响应式的<br />如果给value的值是一个对象，<br />则会通过`reactive`函数进行代理<br />如果已经是代理，则直接使用代理 |
| `computed` | `function`                | `{ value: ... }` | 当读取value值时，<br />会**根据情况**决定是否要运行函数      |

应用：

- 如果想要让一个对象变为响应式数据，可以使用`reactive`或`ref`
- 如果想要让一个对象的所有属性只读，使用`readonly`
- 如果想要让一个非对象数据变为响应式数据，使用`ref`
- 如果想要根据已知的响应式数据得到一个新的响应式数据，使用`computed`

笔试题1：下面的代码输出结果是什么？

```js
import { reactive, readonly, ref, computed } from "vue";

const state = reactive({
  firstName: "Xu Ming",
  lastName: "Deng",
});
const fullName = computed(() => {
  console.log("changed");
  return `${state.lastName}, ${state.firstName}`;
});
console.log("state ready");
console.log("fullname is", fullName.value);
console.log("fullname is", fullName.value);
const imState = readonly(state);
console.log(imState === state);

const stateRef = ref(state);
console.log(stateRef.value === state);

state.firstName = "Cheng";
state.lastName = "Ji";

console.log(imState.firstName, imState.lastName);
console.log("fullname is", fullName.value);
console.log("fullname is", fullName.value);

const imState2 = readonly(stateRef);
console.log(imState2.value === stateRef.value);

```

笔试题2：按照下面的要求完成函数

```js
function useUser(){
  // 在这里补全函数
    
    
    
    
  return {
    user, // 这是一个只读的用户对象，响应式数据，默认为一个空对象
    setUserName, // 这是一个函数，传入用户姓名，用于修改用户的名称
    setUserAge, // 这是一个函数，传入用户年龄，用户修改用户的年龄
  }
}
```

笔试题3：按照下面的要求完成函数

```js
function useDebounce(obj, duration){
  // 在这里补全函数
  return {
    value, // 这里是一个只读对象，响应式数据，默认值为参数值
    setValue // 这里是一个函数，传入一个新的对象，需要把新对象中的属性混合到原始对象中，混合操作需要在duration的时间中防抖
  }
}
```



# 监听数据变化

**watchEffect**

```js
const stop = watchEffect(() => {
  // 该函数会立即执行，然后追中函数中用到的响应式数据，响应式数据变化后会再次执行
})

// 通过调用stop函数，会停止监听
stop(); // 停止监听
```

**watch**

```js
// 等效于vue2的$watch

// 监听单个数据的变化
const state = reactive({ count: 0 })
watch(() => state.count, (newValue, oldValue) => {
  // ...
}, options)

const countRef = ref(0);
watch(countRef, (newValue, oldValue) => {
  // ...
}, options)

// 监听多个数据的变化
watch([() => state.count, countRef], ([new1, new2], [old1, old2]) => {
  // ...
});
```

**注意：无论是`watchEffect`还是`watch`，当依赖项变化时，回调函数的运行都是异步的（微队列）**

应用：除非遇到下面的场景，否则均建议选择`watchEffect`

- 不希望回调函数一开始就执行
- 数据改变时，需要参考旧值
- 需要监控一些回调函数中不会用到的数据

笔试题: 下面的代码输出结果是什么？

```js
import { reactive, watchEffect, watch } from "vue";
const state = reactive({
  count: 0,
});
watchEffect(() => {
  console.log("watchEffect", state.count);
});
watch(
  () => state.count,
  (count, oldCount) => {
    console.log("watch", count, oldCount);
  }
);
console.log("start");
setTimeout(() => {
  console.log("time out");
  state.count++;
  state.count++;
});
state.count++;
state.count++;

console.log("end");

```



# 判断

| API          | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| `isProxy`    | 判断某个数据是否是由`reactive`或`readonly`                   |
| `isReactive` | 判断某个数据是否是通过`reactive`创建的<br />详细:https://v3.vuejs.org/api/basic-reactivity.html#isreactive |
| `isReadonly` | 判断某个数据是否是通过`readonly`创建的                       |
| `isRef`      | 判断某个数据是否是一个`ref`对象                              |



# 转换

**unref**

等同于：`isRef(val) ? val.value : val`

应用：

```js
function useNewTodo(todos){
  todos = unref(todos);
  // ...
}
```



**toRef**

得到一个响应式对象某个属性的ref格式

```js
const state = reactive({
  foo: 1,
  bar: 2
})

const fooRef = toRef(state, 'foo'); // fooRef: {value: ...}

fooRef.value++
console.log(state.foo) // 2

state.foo++
console.log(fooRef.value) // 3
```

**toRefs**

把一个响应式对象的所有属性转换为ref格式，然后包装到一个`plain-object`中返回

```js
const state = reactive({
  foo: 1,
  bar: 2
})

const stateAsRefs = toRefs(state)
/*
stateAsRefs: not a proxy
{
  foo: { value: ... },
  bar: { value: ... }
}
*/
```

应用：

```js
setup(){
  const state1 = reactive({a:1, b:2});
  const state2 = reactive({c:3, d:4});
  return {
    ...state1, // lost reactivity
    ...state2 // lost reactivity
  }
}

setup(){
  const state1 = reactive({a:1, b:2});
  const state2 = reactive({c:3, d:4});
  return {
    ...toRefs(state1), // reactivity
    ...toRefs(state2) // reactivity
  }
}
// composition function
function usePos(){
  const pos = reactive({x:0, y:0});
  return pos;
}

setup(){
  const {x, y} = usePos(); // lost reactivity
  const {x, y} = toRefs(usePos()); // reactivity
}
```

# 降低心智负担

所有的`composition function`均以`ref`的结果返回，以保证`setup`函数的返回结果中不包含`reactive`或`readonly`直接产生的数据

```js
function usePos(){
  const pos = reactive({ x:0, y:0 });
  return toRefs(pos); //  {x: refObj, y: refObj}
}
function useBooks(){
  const books = ref([]);
  return {
    books // books is refObj
  }
}
function useLoginUser(){
  const user = readonly({
    isLogin: false,
    loginId: null
  });
  return toRefs(user); // { isLogin: refObj, loginId: refObj }  all ref is readonly
}

setup(){
  // 在setup函数中，尽量保证解构、展开出来的所有响应式数据均是ref
  return {
    ...usePos(),
    ...useBooks(),
    ...useLoginUser()
  }
}
```

> 面试题：composition api相比于option api有哪些优势？

不同于reactivity api，composition api提供的函数很多是与组件深度绑定的，不能脱离组件而存在。

# setup

```js
// component
export default {
  setup(props, context){
    // 该函数在组件属性被赋值后立即执行，早于所有生命周期钩子函数
    // props 是一个对象，包含了所有的组件属性值
    // context 是一个对象，提供了组件所需的上下文信息
  }
}
```

context对象的成员

| 成员  | 类型 | 说明                    |
| ----- | ---- | ----------------------- |
| attrs | 对象 | 同`vue2`的`this.$attrs` |
| slots | 对象 | 同`vue2`的`this.$slots` |
| emit  | 方法 | 同`vue2`的`this.$emit`  |

# 生命周期函数

| vue2 option api | vue3 option api       | vue 3 composition api           |
| --------------- | --------------------- | ------------------------------- |
| beforeCreate    | beforeCreate          | 不再需要，代码可直接置于setup中 |
| created         | created               | 不再需要，代码可直接置于setup中 |
| beforeMount     | beforeMount           | onBeforeMount                   |
| mounted         | mounted               | onMounted                       |
| beforeUpdate    | beforeUpdate          | onBeforeUpdate                  |
| updated         | updated               | onUpdated                       |
| beforeDestroy   | ==改== beforeUnmount  | onBeforeUnmount                 |
| destroyed       | ==改==unmounted       | onUnmounted                     |
| errorCaptured   | errorCaptured         | onErrorCaptured                 |
| -               | ==新==renderTracked   | onRenderTracked                 |
| -               | ==新==renderTriggered | onRenderTriggered               |

新增钩子函数说明：

| 钩子函数        | 参数          | 执行时机                       |
| --------------- | ------------- | ------------------------------ |
| renderTracked   | DebuggerEvent | 渲染vdom收集到的每一次依赖时   |
| renderTriggered | DebuggerEvent | 某个依赖变化导致组件重新渲染时 |

DebuggerEvent:

- target: 跟踪或触发渲染的对象
- key: 跟踪或触发渲染的属性
- type: 跟踪或触发渲染的方式

# 面试题参考答案

面试题：composition api相比于option api有哪些优势？

> 从两个方面回答：
>
> 1. 为了更好的逻辑复用和代码组织
> 2. 更好的类型推导

```
有了composition api，配合reactivity api，可以在组件内部进行更加细粒度的控制，使得组件中不同的功能高度聚合，提升了代码的可维护性。对于不同组件的相同功能，也能够更好的复用。
相比于option api，composition api中没有了指向奇怪的this，所有的api变得更加函数式，这有利于和类型推断系统比如TS深度配合。
```

# vuex方案

安装`vuex@4.x`

两个重要变动：

- 去掉了构造函数`Vuex`，而使用`createStore`创建仓库
- 为了配合`composition api`，新增`useStore`函数获得仓库对象

# global state

由于`vue3`的响应式系统本身可以脱离组件而存在，因此可以充分利用这一点，轻松制造多个全局响应式数据

<img src="http://mdrs.yuanjin.tech/img/20201026171519.png" alt="image-20201026171519761" style="zoom:50%;" />

```js
// store/useLoginUser 提供当前登录用户的共享数据
// 以下代码仅供参考
import { reactive, readonly } from "vue";
import * as userServ from "../api/user"; // 导入api模块
// 创建默认的全局单例响应式数据，仅供该模块内部使用
const state = reactive({ user: null, loading: false });
// 对外暴露的数据是只读的，不能直接修改
// 也可以进一步使用toRefs进行封装，从而避免解构或展开后响应式丢失
export const loginUserStore = readonly(state);

// 登录
export async function login(loginId, loginPwd) {
  state.loading = true;
  const user = await userServ.login(loginId, loginPwd);
  state.loginUser = user;
  state.loading = false;
}
// 退出
export async function loginOut() {
  state.loading = true;
  await userServ.loginOut();
  state.loading = false;
  state.loginUser = null;
}
// 恢复登录状态
export async function whoAmI() {
  state.loading = true;
  const user = await userServ.whoAmI();
  state.loading = false;
  state.loginUser = user;
}
```



# Provide&Inject

在`vue2`中，提供了`provide`和`inject`配置，可以让开发者在高层组件中注入数据，然后在后代组件中使用

<img src="http://mdrs.yuanjin.tech/img/20201026173949.png" alt="image-20201026173949874" style="zoom: 40%;" />

除了兼容`vue2`的配置式注入，`vue3`在`composition api`中添加了`provide`和`inject`方法，可以在`setup`函数中注入和使用数据

<img src="http://mdrs.yuanjin.tech/img/20201026174039.png" alt="image-20201026174039594" style="zoom:40%;" />

考虑到有些数据需要在整个vue应用中使用，`vue3`还在应用实例中加入了`provide`方法，用于提供整个应用的共享数据

```js
creaetApp(App)
  .provide("foo", ref(1))
  .provide("bar", ref(2))
	.mount("#app");
```

<img src="http://mdrs.yuanjin.tech/img/20201026174611.png" alt="image-20201026174611477" style="zoom:40%;" />

因此，我们可以利用这一点，在整个vue应用中提供共享数据

```js
// store/useLoginUser 提供当前登录用户的共享数据
// 以下代码仅供参考
import { readonly, reactive, inject } from "vue";
const key = Symbol(); // Provide的key

// 在传入的vue应用实例中提供数据
export function provideStore(app) {
  // 创建默认的响应式数据
  const state = reactive({ user: null, loading: false });
  // 登录
  async function login(loginId, loginPwd) {
    state.loading = true;
    const user = await userServ.login(loginId, loginPwd);
    state.loginUser = user;
    state.loading = false;
  }
  // 退出
  async function loginOut() {
    state.loading = true;
    await userServ.loginOut();
    state.loading = false;
    state.loginUser = null;
  }
  // 恢复登录状态
  async function whoAmI() {
    state.loading = true;
    const user = await userServ.whoAmI();
    state.loading = false;
    state.loginUser = user;
  }
  // 提供全局数据
  app.provide(key, {
    state: readonly(state), // 对外只读
    login,
    loginOut,
    whoAmI,
  });
}

export function useStore(defaultValue = null) {
  return inject(key, defaultValue);
}

// store/index
// 应用所有store
import { provideStore as provideLoginUserStore } from "./useLoginUser";
// 继续导入其他共享数据模块...
// import { provideStore as provideNewsStore } from "./useNews"

// 提供统一的数据注入接口
export default function provideStore(app) {
  provideLoginUserStore(app);
  // 继续注入其他共享数据
  // provideNewsStore(app);
}

// main.js
import { createApp } from "vue";
import provideStore from "./store";
const app = createApp(App);
provideStore(app);
app.mount("#app");

```

# 对比

|              | vuex | global state | Provide&Inject |
| ------------ | ---- | ------------ | -------------- |
| 组件数据共享 | ✅    | ✅            | ✅              |
| 可否脱离组件 | ✅    | ✅            | ❌              |
| 调试工具     | ✅    | ❌            | ✅              |
| 状态树       | ✅    | 自行决定     | 自行决定       |
| 量级         | 重   | 轻           | 轻             |

# Pinia基本概念

>面试题：Pinia 相比 Vuex 有什么样的优点？为什么现在官方推荐使用 Pinia ？

Pinia，是一个 Vue 阵营的新的状态管理库，现在 Vue 官方已经推荐使用 Pinia 来代替 Vuex，或者你可以把 Pinia 看作是 Vuex 的最新的版本。

- Pinia 的基本介绍
- Pinia 优势



## Pinia 的基本介绍

Pinia 是一个西班牙语的单词，表示“菠萝”的意思。因为菠萝是由一小块一小块组成的，这个和 Pinia 的思想就非常的吻合，在 Pinia 中，每个 Store 仓库都是单独的扁平化的存在的。

Pinia 是由 Vue 官方团队中的一个成员开发的，最早是在 2019 年 11 左右作为一项实验性工作所提出的，当时的目的是将组合 API 融入到 Vuex 中，探索新版本的 Vuex 应有的形态，随着探索的进行，最终发现 Pinia 已经实现了 Vuex5 大部分的提案，因此 Pinia 就作为了最新版本的 Vuex，但是为了尊重作者本人，名字保持不变，仍然叫做 Pinia。

相比 Vuex，Pinia 的 API 更少而且更简单，还支持组合式 API，还可以和 Typescript 一起使用来做类型的推断。

pinia 官网：https://pinia.vuejs.org/

<img src="https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2023-03-21-093840.png" alt="image-20230321173840739" style="zoom:50%;" />



## Pinia 优势

1. 在 Pinia 中，已经不存在 mutations，只有 state、getters、actions

```js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore('counter',{
  state: () => ({
    count: 0
  }),
  getters: {
    doubleCount: state => state.count * 2
  },
  actions: {
    increment() {
      this.count++
    },
  }
})

```

在上面的代码中，我们创建了一个仓库，该仓库中提供三个选项，分别是 state、getters 以及 actions。



2. actions 里面支持同步和异步来修改 store，相当于将之前 Vuex 中的 mutation 和 action 合并了

```js
import { defineStore } from 'pinia'

export const useCounterStore = defineStore({
  // ...
  actions: {
    // 同步的修改仓库状态
    increment() {
      this.count++
    },
    decrement() {
      this.count--
    },
    // 异步的修改仓库状态
    async incrementAsync() {
      await new Promise(resolve => setTimeout(resolve, 1000))
      this.increment()
    },
    async decrementAsync() {
      await new Promise(resolve => setTimeout(resolve, 1000))
      this.decrement()
    }
  }
})
```



3. 可以和 TypeScript 一起使用，以此来获得类型推断的支持

```js
import { defineStore } from 'pinia'

// 这里定义了一个名为 Todo 的接口
interface Todo {
  id: number;
  text: string;
  done: boolean;
}

export const useTodoStore = defineStore({
  id: 'todo',
  state: () => ({
    todos: [] as Todo[],
  }),
  getters: {
    completedTodos: state => state.todos.filter(todo => todo.done),
  },
  actions: {
    // text 指定了是 string 类型
    addTodoItem(text: string) {
      const id = state.todos.length + 1
      const newTodo = { id, text, done: false }
      state.todos.push(newTodo)
    },
    // todo 指定了是 Todo 类型
    toggleTodoItem(todo: Todo) {
      todo.done = !todo.done
    },
    async fetchTodos() {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos')
      const todos = await response.json() as Todo[]
      state.todos = todos
    },
  },
})
```



4. 关于 Store 仓库，每一个 Store 仓库都是独立的扁平化的存在的，不再像 Vuex 里面是通过 modules 嵌套
5. 支持插件扩展，可以通过插件（函数）来扩展仓库的功能，为仓库添加全局属性或者全局方法

```js
// ...
// 这里定义了一个名为 localStoragePlugin 的插件，本质上就是一个函数
const localStoragePlugin = (context: PiniaPluginContext) => {
  const key = 'my-app-state'

  // 从 localStorage 中恢复状态
  context.state = localStorage.getItem(key) || context.state

  // 监听 state 变化，将变化保存到 localStorage
  context.subscribe((mutation) => {
    localStorage.setItem(key, context.state)
  })
}
// ...

// 创建 Pinia 实例，并注册 localStoragePlugin 插件
const pinia = createPinia()
pinia.use(localStoragePlugin)
```



6. 更加轻量，压缩之后体积只有 1kb 左右，基本上可以忽略这个库的存在



## 真题解答

> 题目：Pinia 相比 Vuex 有什么样的优点？为什么现在官方推荐使用 Pinia ？
>
> 参考答案：
>
> Pinia 是由 Vue.js 团队成员开发的下一代状态管理仓库，相比 Vuex 3.x/4.x，Pinia 可以看作是 Vuex5 版本。
>
> Pinia 具有如下的优势：
>
> - mutations 不复存在。只有 state 、getters 、actions。
>
> - actions 中支持同步和异步方法修改 state 状态。
>
> - 与 TypeScript 一起使用具有可靠的类型推断支持。
>
> - 不再有模块嵌套，只有 Store 的概念，Store 之间可以相互调用。
>
> - 支持插件扩展，可以非常方便实现本地存储等功能。
>
> - 更加轻量，压缩后体积只有 1kb 左右。

# Pinia快速入门

> 面试题：是否使用过 Pinia？简单谈一下 Pinia 的使用？



## 安装 Pinia

首先第一步，需要安装 Pinia，可以通过下面的命令进行安装：

```js
npm install pinia
```

安装完毕后，需要在 Vue 应用中挂载 Pinia

```js
import { createPinia } from "pinia";
// 创建 pinia 实例
const pinia = createPinia();
createApp(App).use(router).use(pinia).mount("#app");
```

在 src 目录下面创建仓库目录 store，在该目录下面创建对应的仓库文件，注意名字一般是 useXXXStore

在仓库文件中，我们可以通过 defineStore 来创建一个 pinia 仓库，如下：

```js
// 仓库文件
import { defineStore } from "pinia";

// 第二个参数支持两种风格：options api 以及 composition api
export const useCounterStore = defineStore("counter", {
  state: () => {
    return {
      num: 0,
    };
  },
});
```

创建的时候支持两种风格，选项式 API 以及组合式 API。



## 选项式风格

该风格基本上和之前的 Vuex 是非常相似的，只不过没有 mutation 了，无论是同步的方法还是异步的方法，都写在 actions 里面。

```js
// 仓库文件
import { defineStore } from "pinia";

// 第二个参数支持两种风格：options api 以及 composition api
export const useCounterStore = defineStore("counter", {
  state: () => {
    return {
      num: 0,
    };
  },
  getters: {
    // 针对上面 state 的数据做一个二次计算
    // 可以看作是计算属性
    doubleCount: (state) => state.num * 2,
  },
  actions: {
    // 同步方法
    increment() {
      this.num++;
    },
    decrement() {
      this.num--;
    },
    // 异步方法
    async asyncIncrement() {
      // 等待 1 秒钟
      await new Promise((resolve) => setTimeout(resolve, 1000));
      this.increment();
    },
    async asyncDecrement() {
      await new Promise((resolve) => setTimeout(resolve, 1000));
      this.decrement();
    },
  },
});

```

在组件中使用仓库数据时，首先引入仓库方法，并执行该方法：

```js
import { useCounterStore } from "@/store/useCounterStore.js";
const store = useCounterStore(); // 拿到仓库
```

如果是要获取数据，为了保持数据的响应式，应该使用 storeToRefs 方法。

```js
import { storeToRefs } from "pinia";
// 接下来我们可以从仓库中解构数据出来
const { num, doubleCount } = storeToRefs(store);
```

如果是获取方法，直接从 store 里面解构出来即可。

```js
// 从仓库将方法解构出来
const { increment, asyncIncrement, asyncDecrement } = store;
```



另外，仓库还提供了两个好用的 api：

- store.$reset ：重置 state
- store.$patch：变更 state



## 真题解答

> 题目：是否使用过 Pinia？简单谈一下 Pinia 的使用？
> 参考答案：

# 添加插件

>面试题：是否给 Pinia 添加过插件？具体添加的方式是什么？

在 Pinia 中，我们可以为仓库添加插件，通过添加插件能够扩展以下的内容：

- 为 store 添加新的属性
- 定义 store 时增加新的选项
- 为 store 增加新的方法
- 包装现有的方法
- 改变甚至取消 action
- 实现副作用，如[本地存储](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)
- **仅**应用插件于特定 store



## 自定义插件

首先建议插件单独拿一个目录来存放，一个插件就是一个方法：

```js
export function myPiniaPlugin1() {
  // 给所有的仓库添加了一条全局属性
  return {
    secret: "the cake is a lie",
  };
}

export function myPiniaPlugin2(context) {
  //   console.log(context);
  const { store } = context;
  store.test = "this is a test";
}

/**
 * 给特定的仓库来扩展内容
 * @param {*} param0
 */
export function myPiniaPlugin3({ store }) {
  if (store.$id === "counter") {
    // 为当前 id 为 counter 的仓库来扩展属性
    return {
      name: "my name is pinia",
    };
  }
}

/**
 * 重置仓库状态
 */
export function myPiniaPlugin4({ store }) {
  // 我们首先可以将初始状态深拷贝一份
  const state = deepClone(store.$state);
  store.reset = () => {
    store.$patch(deepClone(state));
  };
}
```

每个插件在扩展内容时，会对所有的仓库进行内容扩展，如果想要针对某一个仓库进行内容扩展，可以通过 context.store.$id 来指定某一个仓库来扩展内容。

插件书写完毕后，需要通过 *pinia* 实例对插件进行一个注册操作。

```js
// 引入自定义插件
import {
  myPiniaPlugin1,
  myPiniaPlugin2,
  myPiniaPlugin3,
  myPiniaPlugin4,
} from "./plugins";

pinia.use(myPiniaPlugin1);
pinia.use(myPiniaPlugin2);
pinia.use(myPiniaPlugin3);
pinia.use(myPiniaPlugin4);
```



## 添加第三方插件

有一些第三方插件，直接通过 npm 安装使用即可。

具体的使用方法一定要参阅文档。



## 真题解答

>题目：是否给 Pinia 添加过插件？具体添加的方式是什么？
>参考答案：
>
>在 Pinia 中可以非常方便的添加插件。一个插件就是一个函数，该函数接收一个 context 上下文对象，通过 context 对象可以拿到诸如 store、app 等信息。
>
>每个插件在扩展内容时，会对所有的仓库进行内容扩展，如果想要针对某一个仓库进行内容扩展，可以通过 context.store.$id 来指定某一个仓库来扩展内容。
>
>插件书写完毕后，需要通过 *pinia* 实例对插件进行一个注册操作。
>
>另外，我们还可以使用一些第三方插件，直接通过 npm 安装使用即可。安装完毕后，使用方法和自定义插件是一样的，具体的使用方法一定要参阅文档。

# 最佳实践与补充内容

> 面试题：在目前的 Vue 应用中，使用状态管理库进行状态管理时有哪些最佳实践？请列举一至两条



## 最佳实践

- 分离状态逻辑和业务逻辑

实际上这个就是我们使用状态管理库的目的，我们使用状态管理库，就是为了将组件的状态分离出来，这样可以方便我们维护，也方便组件之间进行状态的共享。

没有使用状态管理库：

<img src="https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2022-11-04-023144.png" alt="image-20221104103143856" style="zoom:50%;" />

使用状态管理库之后：

<img src="https://xiejie-typora.oss-cn-chengdu.aliyuncs.com/2022-11-04-023459.png" alt="image-20221104103459131" style="zoom:50%;" />

但是需要注意一点，并非所有的 Vue 应用都需要使用状态管理库，这个取决于我们所开发的应用的规模大小。如果只是小规模的 Vue 应用，使用状态管理库反而显得更麻烦。



- 选择 Pinia 来进行状态管理

目前 Vue 官方已经推荐开发者使用 Pinia 来替代 Vuex 作为状态管理库，你可以将 Pinia 看作是 Vuex5.x

相比 Vuex，Pinia 真的真的真的很轻量，大小只有 1kb 左右，基本上可以忽略

当然相比之前的 Vuex，还有一些其他的优点：

https://pinia.vuejs.org/zh/introduction.html#comparison-with-vuex

另外如果你之前的项目使用的是 Vuex，那么你可以看一下官方的迁移指南：

https://pinia.vuejs.org/zh/cookbook/migration-vuex.html



- 避免直接操作 store 的状态

虽然我们可以直接操作 store 的状态，但是在 Pinia 中我们最好还是避免直接操作 store 里面的状态，而是通过对应的 getters 来读取，actions 来修改

```html
<!-- 计数器-->
<button class="btn" @click="num++">+</button>
```

```js
// 待办事项
function addHandle() {
  if (newItem.value) {
    console.log(list.value.items);
    // 直接操作 store 的状态
    list.value.items.push({
      text : newItem.value,
      isCompleted: false,
    });
    newItem.value = "";
  } else {
    window.alert("请填写新增项目");
  }
}
```

与其对应的应该使用 getters 和 actions 等 API 来处理状态的读取和修改

```html
<button class="btn" @click="increment">+</button>
```

```js
function addHandle() {
  if (newItem.value) {
    addItem(newItem.value);
    newItem.value = "";
  } else {
    window.alert("请填写新增项目");
  }
}
```

这样做的好处在于提高了代码的可维护性，应该数据的改变始终来自于 actions 的方法，而不是分散于组件的各个部分。



- 使用 TypeScript

Pinia 本身就是使用 typescript 编写的，因此我们在使用 pinia 的时候，能够非常方便的、非常自然的使用 typescript，使用 typescript 可以更好的提供类型检查和代码提示，让我们的代码更加可靠和易于维护。

官方文档对应：https://pinia.vuejs.org/zh/core-concepts/state.html#typescript



- 将状态划分为多个模块

在一个大型应用中，如果将所有组件的状态放置在一个状态仓库中，那么会显得该状态仓库非常的臃肿。因此一般在大型项目中，是一定会将状态仓库进行拆分的。

在早期的 Vuex 中，就已经支持将状态仓库按照不同的功能模块进行拆分，只不过在 Vuex 时期，状态仓库拆分时按照的是嵌套的方式进行代码组织的。

在 Pinia 中，组织状态仓库的形式不再采用像 Vuex 一样的嵌套，而是采用的是扁平化的设计，每一个状态仓库都是独立的，这个其实也是 Pinia 这个名字的来源。



## 补充内容

- 辅助函数
- 订阅 state 以及 action
- 插件选项



## 真题解答

> 题目：在目前的 Vue 应用中，使用状态管理库进行状态管理时有哪些最佳实践？请列举一至两条
>
> 参考答案：
>
> 在使用 Vue 开发应用时，有关组件的状态管理这一块，有如下的最佳实践：
>
> - 使用专门的状态仓库来管理组件状态，以达到状态逻辑和业务逻辑的分离
> - 比起 Vuex，目前更推荐使用 Pinia 来管理仓库的状态
> - 尽量都集中使用 actions 中的方法来操作 store 的状态，避免直接操作 store
> - 使用 typescript 以便得到更好的类型提示
> - 根据不同的功能模块来创建对应的独立的状态仓库

# Pinia部分源码解析

养成阅读源码的习惯，有如下的好处：

- 阅读源码可以帮助我们扩宽自己的视野，可以看到优秀的程序员是如何书写代码的，从而提升我们自己的编码水平
- 知其然知其所以然。如果你阅读过源码，那么你自然能够知道某一个 API 是如何实现，背后的实现原理是什么，那么你也就能够自然的避免在使用该 API 时可能会遇到的一些 bug，会有一些自己独特的优化心得
- 最后一点就是阅读源码能够冲击大厂，大厂在面试的时候不会考察某个 API 如何使用，没什么意义，因为 API 经常也在变化，一般都是考察 API 背后的原理



阅读源码时的一些注意事项

- 阅读源码基于你已经使用过了该库或者该框架，对里面的 API 已经很熟悉了，是一种自发的行为
- 阅读源码一定要**耐心**
- 不要**陷入于细节**，在阅读源码的时候往往需要你站在一个更高的角度



## defineStore 方法

回顾 defineStore 方法的使用。defineStore 方法支持两种变成风格，一种是 option store，另一种是 setup store

option store 风格：

```js
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0 }),
  getters: {
    double: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++
    },
  },
})
```

option store 风格可以将 id 写到选项里面：

```js
export const useCounterStore = defineStore({
  id: 'counter',
  state: () => ({ count: 0 }),
  getters: {
    double: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++
    },
  },
})
```

setup store 风格：

```js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  function increment() {
    count.value++
  }

  return { count, increment }
})
```

defineStore 对应的源码如下：

```js
function defineStore(
// TODO: add proper types from above
idOrOptions, setup, setupOptions) {
    let id;
    let options;
    // isSetupStore 会是一个布尔值，如果是 setup 函数，isSetupStore 为 true，否则为 false
    const isSetupStore = typeof setup === 'function';
    if (typeof idOrOptions === 'string') {
        // 如果进入此 if，说明 idOrOptions 是该仓库的 id
        // id 是 defineStore 函数内部的变量，存储仓库 id
        id = idOrOptions;
        // the option store setup will contain the actual options in this case
        // 如果是 setup 风格，就将第三个参数（如果有）赋值给 options，否则就将配置对象赋值给 options
        options = isSetupStore ? setupOptions : setup;
    }
    else {
        // idOrOptions 参数为配置对象
        options = idOrOptions;
        id = idOrOptions.id;
    }
    // 这个函数就是最终返回给外部的函数
    // 外部通过执行这个函数拿到 store 仓库 
    function useStore(pinia, hot) {
        const currentInstance = getCurrentInstance();
        pinia =
            // in test mode, ignore the argument provided as we can always retrieve a
            // pinia instance with getActivePinia()
            (pinia) ||
                (currentInstance && inject(piniaSymbol, null));
        if (pinia)
            setActivePinia(pinia);
        if (!activePinia) {
            throw new Error(`[🍍]: getActivePinia was called with no active Pinia. Did you forget to install pinia?\n` +
                `\tconst pinia = createPinia()\n` +
                `\tapp.use(pinia)\n` +
                `This will fail in production.`);
        }
        pinia = activePinia;
        if (!pinia._s.has(id)) {
            // creating the store registers it in `pinia._s`
            // 创建一个仓库，并且将这个仓库注册到 pinia._s
            // 根据不同的风格开始创建仓库
            if (isSetupStore) {
                // 如果是 setup 风格，调用的是 createSetupStore
                createSetupStore(id, setup, options, pinia);
            }
            else {
                // 如果是 option 风格，调用的是 createOptionsStore
                // createOptionsStore 方法背后实际上也是在调用 createSetupStore，内部会创建一个名为 setup 的函数
                // 将选项转为 setup 函数内部的项目，然后调用 createSetupStore 方法，将 setup 函数作为第二个参数传递过去
                // 因此理论上来讲，setup 实践上要更加高效一些，因为 option store 背后也是转为 setup，这些是你不阅读源码无法知道的
                createOptionsStore(id, options, pinia);
            }
            /* istanbul ignore else */
            {
                // @ts-expect-error: not the right inferred type
                useStore._pinia = pinia;
            }
        }
        const store = pinia._s.get(id);
        if (hot) {
            const hotId = '__hot:' + id;
            const newStore = isSetupStore
                ? createSetupStore(hotId, setup, options, pinia, true)
                : createOptionsStore(hotId, assign({}, options), pinia, true);
            hot._hotUpdate(newStore);
            // cleanup the state properties and the store from the cache
            delete pinia.state.value[hotId];
            pinia._s.delete(hotId);
        }
        // save stores in instances to access them devtools
        if (IS_CLIENT &&
            currentInstance &&
            currentInstance.proxy &&
            // avoid adding stores that are just built for hot module replacement
            !hot) {
            const vm = currentInstance.proxy;
            const cache = '_pStores' in vm ? vm._pStores : (vm._pStores = {});
            cache[id] = store;
        }
        // StoreGeneric cannot be casted towards Store
        return store;
    }
    useStore.$id = id; // 在 useStore 函数上面还挂了一个 $id，存储了该仓库的 id
    return useStore; // 在向外部返回这个函数
}
```



## storeToRefs 方法

首先我们还是回顾该方法的用法：

```vue
<script setup>
import { storeToRefs } from 'pinia'
const store = useCounterStore()
const { name, doubleCount } = storeToRefs(store)
const { increment } = store
</script>
```

源码如下：

```js
function storeToRefs(store) {
    // See https://github.com/vuejs/pinia/issues/852
    // It's easier to just use toRefs() even if it includes more stuff
    // 针对 Vue2 版本的处理
    if (isVue2) {
        // @ts-expect-error: toRefs include methods and others
        return toRefs(store);
    }
    else {
        store = toRaw(store);
        // 创建了一个空对象
        const refs = {};
        // 遍历仓库对象
        for (const key in store) {
            // 拿到仓库对象对应的每一项的值
            const value = store[key];
            if (isRef(value) || isReactive(value)) {
                // @ts-expect-error: the key is state or getter
                // 如果这个值本身是响应式的，将这个值以原本的 key 添加到 refs 对象上面
                refs[key] =
                    // ---
                    toRef(store, key);
            }
        }
        // 整个 for 循环完了之后，所有响应式的值被添加到了 refs 对象上面
        // 向外部返回这个 refs 对象
        return refs;
    }
}
```

