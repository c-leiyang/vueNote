# Vue笔记

## HTTP状态码

### 状态码一般由3位构成：

1xx : 表示请求已经接受了，继续处理。
2xx : 表示请求已经处理掉了。
3xx : 重定向。
4xx : 一般表示客户端有错误，请求无法实现。
5xx : 一般为服务器端的错误。

### 比如常见的状态码：

200 OK 客户端请求成功。
301 Moved Permanently 请求永久重定向。
302 Moved Temporarily 请求临时重定向。
304 Not Modified 文件未修改，可以直接使用缓存的文件。
400 Bad Request 由于客户端请求有语法错误，不能被服务器所理解。
401 Unauthorized 请求未经授权，无法访问。
403 Forbidden 服务器收到请求，但是拒绝提供服务。服务器通常会在响应正文中给出不提供服务的原因。
404 Not Found 请求的资源不存在，比如输入了错误的URL。
500 Internal Server Error 服务器发生不可预期的错误，导致无法完成客户端的请求。
503 Service Unavailable 服务器当前不能够处理客户端的请求，在一段时间之后，服务器可能会恢复正常。

### Vue基础第一天

#### Vue概述

1. Vue 简述
① 2013年，还在 Google 工作的尤雨溪，受到 Angular 的启发，提取核心部分，开发出了一款轻量框架，同年12月，更名为Vue，
② 2014.01.24，Vue 正式对外发布
③ 2014.02.25，发布了一个重要版本，代号：Animatrix(黑客帝国)
④ 2015 年，Vue 使用数激增，实现了爆发式增长一系列看的推出，标志着 Vue从一个视图层库发展为一个渐进式框架，很多前端同学也是从这个版本开始成为Vue的用户
2015.06.13，发布了一个重要版本，代号：Dragon Ball(龙珠)，
2015.10.27，Vue 1.0.0 发布，代号：Evangelion (新世纪福音战士)  vue.js
2015.08.18，vue-router 发布
2015.11.28，vuex 发布 
2015.12.27，vue-cli 发布  脚手架
⑤ 2016 年 10 月 1号，Vue 2.0.0 发布，代号：Ghost in the Shell（攻壳机动队）,这次发布是 Vue 的第二个重要的里程碑，它吸收了React的Virtual Dom方案，还支持服务端渲染。
⑥ 3.0 预计会在 2020 年初进行发布，

2. 库和框架的区别
库：小而美，对一些常用的方法进行了封装，形成了一个新的方法进行使用 documen.xxxx , $('.')
框架: 大而全， 不仅提供了路由操作、还提供了数据的统一管理、同时还给提供了创建项目结构目录的库
使用框架，那么必须框架给提供的套路、方法来使用，否则，肯定有 bug

3. 什么是渐进式框架 ☆☆☆☆☆
声明式渲染 --> 组件系统 --> 客户端路由 --> 集中式状态管理 --> 项目构建
说白了：
  就是现在你已经有了一个应用项目，你可以在其中的一两个页面来使用 Vue, 带来更丰富的交互体验，
  但是如果是想在前端实现更多复杂的逻辑功能， Vue 的核心库和生态系统也可以满足相关业务的需求

4. Vue 技术栈(全家桶): vue、vue-router、vuex、vue-cli、axios  ☆☆☆☆☆

#### Vue的基本使用步骤

1. 创建需要Vue托管用于填充数据的容器
2. 引入Vue.js外部文件
3. 创建Vue的基础结构(el-->页面挂载的位置，就是指页面的哪一个部分需要Vue来托管[一般使用css选择器，也可以使用dom元素选择器];data-->代表页面需要使用的数据)
4. 使用插值表达式将数据展示在页面上

#### v-cloak指令

1. 为什要使用v-cloak指令？
   使用插值表达式渲染数据时会有闪动的问题，会先加载大花括号，然后再加载数据，如果页面上有很多差值表达式，就会影响用户体验
2. 原理
   vue底层如果发现页面上使用了v-cloak，那么就不会显示内容，直到页面数据全部渲染完成，才会在内存中将v-cloak替换成显示的内容

#### v-text、v-html、v-pre、v-once指令

1. v-text指令
   v-text指令用于将数据填充到标签中，作用和插值表达式类似，但是没有闪动的问题
   如果数据中含有HTML标签会将html标签一并输出
   注意：此处为单项绑定，数据对象上的值改变，插值会发生改变，但是当插值发生改变时不会影响数据对象上的值
2. v-html指令
   v-html指令用法和v-text相似，但是它可以将HTML片段填充到标签中
   可能有安全问题，一般只在可信任的内容是使用v-html，永不用在用户提交上
   v-html和v-text的区别在于，v-text只会输出纯文本，浏览器不会对其进行HTML解析，但v-html会将HTML解析后输出
3. v-pre(了解)
   v-pre指令会跳过编译过程，显示原始信息(原样输出，写什么输出什么)
4. v-once
   v-once指令显示内容后不再具有数据响应的功能(即当数据改变时，插值处的内容不会继续更新)
   应用场景：如果显示数据后不需要修改，可以使用v-once来提高性能

#### v-model指令(双向数据绑定)
    双向数据绑定：就是指当数据发生改变后，页面上的内容也会随之发生改变(当数据发生变化的时候，视图也就发生变化;当视图发生变化的时候，数据也会跟着同步变化)
    视图层 -- 就是页面的结构
    数据层 -- 就是 data 中的数据
    V-model 原理:就是使用v-bind绑定属性值，然后使用v-on:input时时监听input最新的值(实际上还有更底层原地，就是使用 ES5 里面的 Object.defineProperty)
    eg: <input type="text" v-bind:value="age" v-on:input="inputHandle">

#### MVVM ☆☆☆☆☆

1. MVVM 实际上是三个部分

  ① M --> model -- 数据
  ② V --> view  -- 视图
  ③ VM --> view model  --> 视图逻辑层

  面试题：

    MVVM ，指三层，M 是什么 ？ V 是什么？ VM 又是什么
    MVVM 只是前端一种设计思想，
    这种思路有什么优势呐 ？
    将网站开发进行分层，每层之间相互不影响，方法软件的迭代和后期的维护

#### Vue中绑定事件(v-on、v-bind)

1. v-on:click通过指令的方式绑定事件，简写方式:@click
   注意事项:v-on事件函数中传入参数
   a. 如果事件直接绑定函数名称，那么默认会传递事件对象作为事件函数的第一个参数
   eg: <button v-on:click="add">++</button>
       add: function (event) {
            console.log(event)
            console.log(event.target.innerHTML)
            // 这里的this是Vue的实例对象+
            console.log(this === vm)
            // 在函数中 想要使用data里面的数据 一定要加this 
            this.age++
        }
    b. 如果事件绑定函数调用，那么事件对象必须作为最后一个参数显示传递，并且事件对象的名称必须是$event
    eg: <button v-on:click="add2('1','2',$event)">++</button>
        add2: function (num1,mun2,event) {
            console.log(event)
            console.log(num1,mun2)
            console.log(event.target.innerHTML)
            console.log(event.target.tagName)
            // 这里的this是Vue的实例对象+
            console.log(this === vm)
            // 在函数中 想要使用data里面的数据 一定要加this 
            this.age++
        }

2. 事件修饰符
   阻止事件冒泡.stop
   eg: <button @click.stop="son">son</button>
   阻止事件默认行为.prevent
   eg: <a href="http://www.baidu.com" @click.prevent="baidu">baidu</a>
   为什么不推荐使用原生的阻止事件默认行为以及阻止事件冒泡?
   因为在Vue方法中主要是用来对数据进行处理，不推荐做一些DOM细节操作,而且：三大框架(vue/react/angular) 都不推荐对DOM进行操作，全部是数据驱动,也就是数据驱动视图更新，而不是使用DOM方法更新

3. 按键修饰符
   .enter =>    enter键
   eg: <input type="text" name="pwd" v-model="info" @keyup.enter="enterLogin">
   .delete (捕获“删除”和“退格”按键) =>  删除键
   eg: <input type="text" name="uname" v-model="uname" @keyup.delete="clearContent">

4. 自定义按键修饰符别名---在Vue中可以通过config.keyCodes自定义按键修饰符别名
   eg: <input type="text" v-model="msg" @keyup.a="keyContent">
       自定义按键修饰符， keyCodes 后面是自定义按键修饰符的名称，将键值码赋值给它就可以
       Vue.config.keyCodes.a = 65

5. v-bind指令 ☆☆☆
   v-bind指令被用来响应地更新HTML属性,v-bind:href可以简写为:href
   我们可以给v-bind:class 一个对象，以动态地切换class(注意：v-bind:class指令可以与普通的class特性共存)

I. v-bind绑定对象(如果绑定的是一个对象则 键 为对应的类名 值 为对应data中的数据)
   eg: <ul class="box" v-bind:class="{textColor:isColor, textSize:isSize}">
   data:{
      isColor:true,
      isSize:true，
    }
  HTML最终渲染为 <ul class="box textColor textSize"></ul>
   注意：textColor，textSize  对应的渲染到页面上的CSS类名;isColor，isSize对应vue data中的数据,如果为true则对应的类名渲染到页面上
   当 isColor 和 isSize 变化时，class列表将相应的更新(例如，将isSize改成false)
   class列表将变为 <ul class="box textColor"></ul>

II. v-bind绑定数组
   eg: <ul class="box" :class="[classA, classB]">
   data:{
        classA:‘textColor‘,
        classB:‘textSize‘
    }
    .textColor{
        color:#f00;
        background-color:#eef;
    }
    .textSize{
        font-size:30px;
        font-weight:bold;
    }
    数组中classA和 classB 对应为data中的数据(这里的classA对用data中的classA;这里的classB对用data中的classB)

III. 绑定对象和绑定数组的区别
    A:绑定对象的时候 对象的属性 即要渲染的类名 对象的属性值对应的是 data 中的数据
    B:绑定数组的时候数组里面存的是data 中的数据 

#### 分支结构(v-if)

1. v-if 使用场景
   A:多个元素 通过条件判断展示或者隐藏某个元素
   B:进行两个视图之间的切换

2. v-show和v-if的区别  ☆☆☆☆
  A:v-show本质就是标签display设置为none,控制隐藏(v-show只编译一次,后面其实就是控制css,而v-if不停的销毁和创建,故v-show性能更好一点)
  B:v-if是动态的向DOM树内添加或者删除DOM元素(v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件)

#### 循环结构(v-for)

v-for用于循环的数组里面的值可以是对象，也可以是普通元素
I、循环结构-遍历数组
  item是我们自己定义的一个名字代表数组里面的每一项;items对应的是data中的数组
  eg: <li v-for="(item, index) in items" :key="index">
        {{ item.message }}
      </li> 
      data: {
      items: [
          { message: 'Foo' },
          { message: 'Bar' }
        ]，
      }
  注意事项：
  A:不推荐同时使用v-if和v-for(当v-if与v-for一起使用时，v-for具有比v-if更高的优先级)
  B:key的作用(key来给每个节点做一个唯一标识;key的作用主要是为了高效的更新虚拟DOM)

II、循环结构-遍历对象
  v       代表对象的value
	k       代表对象的键 
	i       代表索引	
  eg: <div v-if='v==13' v-for='(v,k,i) in obj'>{{v + '---' + k + '---' + i}}</div>
  data: {
    obj: {
        uname: 'zhangsan',
        age: 13,
        gender: 'female'
    }
  }

### Vue基础第二天

#### Vue常用特性

1. 表单基本操作

I、通过v-model获取单选框中的值
  A:两个单选框需要同时通过v-model双向绑定一个值 
  B:每一个单选框必须要有value属性且value值不能一样 
  C:当某一个单选框选中的时候v-model会将当前的value值改变data中的数据
  gender 的值就是选中的值，我们只需要实时监控他的值就可以了
  eg: <input type="radio" id="male" value="1" v-model='gender'>
      <label for="male">男</label>
      <input type="radio" id="female" value="2" v-model='gender'>
      <label for="female">女</label>
      <script>
        new Vue({
          data: {
            // 默认会让当前的 value 值为 2 的单选框选中
              gender: 2,  
            },
        })
      </script>

II、通过v-model获取复选框中的值(复选框checkbox这种的组合时,data中的hobby我们要定义成数组,否则无法实现多选)
  A:复选框需要同时通过v-model双向绑定一个值
  B:每一个复选框必须要有value属性且value值不能一样 
  C:当某一个单选框选中的时候 v-model会将当前的value值改变(data中的数据)
  hobby 的值就是选中的值，我们只需要实时监控他的值就可以了
  eg: <div>
        <span>爱好：</span>
        <input type="checkbox" id="ball" value="1" v-model='hobby'>
        <label for="ball">篮球</label>
        <input type="checkbox" id="sing" value="2" v-model='hobby'>
        <label for="sing">唱歌</label>
        <input type="checkbox" id="code" value="3" v-model='hobby'>
        <label for="code">写代码</label>
      </div>
      <script>
        new Vue({
          data: {
            // 默认会让当前的 value 值为 2 和 3 的复选框选中
            hobby: ['2', '3'],
          },
        })
      </script>

III、通过v-model获取下拉框和文本框中的值
  A:需要给select  通过v-model 双向绑定 一个值 
  B:每一个option  必须要有value属性  且value 值不能一样 
  C:当某一个option选中的时候 v-model  会将当前的 value值 改变 data 中的 数据
  occupation 的值就是选中的值，我们只需要实时监控他的值就可以了
  eg: <!-- multiple  多选 -->
      <select v-model='occupation' multiple>
          <option value="0">请选择职业...</option>
          <option value="1">教师</option>
          <option value="2">软件工程师</option>
          <option value="3">律师</option>
      </select>
      <!-- textarea 是 一个双标签   不需要绑定value 属性的  -->
      <textarea v-model='desc'></textarea>
      <script>
        new Vue({
          data: {
            // 默认会让当前的 value 值为 2 和 3 的下拉框选中
            occupation: ['2', '3'],
            desc: 'nihao'
          },
        })
      </script>

2. 表单修饰符(.number/.trim/.lazy)
  .number: 转换为数值(当开始输入非数字的字符串时，因为Vue无法将字符串转换成数值;所以属性值将实时更新成相同的字符串。即使后面输入数字，也将被视作字符串)
  .trim: 自动过滤用户输入的首尾空白字符(只能去掉首尾的 不能去除中间的空格)
  .lazy: 将input事件切换成change事件(.lazy修饰符延迟了同步更新属性值的时机。即将原本绑定在input事件的同步逻辑转变为绑定在change事件上)[change事件失去焦点的时候触发，input事件有值输入的时候触发]
  eg: <!-- 自动将用户的输入值转为数值类型 -->
      <input v-model.number="age" type="number">
      <!--自动过滤用户输入的首尾空白字符   -->
      <input v-model.trim="msg">
      <!-- 在“change”时而非“input”时更新 -->
      <input v-model.lazy="msg">

3. 自定义指令

I、Vue.directive注册全局指令
    使用自定义的指令，只需在对用的元素中，加上'v-'的前缀形成类似于内部指令'v-if'，'v-text'的形式
    eg: <input type="text" v-focus>
    注意点:
    A: 在自定义指令中  如果以驼峰命名的方式定义 如  Vue.directive('focusA',function(){})
    B: 在HTML中使用的时候 只能通过 v-focus-a 来使用
    注册一个全局自定义指令 v-focus
    eg: Vue.directive('focus', {
          // 当绑定元素插入到 DOM 中,其中el为dom元素
          inserted: function (el) {
            // 聚焦元素
            el.focus();
          }
        });
        new Vue({
        　　el:'#app'
        });

II、Vue.directive注册全局指令带参数
   eg: <input type="text" v-color='msg'>
    <script type="text/javascript">
      //自定义指令-带参数
      //bind - 只调用一次，在指令第一次绑定到元素上时候调用
      Vue.directive('color', {  
        // bind声明周期, 只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置
        // el 为当前自定义指令的DOM元素  
        // binding 为自定义的函数形参   通过自定义属性传递过来的值 存在 binding.value 里面
        bind: function(el, binding){
          // 根据指令的参数设置背景色
          // console.log(binding.value.color)
          el.style.backgroundColor = binding.value.color;
        }
      });
      var vm = new Vue({
        el: '#app',
        data: {
          msg: {
            color: 'blue'
          }
        }
    });
    </script>

III、自定义指令局部指令
  注意事项:
  A:局部指令，需要定义在directives的选项,用法和全局用法一样 
  B:局部指令只能在当前组件里面使用
  C:当全局指令和局部指令同名时以局部指令为准
  eg: <input type="text" v-color='msg'>
      <input type="text" v-focus>
      <script type="text/javascript">
        var vm = new Vue({
          el: '#app',
          data: {
            msg: {
              color: 'red'
           }
          },
        //局部指令，需要定义在 directives 的选项
        directives: {
          color: {
            bind: function(el, binding){
              el.style.backgroundColor = binding.value.color;
            }
          },
          focus: {
            inserted: function(el) {
              el.focus();
            }
          }
        }
      });
      </script>

4. 计算属性(computed) ☆☆☆☆☆

I、为什么需要计算属性，什么是计算属性
  
  在模板中使用表达式非常的便捷，但是如果在其中写很多的逻辑代码，
  那么程序就会非常难以维护，
  插值表达式诞生的目的是做一些简单的运算，
  如果在里面写很多太复杂的逻辑，代码看起来非常冗余，缺少可读性

  所以：就提供了计算属性，
  目的：将表达式的代码进行提取，提取到计算属性中

II、计算属性的注意事项
  A: 在data同级，声明一个computed属性，它是一个对象
  B: 在对象中定义计算属性方法，是个 [方法]，函数
  C: 在方法内部，必须使用 return 返回结果
  D: 在使用计算属性的时候，不需要加括号
  E: 计算属性的值依赖与 data 中的数据
  eg: <div id="app">
        <p>{{ num + 1 }}</p>
        <p>{{str.split('').reverse().join('')}}</p>
        <p>{{reverse}}</p>
        <p>苹果总价： {{allPrice}}</p>
      </div>
      <script type="text/javascript" src="js/vue.js"></script>
      <script type="text/javascript">
        var vm = new Vue({
          el: '#app',
          data: {
            num: 1,
            str: 'tomandjerry',
            applePrice: 10,
            appleNum: 10 
          },
          computed: {
            reverse: function () {
              return this.str.split('').reverse().join('')
            },

            allPrice: function () {
              return this.applePrice * this.appleNum
            }
          }
        });
      </script>

III、计算属性和方法的区别 ☆☆☆☆☆

  A: 计算属性存在缓存，methods里面的方法不存在缓存(methods里面的方法每次都是重新运算或者执行相应的逻辑)
  B: 计算属性因为依赖于data中的数据，只要data中的数据没有发生变化,那么在使用计算属性的时候，结果始终从缓存中进行取值

5. 侦听器(watch) ☆☆☆☆☆

I、什么是侦听器

  侦听器就是用来对data中的数据进行监听，
  当数据发生改变之后，就会触发 watch 中绑定的方法
  在侦听器方法中就可以获取到更新之后的最新值以及旧的值
  用来操作一些异步操作和复杂的运算

II、侦听器注意事项
  A: 侦听器 也是和 data 同级进行声明 一个 watch
  B: 侦听器的属性不能随便写，需要是 data 中的数据，也就是对谁进行监听，就写谁
  C: 在回调函数中，有两个参数：第一个参数是更新之后的值，也就是最新的值；第二个参数是更新之前的值，也就是旧的值
  eg: <div id="app">
        <p>数量：<input type="text" v-model.number="appleNum"></p>
        <p>价格：<input type="text" v-model.number="applePrice"></p>
        <p>总价: {{allPrice}}</p>
      </div>
      <script type="text/javascript" src="js/vue.js"></script>
      <script type="text/javascript">
        var vm = new Vue({
          el: '#app',
          data: {
            appleNum: '',
            applePrice: '',
            allPrice: ''
          },
          watch: {
            // 对谁进行监听，那么属性就写谁
            // newVal 最新值，oldVal 之前的值
            appleNum: function (newVal, oldVal) {
              this.allPrice = this.applePrice * newVal
            },

            applePrice: function (newVal, oldVal) {
              this.allPrice = newVal * this.appleNum
            }
          }
        })
      </script>

6. 过滤器 ☆☆☆

I、什么是过滤器(过滤器的本质：就是对数据进行格式化处理，最后将格式化处理好的数据返回，展示到页面中的过程)
  过滤器就是对文本值、时间等进行格式化的方法
II、两个定义方法
  全局定义  -- Vue.xxx
  局部定义  -- filters
III、全局定义
  A: 需要挂载Vue上面，Vue.filter,不带 s
  B: 有两个参数: 第一个参数是 过滤器的名称，第二个参数是 一个方法,方法中有个参数，这个参数就是指所需要处理的数据
  C: 函数内部需要有 return，需要有返回值
  D：如果需要使用多个过滤器，直接使用竖线分隔 | ，后面跟上另一个过滤器名称就可以
IV、局部定义
  filters: {}
  eg: <div id="app">
        <p>{{ msg | upper }}</p>
        <p>{{ msg | upper | lower }}</p>
      </div>
      <script type="text/javascript" src="./js/vue.js"></script>
      <script type="text/javascript">
        Vue.filter('upper', function (value) {
          console.log(value)
          return value.charAt(0).toUpperCase() + value.slice(1)
        })

        Vue.filter('lower', function (value) {
          console.log(value)
          return value.charAt(0).toLowerCase() + value.slice(1)
        })

        var vm = new Vue({
          el: '#app',
          data: {
            msg: 'world'
          },
          filters: {
            upper: function (value) {
              return value.charAt(0).toUpperCase() + value.slice(1)
            }
          }
        })
      </script>
V、过滤器中传递参数
   filterA 被定义为接收三个参数的过滤器函数
   其中 message 的值作为第一个参数
   普通字符串 'arg1' 作为第二个参数，表达式 arg2 的值作为第三个参数
   eg: {{ message | filterA('arg1', 'arg2') }}
   在过滤器中 第一个参数 对应的是  管道符前面的数据 n 此时对应 message
   第2个参数 a 对应 实参 arg1 字符串;第3个参数 b 对应 实参 arg2 字符串
  eg: ue.filter('filterA',function(n,a,b){
        if(n<10){
            return n+a;
        }else{
            return n+b;
        }
      })

#### Vue生命周期 ☆☆☆☆☆☆☆☆☆☆☆☆

1. Vue的生命周期是什么
  Vue 实例在被创建时都要经过一系列的初始化过程，这个过程包括在页面在挂载 - 页面更新 -- 实例销毁的过程
  创建 -- 控制页面 -- 执行DOM -- 实例数据更新 -- 销毁
  beforeCreated()  -- created  -- mounted ~~~~~~~~
  Vue 在生命周期的每个阶段，给提供了不同的方法，叫钩子函数
2. 生命周期钩子
  所谓的生命周期钩子：就是指实例在某个阶段，Vue 在这个阶段提供的方法，就是钩子，也叫钩子函数，具体叫：生命周期钩子函数
3. 生命周期函数有三个阶段
  ① 创建阶段 
  beforeCreate
  created
  beforeMount
  mounted: 先把这个记住：为什么呢！因为这个时候才能进行 DOM 操作，也就才能看到页面
  ② 运行阶段
  beforeUpdate
  updated
  ③ 销毁阶段
  beforeDestroy
  destroyed
4. 生命周期总共有8个函数 ☆☆☆☆☆☆☆☆☆☆☆☆---很重要
  eg: <script>
        // 第一个：创建一个新的 Vue 实例对象，只是创建，还没有初始化
        var vm = new Vue({
          el: '#root',
          data: {
            msg: '关雎'
          },
          methods: {
            handle () {
              console.log('国风-周南')
            }
          },
          beforeCreate() {
            // 第一个：
            // 这是 Vue 生命周期中，我们会遇到的第一个生命周期，当实例创建完全被创建出来，就会执行这个函数
            // 但是这个时候，data 和 methods 还没有被初始化
            // 这时候， data 数据访问不到， 同时，methods 方法也不能不能调用的，
            // 这时候，只能访问一些生命周期钩子函数，也可以说就是只能访问 Vue 给提供的一些方法
            // console.log(this.msg)
            // this.handle()
          },
          created() {
            // 第二个：
            // 这是 Vue 创建阶段的第二个生命周期，表示 data 和 methods 已经被初始化好了，
            // 这个时候，data 和 methods 可以进行调用
            // 也是最好调用 data 和 methods 的地方
            // 如果以后想最早发送 ajax 请求，获取数据，最早就应该在 created 里面
            console.log(this.msg)
            this.handle()
          },
          beforeMount() {
            // 第三个：
            // 这是 Vue 创建阶段的第三生命周期，表示代码在内存中已经编译成功，
            // 这个阶段，是 Vue 对代码进行编译的阶段，如果网速超级慢，那么这时候，能够在页面上看到 插值表达式
            // 在这个阶段，Vue 开始从 data 中取数据，取出来数据和 插值表达式以及指令等在进行结合渲染，
            // 这个阶段是在内存中进行的，也就是说，这时候在页面上还看不到页面的具体数据
            // 注意：只是在内存中编译成功，并没有渲染到页面中
            // 在 beforeMount 访问元素，获取元素的时候，因为还没渲染到页面，所有获取的是模板内容
            console.log(document.querySelector('h5').innerHTML)
          },
          mounted() {
            // 第四个：
            // 这是 Vue 创建阶段的第四生命周期，表示代码在内存中已经编译成功，并且渲染到页面中，
            // 用户可看到已经渲染好的页面，
            // 在这个阶段，模板字符串已经在内存中编译完成，已经插入到真实的 DOM 结构中
            // 也就是说这时候，就能够看到真正的数据和模板结合字符串
            // 当 执行完 mounted ，就代表 Vue 实例已经被完全创建好了，这时候，我们可以对页面的元素进行操作
            // 如果想最早的操作 DOM 元素，获取里面的值，那么最早就应该在 mounted 中进行获取
            console.log(document.querySelector('h5').innerHTML)
          },
          beforeUpdate() {
            // 第五个：
            // 这是 Vue 运行阶段的第一个生命周期，
            // 注意：beforeUpdate 和 update 会根据数据的变化与否有选择的执行 0 次或者 N 次
            // 当 执行完 beforeUpdate ，页面中显示的数据还是旧的，但是 data 中的数据已经是最新的
            // 在这个阶段，说明页面中的数据有更新，但是还没有和页面进行同步
            // 也就是说此时：数据是最新的，但是页面是旧的
            console.log(this.msg)
            console.log(document.querySelector('h5').innerHTML)
          },
          updated() {
            // 第六个：
            // 这是 Vue 运行阶段的第二个生命周期，
            // 注意：beforeUpdate 和 update 会根据数据的变化与否有选择的执行 0 次或者 N 次
            // 当 执行完 updated ，页面中显示的数据已经是最新的，data 中的数据也是最新的
            // 注意：这一步。做了哪些东西呢  ？
            // 首页，Vue 根据 data 中的最新的数据生成一份新的 Dom 结构在内存中，
            // 当最新的 内存 DOM 树被渲染到 页面中的时候,就完成了 data --> view 成的更新与渲染
            // 在这个阶段，数据和页面都是最新的，
            // 为什么是最新的，
            // 因为在调用这个生命钩子函数之前，Vue 又把最新的数据放到 内存中和页面再次进行拼接处理
            // 生成模板字符串，并且插入到了 DOM 结构中，所以，这时候数据和页面都是最新的
            // console.log(this.msg)
            // console.log(document.querySelector('h5').innerHTML)
          },
        })
      </script>

#### Vue中的数组方法 ☆☆☆

1. Vue对数组方法进行了进一步的处理，处理好之后，能够让操作后的数据，具有响应式的功能，能够触发视图的更新
   这个响应式指的，数据更新能够触发视图更新，页面能够响应数据的变化

2. 把数组方法处理好之后，就分成了两类

A: 变异方法：就是直接对原数组进行操作，进行更新(变异数组方法即保持数组方法原有功能不变的前提下对其进行功能拓展)

push()--往数组最后面添加一个元素，成功返回当前数组的长度
pop()--删除数组的最后一个元素，成功返回删除元素的值
shift()--删除数组的第一个元素，成功返回删除元素的值
unshift()--往数组最前面添加一个元素，成功返回当前数组的长度
splice()--有三个参数，第一个是想要删除的元素的下标（必选），第二个是想要删除的个数（必选），第三个是删除 后想要在原位置替换的值
sort()--sort()  使数组按照字符编码默认从小到大排序,成功返回排序后的数组
reverse()--reverse()  将数组倒序，成功返回倒序后的数组

B: 替换数组：替换数组会生成一个新的数组

filter()--filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。
concat()--concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组
slice()--slice() 方法可从已有的数组中返回选定的元素。该方法并不会修改数组，而是返回一个子数组

#### Vue中响应数据(纯粹了解，不用深入)

1. 由于JavaScript的限制，Vue不能检测以下数组的变动
   例如：
   A: 通过索引给 data 中的数据赋值，更新，检测不到
   B: 更改数组的长度，检测不到
   C: 动态给对象添加属性，检测不到

2. 解决方案
  Vue.set 或者  vm.$set
  eg: <div id="app">
        <ul>
          <li v-for="(item, index) in arr" :key="index">{{item}}</li>
        </ul>
      </div>
      <script type="text/javascript" src="./js/vue.js"></script>
      <script type="text/javascript">
        var vm = new Vue({
          el: '#app',
          data: {
            value: '',
            arr: [1, 2, 3, 4]
          }
        })
        // vm.arr[0] = '哈哈哈'
        // Vue.set(vm.arr, 0, '哈哈哈')
        vm.$set(vm.arr, 0, '哈哈哈')
      </script>

### Vue基础第三天