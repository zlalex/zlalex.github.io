## 测试用例

优秀的测试用例具有三个重要特征。

* 可重用性

* 简单性

* 独立性

构建测试的两种主要方法。

* 解构型测试用例——解构型测试用例，在消弱代码隔离问题时创建，以消除任何不恰当的问题。

* 构建型测试用例——构建型测试用例，从良好精简场景开始，构建用例，直到重现bug为止。

断言

- 单元测试框架的核心是断言方法，通常叫 assert()。该方法通常接受一个需要断言的值，以及一个表示该断言目的的描述。

```javascript

function assert (val, msg){
    var li = document.createElement('li');

    li.className = val ? 'pass' : 'fail';
    li.appendChild(document.createTextNode(msg));
    document.getElementById('results').appendChild(li);
}

```

## 函数

- 函数是**第一型对象**，可以被任意变量进行引用，或声明成对象字面量，或可以将其作为函数参数进行传递。

对象(Object)

- 对象在 JavaScript 中有以下功能

* 可以通过字面量进行创建( var obj = {} )。

* 可以赋值给变量、数组或其他对象的属性。

* 可以作为参数传递给函数。

* 可以作为函数的返回值进行返回。

* 可以拥有动态创建并赋值的属性。

* **函数对象可以被调用（invoked）**

## 线程（需要事件机制）

- 浏览器的事件轮询是**单线程**，每个事件都是按照在队列中所置放的顺序来处理的（FIFO:first in first out）。这就是所谓的先进先出列表。每个事件都在自己的生命周期           

```javascript
var a = {
    haha: function enen(n) {
        // console.log(this) // window [作为考察题目]

        // console.log(typeof enen) // function
        if (!n) {
            return n;
        } else {
            return enen(--n) + n;
        }
    }
};

var b = {
    hehe: a.haha
}

a = {};

// 忍者秘籍p.64: 不同名方法的递归调用报错
// 于是给haha的匿名函数取个函数名，这种叫内联函数
// 内联函数时也是具名函数，所有的具名函数的调用，this（函数执行的上下文都是window）
// 但是，作为内联函数，也只是能在创建时的作用域内访问

b.hehe(5);

// console.log(typeof enen) // undefined [作为考查题目]

// console.log(b.hehe(5))

var aa = function bb() {

    console.log(aa === bb);

    // console.log(typeof aa === bb); // false 
}

// aa();
// console.log(typeof bb);

// 如何解释原型，原型是指的prototype 属性，每一个声明的变量，都是由该数据对象的创建出来的实例，字符串是字符串对象创建出来的实例等

// 万物皆虚无（null），道生一（Object.prototype），一生二（Function.prototype）,再生万物（Object, String, Number, Function, Array）

// 当声明了一个函数的时候，该函数是函数对象创建的实例；

function abc() {}; // var abc == new Function();

var b = new abc();

console.log(b.constructor === abc);

console.dir(abc.__proto__ === Function.prototype);

var a = {};

console.log(a.__proto__ === Object.prototype); //Object.prototype
```