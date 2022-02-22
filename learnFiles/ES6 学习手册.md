let 关键字

    let a;
    let b,c,d;
    let e = 100 , g = 'loveyou' , h = [];

变量不能重复声明
let star = 10
let star = 30;//error 

2. 块级作用域
    只在函数体内部有效
    {
        let a = 4
    }
    console.log(a);     //error


3. 不存在变量提升
    其他的许多的变量会提升，比如
    var a;
    const t;

4. 不影响作用域链
    {
        let school = 'a' //定义在fun函数的外面
        function fn(){
            console.log(school);    //调用school变量，不过依然正常 
        }
    }
    fn(); // 会正常运行
    

const 关键字
    const a ='a'  //声明一个常量，值无法修改

    1. 必须有初始值
    2. 一般常量使用大写（潜规则）
    3. 常量的值无法修改
    4. 块儿级作用域


# ES6 教程

## let 关键字
1. 语法
   `let a = 'a'`
2. 属性
   * 变量不能重复声明
   * 块级作用域
   * 不存在变量提升
   * 不影响作用域链

## const 关键字
1. 语法
   `const a = 'a'`
2. 属性
   * 必须要有初始值
   * 一般常量使用大写（潜规则）
   * 常量的值是无法修改的
   * 块级作用域
   * 对于数组和对象的元素修改，不算做对常量的修改，不会报错

## 解构赋值
1. 概念
   ES6 允许按照一定模式从数组和对象中提取值，对变量进行赋值

   1. 数组的结构
   ```javascript
    const arr = ['a','b','c','d'];
    let [inputA,inputB,inputC,inputD] = arr;

    console.log(inputA);    //输出结果：a
    console.log(inputB);    //输出结果：b
    console.log(inputC);    //输出结果：c
    console.log(inputD);    //输出结果：d
   ```
   2. 对象的解构
   ```javascript
    const myClass = {
        name:"张三",
        age:18,
        sayHi:function(){
            console.log("大家好！");
        }
    };

    let {name,age,sayHi} = myClass;

    console.log(name);      //输出:张三
    console.log(age));      //输出:18
    console.log(sayHi);      //输出:f(){console.log("大家好！")}

    sayHi();    //输出：大家好！
   ```

## 模板字符串
1. 概念
    ES6 引入了新的声明字符串的方式 \` \` ' ' " "
2. \` \` 的特性
   1. 可以直接出现换行符
   2. 变量拼接
      ```javascript
        let str = "text"
        let out = `${str} more and more text`
        console.log(out); //输出：text more and more text
      ```

## 简化对象的写法
1. 概述
   ES6允许在大括号的里面，直接写入变量和函数，作为对象的属性和方法。这样书写可以更加简洁
   ```javascript
    let name="theName"
    let change = function(){
        console.log("我们可以改变！")
    }

    const school = {
        name,   //标准写法 name : name
        change, //标准写法 change : change
        improve(){
            console.log("text")
        }
        //标准写法
        //improve:function(){}
    }
   ```

## 箭头函数
1. 概念
   ES6 允许使用[箭头] (=>) 定义函数
   ```javascript
    //以前声明函数的样子
    let fn1 = function(a,b){
        //代码体
        retrun a+b
    }
    //现在声明函数的样子
    let fn2 =(a,b) => {
        //代码体
        return a+b
    }
   ```
   调用他们
   ```javascript
    fn1(1,2);
    fn2(5,6);
   ```
2. 箭头函数的特性
   1. this 是静态的，this  始终指向函数声明时所在所用域下的this的值(使用的是外面结构体的this)
   2. 不能作为构造实例化对象
    ```javascript
        let Person = (name,age) => {
            this.name = name;
            this.age = age;
        }

        let me = new Person("张三",18); //error  : Person是一个箭头函数，无法当做构造器使用
        console.log(me)
    ```
    3. 不能使用 arguments 变量
    ```javascript
        let fn =() =>{
            console.log(argments);
        }

        fn(1,2,3);  //error: fn 是一个箭头函数，无法使用arguments变量
    ```
    1. 箭头函数的简写
       1. 省略小括号，当形参有且只有一个的时候
        `let add = (n) =>{ ... }`
        `let add = n => { ... }`
       2. 省略花括号，当函数体有且仅有一句的时候
        `let add = (n) => { return n+1 }`
        `let add = n => n+1`
        **注意，如果省略花括号，里面的return也必须省略，而且语句的执行结果就是函数的返回值**

## 初始值
1. 概述
   ES6允许给参数赋值初始值
   1. 形参初始值,具有默认值的参数，一般位置要靠后(潜规则)
    ```javascript
    //旧标准
    function add(a,b,c){
        return a + b + c;
    }

    let add(1,2,3);     //会正常输出值
    let add(1,2);       //因为c 未定义，所以最终值是NaN

    //新标准
    function add(a,b,c=3){
        return a + b + c;
    }

    let add(1,2,3);     //会正常输出值
    let add(1,2);       //依然正常
    ```
    2. 可以和解构赋值结合
    ```javascript
    function connect({host='127.0.0.1' , uersname , passwrod , port}){
        console.log(host);
        console.log(username);
        console.log(passwrod);
        console.log(prot);
    }
    connect({
        host: "localhose",
        username : 'GL',
        password : 'root'
        port : 8080
    })

    ```

## rest 参数 
1. 概述
   用于获取函数的实参，用来代替 arguments
   ```javascript
    //es5获取实参的方式
    function data(){
        console.log(arguments); //输出的是对象 {'a','b','c','d'}
    }
    data('a','b','c','d');      


    //ES6 rest 参数
    function data(...args){
        console.log(args)   //输出的是数组 ['a','b','c','d']
    }
    data('a','b','c','d');

   ```
   **rest 参数必须要放到参数最后**

## 扩展运算符
1. [...]  扩展运算符能将数组，转换为逗号分割的 参数序列
   ```javascript
    const arr =['text1','text2','text3'];

    function fn(){
        console.log(arguments);
    }

    fn(...arr); // 也就是fn('text1','text2','text3')
   ```
2. 扩展运算符的应用
   1. 数组的合并
    ```javascript
    const a = [1,2,3]
    const b = [4,5,6]
    const c = [...a,...b]; // 结果就是[1,2,3,4,5,6]
    ```
    2. 数组的克隆
    ```javascript
    const a = [1,2,3]
    const b = [...a];       //结果是[1,2,3]
    ```

    3. 将伪数组转为真正的数组
    ```javascript
    const divs = document.querSelectorAll('div')
    const divArr = [...divs];       //会变为真的数组
    ```
        
## symbol的基本使用
1. 概述
   ES3 引入了一种新的原始数据类型symbol.表示独一无二的值。
   它是javascript 语言的第七种数据类型，是一种类似于字符串的数据类型
   他的特点
    1. symbol 的值是唯一的，用来解决命名冲突的问题
    2. symbol 的值不能与其他数据进行运算
    3. symbol 定义的对象属性不能使用for...in循环遍历，但是可以使用Reflect.ownkeys来获取对象的所有键名
   

    ```javascript
    //创建symbol
    let s = Symbol();
    const.log(s,typeof(s));

    let s2 = Symbol('text');

    let s3 = Symbol('text');

    console.log(s2 === s3)      //输出: false

    //Symbol.for创建
    let s4 = Symbol.for('text')
    let s5 = Symbol.for('text')
    console.log(s4 === s5)      //输出：true

    console.log(s4, typeof s4)
    ```
2. 使用
   1. 作用，给对象添加属性和方法
   ```javascript
    //给对象中添加方法 up down
    let game = {...}

    let methods = {
        up: Symbol(),
        down: Symbol(),
    }

    game[methods.up] = function(){
        console.log("is up");
    }
    game[methods.down] = function(){
        console.log("is down")
    }

    //new 
    let Persons = {
        name: "zyyyg",
        [Symbol('say')]:function{
            console.log("说话")
        }
    }
   ```