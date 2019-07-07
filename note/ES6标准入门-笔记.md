# ES6学习笔记

## 块级作用域

ES5中只有全局作用域和词法作用域`函数作用域`,没有块级作用域;
没有块级作用域会导致一些潜在的问题出现,譬如:

* 局部变量会覆盖全局变量;

* 循环变量泄漏为全局变量;

于是ES6新增了块级作业域, let 是块级作业域的实现;

```javascript
// 块级作用域的实现
{
    let tmp;
}
```
----

块级作用域的特性:

* 两个块级作用域内的变量互不影响,互不能访问;

* 块级作用域存在嵌套关系时,外层作用域的同名变量,不会受到内层作用域的同名变量赋值影响;

    - 外层作用域不能访问内层作业域的变量;
 
```javascript
{
    let flag = true;

    if( flag ){
        let flag = false;
        /**
         * 如果此代码块内 flag 没有使用 let 声明,则 if 语句不形成块级作用域
         * flag = false; 也就成了简单的赋值语句,遵循'作用域链'规则;
         */
    }

    console.log(flag); // true
}
```
> 作用域链: 
> 当javascript引擎访问一个变量时,如果当前作业域内`当前作用域不为全局作用域`,存在该变量声明`var`,便将该变量绑定在当前作用域中,为局部变量;
> 如果变量声明不存在,就访问上一层作用域中的同名变量是否声明,如此一层一层向上访问同名变量,直到该变量声明所在的位置,这个过程称为作用域链;

----

块级作用域的应用

* 使用块级作用域替代立即执行匿名函数;
    
* 函数本身的作用域,也在其所在的块级作用域内`{}`;

```JavaScript
let foo = function(){
    console.log(typeof foo) //function
    
    /*
     * // 函数本身的作用域,也在其所在的块级作用域内`{ ... }`
     */
    
}
```

## let 与 const 
 
let 用于声明变量,其用法类似 var ;

```javascript
let str = "string";
var num = 126;

console.log(str); // string
console.log(num); // 126
```
### let 与 var 区别: 

* let 不存在"变量提升"现象;

> 变量提升: 因为预解析的原因,JavaScript引擎会将所有的变量声明与函数声明'提前'解析,变量赋值的位置不变;
 
```javascript
console.log(str); // undefined
var str = "string";

// -- 解析顺序 --
var str;
console.log(str); // undefined
str = "string";
```
> 由于 let 不存在"变量提升"现象,所以,变量必须先声明再访问,否则抛出错误ReferenceError;

```javascrrgipt
console.log(str); // undefined
var str = "string";

console.log(num); // ReferenceError
let num = 126;
```

* let 所声明的变量只在当前代码块有效(访问);

> 代码块: 一个独立并且闭合的花括号`'{...}'`空间;

```javascript
// is let
for(let i = 0 ; i < 2 ; i++){
    console.log(i); // 0,1
}
console.log(i) // ReferenceError

// is var
for(var j = 0 ; j < 2 ; j++){
    console.log(j); // 0,1
}
console.log(j); // 2
```

* 暂时性死区[!]

    - 概念: 当块级作用域内有 let 、const 声明变量时,这些变量将绑定在当前作用域内,与此作用域外的同名变量互不影响;

    - "暂时性死区": temporal dead zone(TDZ);

    - 在"暂时性死区"中, let 、const 变量遵守变量不提升原则,变量访问 之前,必须先声明;

    - 当作用域内有 let 、const 声明变量时,"暂时性死区"默认开启, 在变量未声明之前访问,会抛出错误.直到 let 声明后,"暂时性死区"关闭 ; 

```javascript
if(true){

    // TDZ start
    str = "string";
    console.log(str); // ReferenceError
    // TDZ end

    let str;
    console.log(str); // undefined
}
```

> TDZ作用: 只要解析进入当前作用域,所要使用的变量就已经存在,但是不可访问(获取),只有等到声明语句出现,才可以访问与获取;

* 不允许重复声明

let 不允许在相同作用域内重复声明同一个变量, var 与 let 也不能同时重复声明;

```javascript
{
    let str = "string";
    let str = "String"; // SyntaxError
}

{
    let str = "string";
    var str = "String"; // SyntaxError
}
```


