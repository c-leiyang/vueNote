## ES6笔记

### ES6概述

1. ES6是一个统称，它代表2015年以后发布的所有版本，说白了，ES6就是ECMAScript的第六个版本，(ES2015)协会规定，以后每年都会对ECMAScript进行更新，目前开发中ES3~ES5使用率较高

### ES6中几种常用的声明方式(var、let、const)

1. var--let--const的区别

A：var声明的变量有预解析，let和const声明的变量不存在预解析
B：var声明的变量不存在块级作用域的概念，let声明的变量存在块级作用域的概念
C：var在同级作用域中可以声明多次(声明的变量名相同)，后面的会覆盖前面的，let在同级作用域中只允许声明一次
D: let声明的变量存在暂时性死区，在块级作用域内部，必须先声明后调用
E：cosnt声明的常量，必须在声明的时候就要进行初始化，否则会报错，且cosnt声明的常量不可以重复进行赋值
eg: // 暂时性死区，只是一个现象而已
    // function handle () {
    //   console.log(num)
    //   let num = 10
    // }

#### 解构赋值

1. 什么是解构
  解构就是从数组或者对象中取值，然后对变量进行赋值
eg: var arr = [1,2,3,4]
A: 变量的解构赋值
  var a = arr[0]
  var b = arr[1]
  console.log(a, b)
B: 数组的解构赋值
  let [a, b, c, d] = arr
  console.log(a, b, c, d)
C: 对象的解构赋值
  var Obj = {
    name: 'tom',
    age: 19
  }
  var {name:username, age} = Obj
  console.log(name, age)
  console.log(username, age)
D: 字符串解构赋值
  var str = 'HelloWorld'
  let [i, j, k, m] = str
  console.log(i, j, k, m)

#### 字符串新增的方法

1. includes()--startsWith()--endsWith-->返回值均为boolean

A: includes()---判断字符串中是否包含特定的字符串
B: startsWith()---判断字符串中是否包含特定的字符串开始
C: endsWith()---判断字符串中是否包含特定的字符串结尾
eg:
  var str = 'HelloKitty'
  console.log(str.includes('Hello'))
  console.log(str.startsWith('H'))
  console.log(str.endsWith('y'))

2. padSatrt()--padEnd()--应用场景(对时间和价格进行长度补全)

A: padStart()---字符串长度补全(前补全)
B: padEnd()---字符串长度补全(尾补全)
eg:
  var time = '9'
  var str = time.padStart(2, '0')
  var str = time.padEnd(5, 'qw')

#### 箭头函数注意事项

1. 注意事项
  箭头函数不绑定this,箭头函数没有自己的this关键字，如果在箭头函数中使用this,箭头函数中的this指向箭头函数父级作用域中的this指向
2. 函数拓展

A: 函数中的this是声明时的对象，不是调用时的对象
B: 箭头函数不可以new,也就是说它不是构造函数
C: 函数内部不可以使用arguments,可以使用rest参数(剩余参数)代替

#### 函数的拓展

1. 扩展运算符(形式：...)---...的作用就是把数组转换成单个的数据项---应用场景(合并数组)
eg:
  var arr = [1,2,3,4]
  console.log(...arr)
----合并数组
eg:
  var arr1 = [1, 2, 3, 4]
  var arr2 = [5, 6, 7, 8]
  var arr3 = [...arr1, ...arr2]
  console.log(arr3)

2. rest参数(剩余参数)[形式：...变量名]---rest参数的作用是将单个的数据项转换成数组，是扩展运算符的逆运算---一般用于函数的参数中
eg:
  handle(1, 2, 3)
  function handle (...str) {
    console.log(str)
    str.forEach()
  }

#### 类的使用(类的本质就是构造函数)
eg:
// function Person(sex,weight){
//     this.sex = sex;
//     this.weight = weight;
// }
// Person.prototype.showSex = function(){
//     console.log('sex:'+this.sex);
// }
// Person.prototype.showWeight = function(){
//     console.log('weight:'+this.weight);
// }
// let p = new Person('male','80kg');
// p.showSex();
// p.showWeight();

// 类的基本用法
// class Person{
//     constructor(sex,weight){
//         this.sex = sex;
//         this.weight = weight;
//     }

//     showWeight(){
//         console.log('weight:'+this.weight);
//     }

//     showSex(){
//         console.log('sex:'+this.sex);
//     }
// }

// let p = new Person('female','75kg');
// p.showWeight();
// p.showSex();

// 静态方法(静态方法必须通过类名调用，不可以使用实例对象调用)
// class Person{
//     static showInfo(){
//         console.log('hello');
//     }
//     constructor(sex,weight){
//         this.sex = sex;
//         this.weight = weight;
//     }

//     showWeight(){
//         console.log('weight:'+this.weight);
//     }

//     showSex(){
//         console.log('sex:'+this.sex);
//     }
// }

// let p = new Person('female','75kg');
// p.showWeight();
// p.showSex();
// // p.showInfo();
// Person.showInfo();

// class Student extends Person{
//     constructor(sex,weight,score){
//         super(sex,weight);//调用父类的构造函数,这个步骤是必须的
//         this.score = score;
//     }

//     showScore(){
//         console.log('score:'+this.score);
//     }
// }

// let stu = new Student('male','70kg','100');
// stu.showScore();
// stu.showSex();
// stu.showWeight();
// Student.showInfo();