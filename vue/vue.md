# Vue核心：

## Vue简介：

- 什么是vue？

一套用于构建用户界面的渐进式JavaScript框架

渐进式：vue可以自底向上逐层的应用

- vue特点：

1）采用组件化模式，提高代码复用率、且让代码更好维护

2）声明式编码，让编码人员无需直接操作DOM，提高开发效率

3）使用虚拟DOM+优秀的Diff算法

## 初始Vue：

1、想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象

2、root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法

3、root容器里的代码被称为【Vue模板】

4、Vue实例和容器是一一对应的

5、真是开发中只有一个Vue实例，并且会配合着组件一起使用

6、{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性

7、一旦data中的数据发生变化，那么模板中用到该数据的地方也会自动更新

注意区分：

1、表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方

- a
- a+b
- demo(1)
- x === y ? 'a' : 'b'

2、js代码(语句)：

- if(){}
- for(){}

## 模板语法：

Vue模板语法有2大类：

1、插值语法：

功能：用于解析标签体内容

写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性

2、指令语法：

功能：用于解析标签（包括：标签属性、标签体内容、绑定事件...）

举例：v-bind:href="xxx" 或 简写为 :href="xxx"，xxx同样要写js表达式，且可以直接读取到data中的所有属性

备注：Vue中有很多的指令，且形式都是v-???

## 数据绑定：

Vue有2种绑定方式：

1、单向绑定（v-bind）：数据只能从data流向页面；简写为	：

2、双向绑定（v-model）：数据不仅能从data流向页面，还可以从页面流向data；简写为 v-model

备注：

双向绑定一般都应用在表单类元素上（如：input、select等）

v-model：value可以简写为v-model，因为v-model默认收集的就是value值

## el与data的两种写法：

注意：由Vue管理的函数，一定不要用箭头函数，一旦写了箭头函数，this就不再是Vue实例了

```JavaScript
  <script>
    Vue.config.productionTip = false //阻止vue在启动时生成生产提示

    //el两种写法
    // const v = new Vue({
    //   // el: '#root',//第一种写法
    //   data: {
    //     name: 'wss'
    //   }
    // })
    // console.log(v);
    // v.$count('root');//第二种写法

    // data的两种写法
    const v = new Vue({
      el: '#root',
      // data第一种写法：对象式
      // data: {
      //   name: 'wss'
      // }
      // data第二种写法:函数式
      data() {
        return {
          name: 'wss'
        }
      }
    })
  </script>
```

## MVVM模型：

M：模型（Model）：对应data中的数据

V：视图（View）：模板

VM：试图模型（ViewModel）：Vue实例对象

![image-20220121112019664](https://github.com/Web-Wss/notes/blob/main/vue/image-20220121112019664.png)

## 数据代理：

- 回顾Objecr.defineProperty：

```javascript
  <script>
    let number = 18;
    let person = {
      name: '张三',
      sex: '男'
    }

    Object.defineProperty(person, 'age', {
      // value: 18,
      // enumerable: true,//控制属性是否可以枚举，默认false
      // writable: true,//控制属性是否可以被修改，默认false
      // configurable: true,//控制属性是否可以被删除，默认false
      // 当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age值
      get() {
        console.log('有人读取了age属性');
        return number
      },
      // 当有人读取person的age属性时，set函数(setter)就会被调用，且返回值就是age值
      set(value) {
        console.log('有人修改了value属性，且值是:', value);
        number = value;
      }
    })
    // console.log(Object.keys(person));
    // for (let key in person) {
    //   console.log(key);
    // }
    console.log(person);
  </script>
```

- 数据代理：

通过一个对象代理对另一个对象中属性的操作（读/写）

```javascript
  <script>
    let obj = { x: 100 }
    let obj2 = { y: 200 }
    Object.defineProperty(obj2, 'x', {
      get() {
        return obj.x
      },
      set(value) {
        obj.x = value
      }
    })
  </script>
```

## Vue中的数据代理：

![image-20220121231121820](https://github.com/Web-Wss/notes/blob/main/vue/image-20220121231121820.png)

1、Vue中的数据代理：

通过一个对象代理对另一个对象中属性的操作（读/写）

2、Vue中数据代理的好处：

更加方便的操作data中的数据

3、基本原理：

通过Object.defineProperty()把data对象中所有属性添加到VM上

为每一个添加到VM上的属性，都指定一个getter/setter

在getter/setter内部去操作（读/写）data中对应的属性

## 事件处理：

1、使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名

2、事件的回调需要配置在methods对象中，最终会在VM上

3、methods中配置的函数，不要用箭头函数，否则this就不是VM了

4、methods中配置的函数，都是被Vue所管理的函数，this的指向是VM或组件实例对象

5、@click="demo" 和 @click="demo($event)"效果一致，但后者可以传参

```javascript
<body>
  <div id="root">
    <h2>欢迎来到{{name}}</h2>
    <button v-on:click="showInfo1">点我提示信息</button>
    <button @click="showInfo2($event, 66)">点我提示信息</button>
  </div>

  <script>
    Vue.config.productionTip = false //阻止vue在启动时生成生产提示

    new Vue({
      el: '#root',
      data: {
        name: '安徽'
      },
      methods: {
        showInfo1() {
          // console.log(event.target.innerText);
          console.log(this);//此处的this是VM
          console.log('你好！');
        },
        showInfo2(event, number) {
          console.log(event, number);
          console.log('你好！！');
        }
      }
    })
  </script>
</body>
```

### Vue中事件修饰符：

修饰符可以连续写

1、prevent：阻止默认事件（常用）

2、stop：阻止冒泡事件（常用）

3、once：事件只触发一次（常用）

4、capture：使用事件的捕获模式

5、self：只有event.target是当前操作的元素时才触发事件

6、passive：事件的默认行为立即执行，无需等待事件回调执行完毕

### 键盘事件：

Vue中常用的按键别名：

- 回车 =>enter
- 删除 =>delete（捕获“删除”和“退格”键）
- 退出=>esc
- 空格=>space
- 换行=>tab
- 上=>up
- 下=>down
- 左=>left
- 右=>right

Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名）

系统修饰键（用法特殊）：ctrl、alt、shift、meta

1、配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发

2、配合keydown使用：正常触发事件

也可以使用keyCode去指定具体的按键（不推荐）

Vue.config.keyCodes.自定义键名 = 键码，可以去制定按键别名

## 计算属性与监视：

定义：要用的属性不存在，要通过已有属性计算得来

原理：底层接住了Object.defineproperty方法提供的getter和setter

get函数什么时候执行？

- 初次读取时会执行一次
- 当依赖的数据发生变化时会被再次调用

优势：与methods实现相比，内部有缓存机制（复用），效率更高，调式方便

备注：1、计算属性最终会出现再VM上，直接读取使用即可

​			2、如果计算属性要修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变

```javascript
  <script>
    Vue.config.productionTip = false;

    const VM = new Vue({
      el: '#root',
      data: {
        firstName: '张',
        lastName: '三'
      },
      computed: {
        fullName: {
          // get有什么作用？当有人读取fullName，get就会被调用，且返回值就作为fullName的值
          // get什么时候调用？1、初次读取fullName时。2、所依赖的数据发生变化时
          get() {
            console.log('get被调用了');
            return this.firstName + '-' + this.lastName
          },
          set(value) {
            const arr = value.split('-');
            this.firstName = arr[0];
            this.lastName = arr[1];
          }
        }
      }
    })
  </script>
```

- 监视属性watch：

1、当被监视的属性变化时，回调函数自动调用，进行相关操作

2、监视的属性必须存在，才能进行监视

3、监视的两种写法：

new Vue时传入watch配置

通过VM.$watch监视

- 深度监测：

1、Vue中的watch默认不监测对象内部值的改变（一层）

2、配置deep：true可以监测对象内布置改变（多层）

备注：

1、Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以

2、使用watch时根据数据的具体结构，决定是否采用深度监视

```javascript
watch: {
        // 正常写法
        // isHot: {
        //   // immediate: true,//初始化时让handler调用一下
        //   // deep: true,//深度监视
        //   handler(newValue, oldValue) {
        //     console.log(newValue, oldValue);
        //   }
        // },
        // 简写
        isHot(newValue, oldValue) {
          console.log(newValue, oldValue);
        }
      }
```

## computed和watch之间的区别：

1、computed能完成的功能，watch都可以完成

2、watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作

两个重要的小原则：

1、所被Vue管理的函数，最好写成普通函数，这样this的指向才才是VM或组件实例对象

2、所有不被Vue所管理的函数（定时器的回调、ajax的回调函数等、promise的回调函数），最好写成箭头函数，这样this的指向才是VM或组件实例对象

## class与style绑定：

```javascript
<body>
  <div id="root">
    <!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
    <div class="basic" :class="mood" @click="changeMood">{{name}}</div><br /><br />
    <!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定，名字也不确定 -->
    <div class="basic" :class="classArr">{{name}}</div><br /><br />
    <!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
    <div class="basic" :class="classObj">{{name}}</div>
    <!-- 绑定style样式--对象写法 -->
    <div class="basic" :style="styleObj">{{name}}</div>
    <!-- 绑定style样式--数组写法 -->
    <div class="basic" :style="styleArr">{{name}}</div>
  </div>

  <script>
    Vue.config.productionTip = false

    new Vue({
      el: '#root',
      data: {
        name: 'wss',
        mood: 'normal',
        classArr: ['y1', 'y2', 'y3'],
        classObj: {
          y1: false,
          y2: false
        },
        styleObj: {
          backgroundColor: 'orange'
        },
        styleArr: [
          {
            fontSize: '40px',
            color: 'red'
          }
        ]
      },
      methods: {
        changeMood() {
          const arr = ['happy', 'sad', 'normal'];
          const index = Math.floor(Math.random() * 3);
          this.mood = arr[index];
        }
      }
    })
  </script>
</body>
```

## 条件渲染：

template标签只能和v-if使用条件渲染

v-if：写法：

- v-if=“表达式”
- v-else-if=“表达式”
- v-else=“表达式”

适用于：切换频率较低的场景

特点：不展示DOM元素直接被移除

注意：v-if可以和v-else-if、v-else一起使用，但要求结构不能被打断

v-show：

- 写法：v-show=“表达式”
- 适用于：切换频率较高的场景
- 特点：不展示DOM元素未移除，仅仅是使用样式隐藏掉

备注：使用v-if时，元素可能无法获取到，而使用v-show一定可以获取到

```javascript
<body>

  <div id="root">
    <h2>当前的n值是：{{n}}</h2>
    <button @click="n++">点我n+1</button>
    <!-- 使用v-show做条件渲染 -->
    <!-- <h2 v-show="false">你好{{name}}</h2> -->
    <!-- <h2 v-show="1 === 1">你好{{name}}</h2> -->
    <!-- 使用v-if做条件渲染 -->
    <!-- <h2 v-if="false">你好{{name}}</h2> -->
    <!-- <h2 v-if="1 === 1">你好{{name}}</h2> -->
    <div v-if="n === 1">Angular</div>
    <div v-else-if="n === 2">React</div>
    <div v-else-if="n === 3">Vue</div>
    <!-- template标签只能和v-if使用条件渲染 -->
    <template v-if="n === 1">
      <h2>你好</h2>
      <h2>wss</h2>
      <h2>安徽</h2>
    </template>
  </div>
  <script>
    Vue.config.productionTip = false

    new Vue({
      el: '#root',
      data: {
        name: 'wss',
        n: 0
      }
    })
  </script>
</body>
```

## 列表渲染：

v-for指令：

- 用于展示列表数据
- 语法：v-for=“(item, index) in xxx” :key="yyy"
- 可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）

```javascript
<body>
  <div id="root">
    <!-- 遍历数组 -->
    <h2>人员列表</h2>
    <ul>
      <li v-for="(p, index) in persons" :key="p.id">
        {{index}}={{p.name}}-{{p.age}}
      </li>
    </ul>
    <!-- 遍历对象 -->
    <h2>汽车信息</h2>
    <ul>
      <li v-for="(val, k) in car" :key="k">
        {{k}}-{{val}}
      </li>
    </ul>
    <!-- 遍历字符串 -->
    <h2>遍历字符串</h2>
    <ul>
      <li v-for="(char, index) in str" :key="index">
        {{char}}-{{index}}
      </li>
    </ul>
    <!-- 遍历指定次数 -->
    <h2>遍历指定次数</h2>
    <ul>
      <li v-for="(number, index) in 5" :key="index">
        {{number}}-{{index}}
      </li>
    </ul>
  </div>
  </div>

  <script>
    Vue.config.productionTip = false

    new Vue({
      el: '#root',
      data: {
        persons: [
          { id: '001', name: '张三', age: 18 },
          { id: '002', name: '李四', age: 19 },
          { id: '003', name: '王五', age: 20 }
        ],
        car: {
          name: '奥迪',
          price: '70万',
          color: '黑色'
        },
        str: 'Hello'
      }
    })
  </script>

</body>
```

## key:

react、vue中的key有什么作用？（key的内部原理）

1、虚拟DOM中key的作用：

key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】，随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：

2、对比规则：

- 旧虚拟DOM中找到了与新虚拟DOM相同的key：
  - 若虚拟DOM中内容没变，直接使用之前的真实DOM
  - 若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面之前的真实DOM
- 旧虚拟DOM中未找到与新虚拟DOM相同的key：
  - 创建新的真实DOM，随后渲染到页面

3、用index做为key可能会引发的问题：

- 若对象进行：逆序添加、逆序删除等破坏顺序操作会产生没有必要的真实DOM更新==>界面效果每问题，但效率低
- 如果结构中还包含输入类DOM：会产生错误DOM更新==>界面有问题

4、开发中如何选择key？

- 最好使用每条数据的唯一标识作为key，比如：id、手机号、身份证号、学号等唯一值
- 如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表展示，使用index作为key是没有问题的

## 列表过滤：

```JavaScript
<body>
  <div id="root">
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入名字" v-model="keyWord">
    <ul>
      <li v-for="(p, index) in filPersons" :key="p.id">
        {{p.name}}-{{p.age}}-{{p.sex}}
      </li>
    </ul>
  </div>
  </div>

  <script>
    Vue.config.productionTip = false

    // 用watch实现
    //#region 
    // new Vue({
    //   el: '#root',
    //   data: {
    //     keyWord: '',
    //     persons: [
    //       { id: '001', name: '马冬梅', age: 18, sex: '女' },
    //       { id: '002', name: '周冬雨', age: 19, sex: '女' },
    //       { id: '003', name: '周杰伦', age: 20, sex: '男' },
    //       { id: '004', name: '温兆伦', age: 22, sex: '男' }
    //     ],
    //     filPersons: []
    //   },
    //   watch: {
    //     keyWord: {
    //       immediate: true,
    //       handler(val) {
    //         this.filPersons = this.persons.filter((p) => {
    //           return p.name.indexOf(val) != -1
    //         })
    //       }
    //     }
    //   }
    // })
    //#endregion
    // 用computed实现
    new Vue({
      el: '#root',
      data: {
        keyWord: '',
        persons: [
          { id: '001', name: '马冬梅', age: 18, sex: '女' },
          { id: '002', name: '周冬雨', age: 19, sex: '女' },
          { id: '003', name: '周杰伦', age: 20, sex: '男' },
          { id: '004', name: '温兆伦', age: 22, sex: '男' }
        ],
      },
      computed: {
        filPersons() {
          return this.persons.filter((p) => {
            return p.name.indexOf(this.keyWord) !== -1
          })
        }
      }

    })
  </script>

</body>
```

## 列表升序降序：

```JavaScript
computed: {
        filPersons() {
          const arr = this.persons.filter((p) => {
            return p.name.indexOf(this.keyWord) !== -1
          })
          // 判断是否排序
          if (this.sortType) {
            arr.sort((p1, p2) => {
              return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
            })
          }
          return arr;
        }
      }
```

## 收集表单数据：

若：\<input type="text">，则v-model收集的是value值，用户输入的就是value值

若：\<input type="text">，则v-model收集的是value值，且要给标签配置value值

若：\<input type="checkbox">

​	1、没有配置input的value值，那么收集的就是checked

​	2、配置input的value属性：

​		1、v-model的初始值是非数组，那么收集的就是checked

​		2、v-model的初始值是数组，那么收集的就是value组成的数组

备注：v-model的三个修饰符：

- lazy：失去焦点再收集数据
- number：输入字符串转为有效的数字
- trim：输入首尾空格过滤

```JavaScript
<body>
  <div id="root">
    <form @submit.prevent="demo">
      账号：<input type="text" v-model.trim="userInfo.account"><br />
      密码：<input type="password" v-model="userInfo.password"><br />
      年龄<input type="number" v-model.number="userInfo.age"><br />
      性别：<br />
      男：<input type="radio" name="sex" v-model="userInfo.sex" value="man">
      女：<input type="radio" name="sex" v-model="userInfo.sex" value="feman"><br />
      爱好：
      学习<input type="checkbox" v-model="userInfo.hobby" value="study">
      打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
      吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat"><br />
      所属校区：
      <select v-model="userInfo.city">
        <option value="">请选择校区</option>
        <option value="beijing">北京</option>
        <option value="shanghai">上海</option>
        <option value="shenzhen">深圳</option>
        <option value="wuhan">武汉</option>
      </select><br />
      其他信息：
      <textarea v-model.lazy="userInfo.other"></textarea><br />
      <input type="checkbox" v-model="userInfo.agree">同意并接受<a href="http://www.atguigu.com">《用户协议》</a>
      <button>提交</button>
    </form>
  </div>
  <script>
    Vue.config.productionTip = false

    new Vue({
      el: '#root',
      data: {
        userInfo: {
          account: '',
          password: '',
          age: '',
          sex: 'feman',
          hobby: [],
          city: 'beijing',
          other: '',
          agree: ''
        }
      },
      methods: {
        demo() {
          console.log(JSON.stringify(this.userInfo));
        }
      }
    })
  </script>

</body>
```

## Vue实例生命周期：

## 过度&动画：

## 过滤器：

定义：对要显示的数据进行待定格式化后再显示（适用于一些简单逻辑的处理）

语法：1、注册过滤器：Vue.filter(name,callback)或new Vue{filters: {}}

​			2、使用过滤器：{{xxx | 过滤器名}} 或 v-bind：属性 = “xxx | 过滤器名”

备注：1、过滤器也可以接受额外参数、多个过滤器也可以串联

​			2、并没有改变原本的数据，是产生新的对应的数据

```javascript
<body>
  <div id="root">
    <h2>显示格式化后的时间</h2>
    <!-- 计算属性实现 -->
    <h3>现在是：{{fmtTime}}</h3>
    <!-- methods实现 -->
    <h3>现在是：{{getFmtTime()}}</h3>
    <!-- 过滤器实现 -->
    <h3>现在是：{{time | timeformater}}</h3>
    <!-- 过滤器实现（传参） -->
    <h3>现在是：{{time | timeformater('YYYY-MM-DD') | mySlice}}</h3>
  </div>

  <script>
    Vue.config.productionTip = false

    const VM = new Vue({
      el: '#root',
      data: {
        time: 1642916963338//时间戳
      },
      computed: {
        fmtTime() {
          return dayjs(this.time).format('YYYY年-MM月-DD日 HH:mm:ss')
        }
      },
      methods: {
        getFmtTime() {
          return dayjs(this.time).format('YYYY年-MM月-DD日 HH:mm:ss')
        }
      },
      filters: {
        timeformater(value, str = "YYYY年MM月DD日 HH:mm:ss") {
          return dayjs(value).format(str)
        },
        mySlice(value) {
          return value.slice(0, 4)
        }
      }
    })
  </script>

</body>
```

## 内置指令与自定义指令：

内置指令：

- v-bind：单向绑定解析表达式，可以简写为 :xxx
- v-model：双向数据绑定
- v-for：遍历数组/对象/字符串
- v-on：绑定事件监听，可简写为@
- v-if：条件渲染（动态控制节点是否存在）
- v-else：条件渲染（动态控制节点是否存在）
- v-show：条件渲染（动态控制节点是否展示）
- v-text：
  - 作用：向其所在的节点中渲染文本内容
  - 与插值语法的区别：v-text会替换掉节点的内容，{{xxx}}则不会
- v-html：
  - 作用：可以解析html标签，向其所在的节点中渲染文本
- v-cloak：没有值
  - 作用：当网速过慢的时候，未经解析的模板不会再页面上显示
  - 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性
  - 使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题

- v-once：

v-ocne所在节点在初次动态渲染后，就视为静态内容了

以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能

- v-pre：
  - 跳过其所在节点的编译过程
  - 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译

## 自定义插件：

一、定义语法：

（1）局部指令：

new Vue({

​	directives:{指令名:配置对象}

})

或

new Vue({

​	directives{指令名:回调函数}

})

（2）全局指令：

Vue.directive(指令名，配置对象)

或

Vue.directive(指令名，回调函数)

二、配置对象中常用的3个问题：

（1）.bind：指令与元素成功绑定时调用

（2）.inserted：指令所在元素被插入页面时调用

（3）.update：指令所在模板结构被重新解析时调用

三：备注：

1、指令定义时不加v-，但使用时要加v-

2、指令名如果是多个单词，要使用aa-bb命名方式，不要使用aaBb命名

## 生命周期：

![Vue生命周期](https://github.com/Web-Wss/notes/blob/main/vue/Vue%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)

1、又名：生命周期回调函数、生命周期函数、生命周期钩子

2、是生命：Vue在关键时刻帮我们调用了一些特殊名称的函数

3、生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的

4、生命周期函数中的this指向是VM或组件实例对象

### 生命周期流程：

vm的一生（vm的生命周期）：

- 将要创建：调用beforeCreate函数
- 创建完毕：调用created函数
- 将要挂载：调用beforeMounte函数
- 挂在完毕（重要）：调用mounted函数=========>重要的钩子
- 将要更新：调用beforeUodate函数
- 更新完毕：调用updated函数
- 将要销毁：调用beforeDestroy函数=========>重要的钩子
- 销毁完毕：调用destroyed函数

### 总结：

常用的生命周期钩子：

1.mounted：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】

2.beforeDestroy：清除定时器、解除自定义事件、取消订阅消息等【收尾工作】

关于销毁Vue实例：

1.销毁后借助Vue开发者哦工具看不到任何信息

2.销毁后自定义事件会消失，但原生DOM事件依然有效

3.一般不会再beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了

# Vue组件化编程：

组件的定义：实现应用中局部功能代码和资源的集合

### 非单文件组件：

一个文件中包含有n个组件

- Vue中使用组件的三大步骤：

一、定义组件（创建组件）

二、注册组件

三：使用组件（写组件标签）

- 如何定义一个组件：

使用Vue.extend(options)创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别：区别如下：

1.el不要写，为什么？——最终所有的组件都要经过一个vm的管理，由vm中的el决定服务于哪个容器

2.data必须写成函数，为什么？——避免组件被复用时，数据存在引用关系

备注：使用template可以配置组件结构

- 如何注册组件：

1.局部注册：靠new Vue的时候传入components选项

2.全局注册：靠Vue.component('组件名',组件)

- 编写组件标签：

<school></school>

### 几个注意点:

1.关于组件名：

- 一个单词组成：

第一种写法（首字母小写）：school

第二种写法（首字母大写）：School

- 多个单词组成：

第一种写法（kebab-case命名）：my-school

第二种写法（CamelCase命名）：mySchool（需要Vue脚手架支持）

- 备注：

（1）组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行

（2）可以使用name配置项指定组件在开发者工具中呈现的名字

2.关于组件的标签：

第一种写法：<school></school>

第二种写法：<school/>

备注：不使用脚手架时，<school/>会导致后续组件不能渲染

3.一个简写方式：

const school = Vue.extend(option)，可简写为：const school = options

### VueComponent：

1.school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的

2.我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，即Vue会帮我们执行的：new VueComponent(options)

3.特别注意：每次调用Vue.extend，返回的都是一个全新的VueComponent!!!

4.关于this指向：

（1）组件配置中：

data函数、methods中的函数、watch中的函数、computed中的函数，他们的this均是【VueComponent实例对象】

（2）new Vue(option)配置中：

data函数、methods中的函数、watch中的函数、computed中的函数，他们的this均是【Vue实例】

5.VueComponent的实例对象，以后简称vc（也可称为组件实例对象）

### Vue实例与组件实例：

![image-20220222230217759](https://github.com/Web-Wss/notes/blob/main/vue/image-20220222230217759.png)

### 单文件组件：

一个文件中只包含有1个组件

```vue
<template>
<!-- 组件的结构 -->
  <div class="demo">
    <h2>学校名称:{{name}}</h2>
    <h2>学校地址:{{address}}</h2>
    <button @click="showName">点我提示学校名</button>
  </div>
</template>


<script>
    export default {
      name:'School',
      data() {
        return {
          name: '安师大',
          address: '安徽'
        }
      },
      methods: {
        showName() {
          alert(this.name)
        }
      },  
    }
</script>


<style>
/* 组件的样式 */
  .demo{
    background-color: orange;
  }
  
</style>
```

# 使用Vue脚手架：

## 创建vue脚手架

第一步（仅第一次执行）：全局安装@vue/cli

```
npm install -g @vue/cli
```

第二步：切换到你要创建项目的目录，然后使用命令创建目录

```
vue create xxx
```

第三步：启动项目

```
npm run serve
```

备注：如出现下载缓慢请配置npm淘宝镜像：

```
npm config set registry https://registry.npm.taobao.org
```

## 分析脚手架结构：

- node_modules

- public
  - favicon.ico：页签图标
  - index.html：主页面

- src
  - assets：存放静态资源
    - login.png
  - component：存放组件
    - HelloWorld.vue
  - App.vue：汇总所有组件
  - main.js：入口文件

- .gitignore：git版本管制

- babel.config.js：babel的配置文件

- package-lock.json：包版本控制文件

- package.json：应用包配置文件

- README.md：应用描述文件

## render函数：

关于不同版本的Vue

1.vue.js与vue.runtime.xxx.js区别：

（1）vue.js是完整版的vue，包含：核心功能+模板解析器

（2）vue.runtime.xxx.js是运行版的vue，只包含：核心功能，没有模板解析器

2.因为vue.runtime.xxx.js没有模板解析器，所以不能使用template配置项，需要使用render函数接收到的createElement函数去指定具体内容

## 修改默认配置：

使用vue inspect > output.js可以查看到Vue脚手架的默认配置

使用vue.config.js可以对脚手架进行个性化定制

https://cli.vuejs.org/zh

## ref属性：

被用来给元素或子组件注册应用信息（id的替代者）

应用在html标签上获取的是真实DOM元素，应用在组件标签上的是组件实例对象（vc）

使用方式：

- 打标识：<h1 ref="xxx">...</h1>或<School ref="xxx"></School>
- 获取：this.$refs.xxx

## props配置：

功能：让组件接收外部传过来的数据

（1）传递数据

<Demo name="xxx">

（2）接收数据

第一种方式（只接收）：

props:['name']

第二种方式（限制类型）：

props: {

​	name: Number

}

第三种方式（限制类型、限制必要性、指定默认值）：

props:{

​	name: {

​		type:String,//类型

​		required: true,//必要性

​		default:'老王'//默认值	

​	}

}

备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确定需要修改，那么复制props的内容到data一份，然后去修改data中的数据

## mixin混入：

功能：可以把多个组件公用的配置提取成一个混入对象

使用方式：

第一步定义混合：例如：

{

​	data(){...},

​	methods:{...}

​	...

}

第二步使用全局混入：例如：

（1）全局混入：Vue.mixin(xxx)

（2）局部混入：mixins:['xxx']

## 插件：

功能：用于增强Vue

本质：包含install方法的一个对象，install的第一个参数是Vue，第二个参数是插件使用者传递的数据

定义插件：
对象.install = function(Vue,options) {

​	//1.添加全局过滤器

​	Vue.filter(...)

}

使用插件：Vue.use()

## scoped样式：

作用：让样式在局部生效，防治冲突

写法：<style scoped>

## 案例：Todo-List

mian.js：

```js
// 引入Vue
import Vue from "vue";
// 引入App
import App from "./App.vue";
// 引入插件
import plugins from "./plugins";
// 关闭Vue生产提示
Vue.config.productionTip = false;

// 使用插件
Vue.use(plugins);

// 创建vm
new Vue({
  el: "#app",
  render: (h) => h(App),
});

```

App.vue：

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <MyHeader :addTodo="addTodo" />
        <MyList
          :todos="todos"
          :checkTodo="checkTodo"
          :deleteTodo="deleteTodo"
        />
        <MyFooter
          :todos="todos"
          :checkAllTodo="checkAllTodo"
          :clearAllTodo="clearAllTodo"
        />
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from "./components/MyHeader.vue";
import MyList from "./components/MyList.vue";
import MyFooter from "./components/MyFooter.vue";
export default {
  name: "App",
  components: {
    MyHeader,
    MyList,
    MyFooter,
  },
  data() {
    return {
      todos: [
        { id: "001", title: "抽烟", done: true },
        { id: "002", title: "喝酒", done: false },
        { id: "003", title: "开车", done: true },
      ],
    };
  },
  methods: {
    // 添加一个todo
    addTodo(todoObj) {
      this.todos.unshift(todoObj);
    },
    // 勾选or取消一个todo
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if (todo.id === id) todo.done = !todo.done;
      });
    },
    // 删除一个todo
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id !== id;
      });
    },
    // 全选or全不选
    checkAllTodo(done) {
      this.todos.forEach((todo) => {
        todo.done = done;
      });
    },
    // 清除所有已经完成的todo
    clearAllTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.done;
      });
    },
  },
};
</script>

<style scoped>
/*base*/
body {
  background: #fff;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>

```

MyHeader.vue：

```vue
<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
  name: 'MyHeader',
  props:['addTodo'],
  data() {
    return {
      title: ''
    }
  },
  methods: {
    add() {
      if (!this.title.trim()) return alert('输入不能为空')
      // 将用户的输入包装成为一个todo对象
      const todoObj = {id:nanoid(),title:this.title,done:false}
      // console.log(todoObj);
      this.addTodo(todoObj)
      this.title = ''
    }
  },

}
</script>

<style scoped>
  
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}

</style>
```

MyList.vue：

```vue
<template>
  <ul class="todo-main">
    <MyItem
      v-for="todoObj in todos"
      :key="todoObj.id"
      :todo="todoObj"
      :checkTodo="checkTodo"
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import MyItem from "./MyItem.vue";
export default {
  name: "MyList",
  components: { MyItem },
  props: ["todos", "checkTodo", "deleteTodo"],
};
</script>

<style scoped>
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>

```

MyItem.vue：

```vue
<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="todo.done"
        @change="handleCheck(todo.id)"
      />
      <span>{{ todo.title }}</span>
    </label>
    <button class="btn btn-danger" @click="HandleDelete(todo.id)">删除</button>
  </li>
</template>

<script>
export default {
  name: "MyItem",
  // 声明接收todo对象
  props: ["todo", "checkTodo", "deleteTodo"],
  methods: {
    handleCheck(id) {
      // 通知App组件将相应的todo对象的done值取反
      this.checkTodo(id);
    },
    HandleDelete(id) {
      if (confirm("确定删除吗？")) {
        this.deleteTodo(id);
      }
    },
  },

  // mounted() {
  //   console.log(this.todo);
  // }
};
</script>

<style scoped>
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

li:hover {
  background-color: #ddd;
}

li:hover button {
  display: block;
}
</style>

```

MyFooter.vue：

```vue
<template>
  <div class="todo-footer" v-show="total">
    <label>
      <!-- <input type="checkbox" :checked="isAll" @change="checkAll" /> -->
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["todos", "checkAllTodo", "clearAllTodo"],
  computed: {
    total() {
      return this.todos.length;
    },
    doneTotal() {
      return this.todos.filter((todo) => todo.done == true).length;
    },
    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0;
      },
      set(value) {
        this.checkAllTodo(value);
      },
    },
  },
  methods: {
    // checkAll(e) {
    //   // console.log(e.target.checked);
    //   this.checkAllTodo(e.target.checked);
    // },
    clearAll() {
      this.clearAllTodo();
    },
  },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2),
    0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}
</style>

```

1.组件化编码流程（通用）：

（1）拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突

（2）实现动态组件：考虑好数据存放的位置，数据是一个组件在用，还是一些组件在用

1.一个组件在用：放在组件自身即可

2.一些组件在用，放在他们公共的父组件上（状态提升）

（3）实现交互：从绑定事件开始

2.props适用于：

（1）父组件==》子组件 通信

（2）子组件==》父组件 通信（要求父组件先给子组件一个函数）

3.使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的

4.props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做

## webStorage：

1.存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

2.浏览器通过Window.sessionStorage和Window.localStorage属性来实现本地存储机制

3.相关API：

```
xxxxxStorage.setItem('key','value');
```

该方法接收一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值

```
xxxxxStorage.getItem('person');
```

该方法接收一个键名作为参数，返回键名对应的值

```
xxxxxStorage.removeItem('key')
```

该方法接收一个键名作为参数，并把该键名从存储中删除

```
xxxxxStorage.clear()
```

该方法会清空存储中的所有数据

- 备注：

1.sessionStorage存储的内容会随着浏览器窗口的关闭而消失

2.LocalStorage存储的内容，需要手动清除才会消失

3.xxxxxStorage.getItem(xxx)如果xxx对应的value获取不到，那么getItem的返回值是null

4.JSON.parse(null)的结果依然是null

## 组件自定义事件：

1.一种组件间通信的方式，适用于：子组件===》父组件

2.使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（事件的回调在A中）

3.绑定自定义事件：

1.第一种方式，在父组件中：

```
<Demo @atguigu="test" />或<Demo v-on:atguigu="test" />
```

2.第二种方式，在父组件中：

```
<Demo ref="demo" />
......
mounted() {
	this.$refs.xxx.$on('atguigu',this.test)
}
```

3.若想让自定义事件只能触发一次，可以使用once修饰符，或$once方法

4.触发自定义事件：

```
this.$emit('atguigu',数据)
```

5.解绑自定义事件：

```
this.$off('atguigu')
```

6.组件上也可以绑定原生DOM事件，需要使用native修饰符

7.注意：通过

```
this.$refs.xxx.$on('atguigu',回调)
```

绑定自定义事件时，回调要么配置在methods中，要么用箭头函数，否则this指向会出问题

## 全局事件总线：

全局事件总线：（GolbalEventBus）

1.一种组件间通信的方式，适用于任意组件间通信

2.安装全局事件总线

```js
new Vue({
	...
	brforeCreate() {
	Vue.prototype.$bus = this//安装全局事件总线，$bus就是当前应用的vm
	}
})
```

3.使用事件总线：

1.接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的回调留在A组件自身

```js
methods() {
	demo(data) {...}
}
......
mounted() {
this.$bus.$on('xxx',this.demo)
}
```

2。提供数据：

```js
this.$bus.$emit('xxx'，数据)
```

4.最好在beforeDestroy钩子中，用$off解绑当前组件所用到的事件

## 消息订阅与发布：

1.一种组件间通信的方式，适用于任意组件间通信

2.使用步骤：

1.安装pubsub：`npm i pubsub-js`

2.引入：`import pubsub from 'pubsub-js'`

3.接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的回调留在A组件自身

```
methods() {
	demo(data) {}
}
......
mounted() {
	this.pid = pubsub.subscribe('xxx',this.demo)//订阅消息
}
```

4.提供数据：`pubsub.pulish('xxx',数据)`

5.最好在beforeDestroy钩子中，用`Pubsub.unsubscribe(pid)`去取消订阅

## nextTick：

1.语法：

```
this.$nextTick(回调函数)
```

2.作用：在下一次DOM更新结束后执行其指定的回调

3.什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行

# Vue中的ajax：

## vue脚手架配置代理：

方法一：在vue.config.js中添加如下配置：

```js
devServer:{
	proxy:"http://localhost:5000"
}
```

说明：

1.优点：配置简单，请求资源时直接发给前端8080即可

2.缺点：不能配置多个代理，不能灵活的控制是否走代理

3.工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器（优先匹配前端资源）

方法二：编写vue.config.js配置具体代理规则：

```js
module.exports = {
  devServer: {
    proxy: {
      '/api': {//匹配所有以'/api'开头的请求路径
        target: '<url>',//代理目标的基础路径
        ws: true,
        changeOrigin: true
      },
      '/foo': {
        target: '<other_url>'
      }
    }
  }
}
```

说明：

1.优点：可以配置多个代理，且可以灵活的控制请求是否走代理

2.缺点：配置略微繁琐，请求资源时必须加前缀

## 插槽：

1.作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于父组件==>子组件

2.分类：默认插槽、具名插槽、作用域插槽

3.使用方式：

1.默认插槽：

```vue
父组件：
<Category>
	<div>
        html结构1
    </div>
</Category>
子组件：
<template>
	<div>
        <slot>插槽默认内容...</slot>
    </div>
</template>

```

2.具名插槽：

```vue
父组件：
<Category>
	<template slot="center">
    	<div>
        	html结构1
    	</div>
    </template>
    <template slot="footer">
    	<div>
        	html结构2
    	</div>
    </template>
</Category>
子组件：
<template>
	<div>
        <slot name="center">插槽默认内容...</slot>
        <slot name="footer">插槽默认内容...</slot>
    </div>
</template>
```

3.作用域插槽：

1.理解：数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）

```vue
父组件：
<Category title="游戏">
      <template scope="{games}">
        <ul>
          <li v-for="(g, index) in games" :key="index">{{ g }}</li>
        </ul>
      </template>
    </Category>
    <Category title="游戏">
      <template scope="{games}">
        <ol>
          <li style="color: red" v-for="(g, index) in games" :key="index">
            {{ g }}
          </li>
        </ol>
      </template>
    </Category>
    <Category title="游戏">
      <template scope="{games}">
        <h4 v-for="(g, index) in games" :key="index">{{ g }}</h4>
      </template>
    </Category>
子组件：
<template>
  <div class="category">
    <h3>{{ title }}分类</h3>
    <!-- 定义一个插槽 -->
    <slot :games="games">我是一个默认值1</slot>
  </div>
</template>
<script>
export default {
  name: "Category",
  props: ["title"],
  data() {
    return {
      foods: ["火锅", "烧烤", "小龙虾", "牛排"],
      games: ["红色警戒", "穿越火线", "劲舞团", "超级玛丽"],
      films: ["《教父》", "《拆弹专家》", "《你好，李焕英》", "《哈利波特》"],
    };
  },
};
</script>
```

# vuex：

1.概念：

在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式管理（读/写），也是一种组件间通信的方式，且适用于任意组件

2.何时使用？

多个组件需要共享数据时

3.搭建vuex环境：

1.创建文件：src/store/index.js

```js
//该文件用于创建vuex中最为核心的store
// 引入vuex
import Vue from "vue";

import Vuex from "vuex";
Vue.use(Vuex);

// 准备actions-用于响应组件中的动作
const actions = {};
// 准备mutations-用于操作数据
const mutations = {};
// 准备state-用于存储数据
const state = {};

// 创建并暴露store
export default new Vuex.Store({
  actions,
  mutations,
  state,
});

```

mian.js

```js
// 引入store
import store from "./store/index";

new Vue({
  render: (h) => h(App),
  store,
  beforeCreate() {
    Vue.prototype.$bus = this;
  },
}).$mount("#app");

```

基本使用：

1.初始化数据、配置actions、配置mutations，操作文件store.js

```js
//该文件用于创建vuex中最为核心的store
// 引入vuex
import Vue from "vue";

import Vuex from "vuex";
Vue.use(Vuex);

// 准备actions-用于响应组件中的动作
const actions = {
  // jia(context, value) {
  //   console.log("actioins中的jia被调用了", context, value);
  //   context.commit("JIA", value);
  // },
  // jian(context, value) {
  //   context.commit("JIAN", value);
  // },
  jiaOdd(context, value) {
    if (context.state.sum % 2) {
      context.commit("JIA", value);
    }
  },
  jiaWait(context, value) {
    setTimeout(() => {
      context.commit("JIA", value);
    }, 500);
  },
};
// 准备mutations-用于操作数据
const mutations = {
  JIA(state, value) {
    console.log("mutations中的jia被调用了", state, value);
    state.sum += value;
  },
  JIAN(state, value) {
    state.sum -= value;
  },
};
// 准备state-用于存储数据
const state = {
  sum: 0, //当前的和
};

// 创建并暴露store
export default new Vuex.Store({
  actions,
  mutations,
  state,
});

```

Count.vue：

```vue
<template>
  <div>
    <h2>当前求和为: {{ $store.state.sum }}</h2>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>

<script>
export default {
  name: "Count",
  data() {
    return {
      n: 1, //用户选择的数字
    };
  },
  methods: {
    increment() {
      this.$store.commit("JIA", this.n);
    },
    decrement() {
      this.$store.commit("JIAN", this.n);
    },
    incrementOdd() {
      this.$store.dispatch("jiaOdd", this.n);
    },
    incrementWait() {
      this.$store.dispatch("jiaWait", this.n);
    },
  },
};
</script>

<style></style>

```

2.组件中读取vuex中的数据：$store.state.sum

3.组件中修改vuex中的数据：$store.dispatch('actions中的方法名',数据)或$store.commit('mutations中的方法',数据)

备注：若没有网络请求或其他业务，组件中也可以越过actions，即不写dispatch，直接编写commit

## gettersd的使用：

1.概念：当state中的数据需要经过加工后再使用时，可以使用getters加工

2.在store.js中追加getters配置

```js 
const getters = {
	bigSum(state) {
		return state.sum * 10
	}
}
//创建并暴露store
export default new Vuex.store({
	...
	getters
})
```

3.组件中读取数据：

```
$store.getters.bigSum
```

## 四个map方法：

1.mapState方法：用于帮助我们映射state中的数据为计算属性

```vue
computed: {
    // 借助mapState生成计算数学，从state中读取数据（数组写法）
    ...mapState(["sum", "school", "subject"]),
    // 借助mapState生成计算数学，从state中读取数据（对象写法）
     ...mapState({ sum: "sum", school: "school", subject: "subject" }),
}
```

2.mapGetters方法：用于帮助我们映射getters中的数据为计算属性

```

computed: {
    // 借助mapGetters生成计算数学，从Getters中读取数据（对象写法）
    ...mapGetters({ bigSum: "bigSum" }),
    //借助mapGetters生成计算数学，从Getters中读取数据（数组写法）
    ...mapGetters(["bigSum"]),
}
```

3.mapActionis方法：用于帮助我们生成与actions对话的方法，即包含$store.dispatch(xxx)的函数

```
computed: {
...mapMutations({ increment: "JIA", decrement: "JIAN" }),
}
```

4.mapMutations方法：用于帮助我们生成与mutations对话的方法，即：包含$store.commit(xxx)的函数

```
computed: {
...mapActions({ incrementOdd: "jiaOdd", incrementWait: "jiaWait" }),
}
```

## 模块化+命名空间：

1.目的：让代码更好维护，让多种数据分类更加明确

2.修改store.js：

```
const countAbout = {
	namespaced:true,//开启命名空间
	state:{x:1},
	mutations:{...},
	actions:{...},
	getters:{
		bigSum(state) {
			return state.sum * 10
		}
	}
}

const personAbout = {
	namespaced:true,//开启命名空间
	state:{...},
	mutations:{...},
	actions:{...}
}

const store = new Vuex.Store({
	modules:{
		countAbout,
		personAbout
	}
})
```

3.开启命名空间后，组件中读取state数据

```
//方式一：自己直接读取
this.$store.state.personAbout.list
//方式二：借助mapState读取
...mapState('countAbout',['sum','school','subject'])
```

4.开启命名空间后，组件中读取getters数据

```
//方式一：自己直接读取
this.$store.getters['personAbout/firstPersonName']
//方式二：借助mapGetters读取
...mapGetters('countAbout',['bigSum'])
```

5.开启命名空间后，组件中调用dispatch

```
//方式一：直接自己读取
this.$store.dispatch('personAbout/addPersonWang',person)
//方式二：借助mapActions
...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWiat:'jiaWait'})
```

6.开启命名空间后，组件中调用commit

```
//方式一：自己直接commit
this.$store.commit('personAbout/ADD_PERSON',person)
//方式二：借助mapMutations
...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'})
```

# vue-router：

vue的一个插件库，专门用来实现SPA应用

- 对SPA应用的理解：

1.单页Web应用（single page web application，SPA）

2.整个应用只有一个完整的页面

3.点击页面中的导航链接不会刷新页面，只会做页面的局部更新

4.数据需要通过ajax请求获取

- 什么是路由：

1.一个路由就是一组映射关系（key-value）

2.key为路径，value可能是function或component

- 路由分类：

1、后端路由：

1.理解：value是function，用于处理客户端提交的请求

2.工作过程：服务器接收到一个请求时，根据请求路径找到匹配的函数来处理请求，返回相应数据

2、前端路由：

1.理解：value是component，用于展示页面内容

2.工作过程：当浏览器的路径改变时，对应的组件就会显示

## 路由的基本使用：

1.按照vue-router，命令：npm i vue-router

2.应用插件：Vue.use(VueRouter)

3.编写router配置项

```
//引入VueRouter
import VueRouter from 'vue-router'
//引入路由组件
import About from '../components/About'
import Home from '../components/Home'

//创建router实例对象，去管理一组一组的路由规则
const router = new VueRouter({
	routes:[
		{
			path:'/about',
			component:About
		},
		{
			path:'/Home',
			component:Home
		},
	]
})
//暴露router
export default router
```

4.实现切换（active-class可配置高亮）

```
<router-link active-class="active" to="/about">About</router-link>
<router-link active-class="active" to="/home">Home</router-link>
```

5.指定展示位置

```
<router-view></router-view>
```

- 几个注意点：

1.路由组件通常存放在pages文件夹，一般组件通常放在components文件夹

2.通过切换，”隐藏“了的路由组件，默认是被销毁的，需要的时候再挂载进去

3.每个组件都有自己的$router，可以通过组件的$router属性获取到

## 嵌套路由：

1.配置路由规则，使用children配置项

```
routes:[
	{
		path:'/about',
		component:About,
	},
	{
		path:'/home',
		component:Home,
		children:[
			{
				path:'news',
				component:News
			},
			{
				path:'message',
				component:Message
			},
		]
	}
]
```

2.跳转（要写完整路径）

```
<router-link to:"/home/news">News</router-link>
```

## 路由传参：

路由的query参数

```vue
<!-- 跳转路由并携带query参数，to的字符串写法 -->
        <!-- <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">{{ -->
        <!-- 跳转路由并携带query参数，to的对象写法 -->
        <router-link
          :to="{
            path: '/home/message/detail',
            query: {
              id: m.id,
              title: m.title,
            },
          }"
          >{{ m.title }}</router-link>
```

## 命名路由：

1.作用：简化路由的跳转

2.如何使用：

1.命名：

```js
routes: [
    {
      name: "guanyu",
      path: "/about",
      component: About,
    }
]
```

2.简化跳转

```vue
<router-link :to="{name;'guanyu'}">跳转</router-link>
```

## params参数：

```js
{
          path: "message",
          component: Message,
          children: [
            {
              name: "xiangqing",
              path: "detail",
              component: Detail,
            },
          ],
        },
```

```vue
<router-link
          :to="{
            name: 'xiangqing',
            params: {
              id: 666,
              title: '你好啊',
            },
          }"
        >
          {{ m.title }}</router-link
        >
```

注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置

```
$route.params.id
$route.params.title
```

## 路由的props配置：

作用：让路由组件更方便的收到参数

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,
	// props的第一种写法，值为对象，该对象中的所有key-value都会以props的形式传给Detail组件
              // props: {
              //   a: 1,
              //   b: "hello",
              // },
              // props的第二种写法，值为布尔值，若布尔值为真，就会把该路由组件收到的所有params参数，以props的形式传给Detail组件
              // props: true,
              // props的第三种写法，值为函数，
              props($route) {
                return { id: $route.params.id, title: $route.params.title };
              },
}
```

## replace属性：

1、作用：控制路由跳转时操作浏览器历史记录的模式

2、浏览器的历史记录有两种写入方式：分别为push和replace，push是追加历史记录，replace是替换当前记录，路由跳转时候默认为push

3.、如何开启replace模式：`<router-link replace ...>News</router-link>`

## 编程式路由导航：

1、作用：不借助`<router-link>`实现路由跳转，让路由跳转更加灵活

2、具体编码：

```
this.$router.push({
	name:'xiangqing',
		params:{
			id:xxx,
			title:xxx
		}
})

this.$router.replace({
	name:'xiangqing',
		params:{
			id:xxx,
			title:xxx
		}
})
this.$router.forward()
this.$router.back()
this.$router.go(3)
```

## 缓存路由组件：

1、作用：让不展示的路由组件保持挂载，不被销毁

2、具体编码：

```
<keep-alive include="News">
	<router-view></router-view>
</keep-alive>
```

## 两个新的生命周期钩子：

1、作用：路由组件独有的两个钩子，用于捕获路由组件的激活状态

2、具体名字：

1.activeted：路由组件被激活时触发

2.deactiveted：路由组件失活时触发

## 路由守卫：

1、作用：对路由进行权限控制

2、分类：全局守卫、独享守卫、组件内守卫

3、全局守卫：

```
//全局前置守卫：初始化时执行，每次路由切换前执行
router.beforeEach((to,from,next)=> {
	if(to.meta.isAuth) {
		if(localStorage.getItem('school') === 'ASD') {
			next();
		}else {
			alert('学校名不匹配，无权查看')
		}
	}else {
		next()
	}
})

//全局后置守卫：初始化时执行、每次路由切换后执行
router.beforeEach((to,from)=> {
	if(to.meta.isAuth) {
			document.title = to.meta.title
		}else {
			document.title = 'vue_test'
		}
})
```

4、独享守卫：

```
beforeEnter(to,from,next) {
	if(to.meta.isAuth) {
		if(localStore.getItem('school') === 'ASD'){
			next()
		}else {
			alert('学校名不匹配')
		}
	}else {
		next()
	}
}
```

5、组件内守卫：

```
//进入守卫
beforeRouteEnter(to,from,next) {

}
//离开守卫
beforeRouteLeave(to,from,next) {

}
```

## 路由器的两种工作模式：

1、对于一个urI来说，什么是hash值？——#及其后面的内容就是hash值

2.hash值不会包含在http请求中，即：hash值不会带给服务器

3.hash模式：

1.地址中永远带着#，不美观

2.若以后将地址通过第三方手机app分享，若app严格校验，则地址会被标记为不合法

3.兼容性较好

4、history模式：

1、地址干净，美观

2、兼容性和hash模式相比略差

3、应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题

# Vue UI组件库：

移动端常用UI组件库

1、Vant：https://youzan.github.io/vant

2、Cube UI：https://didi.github.io/cube-ui

3、Mint UI：http://mint-ui.github.io

PC端常用UI组件库

1、Element UI：https://element.element.cn

2、IVew UI：https://www.iviewui.com
