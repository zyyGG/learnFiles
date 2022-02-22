tsc -p d:\mineFiles\tsconfig.json

```typescript
var flag:boolean  = true

flag = 123 //error
flag = false

var a:number = 123

a = "string" //不可以 error
a = 1.3222 //可以

```

基本类型
- boolean 布尔类型
    let demo:boolean = true 
    let demo:boolean = false
- number 数值类型
    let demo:number = 6
    let demo:number = 0xf00d //16进制
    let demo:number = 0b1010 //2进制
    let demo:number = 0o744 //8进制
- string 字符串类型
    let name:string = "bob"
    name = "smith"

    模板字符串
    ` ` 包裹 , ${ expr } 这种形式嵌入
    let sentence: string = "Hello,my name is"+ name + ".\n\n" + "i'll be" + (age+1)+"years old next month"

    let name:string = `Genne`
    let age:number = 37
    let sentence : string = `Hello my name is ${name}.i'll be ${age+1} years old next month`
- 数组 
    1. let list:number[]=[1,2,3,4]
    2. let list: Array<number> = [1,2,3,4]
- 元组 Tuple
    let x:[string, number]

    x = ['hello', 2] //ok

    x = [10, "Hello"] //error

    console.log(x[0].substr(1)); //ok
    console.log(x[1].substr(1)); //error ,'numbe' does not have substr

    当访问一个越界的元素，会使用联合类型替代
    x[3] = 'world'; //ok ,字符串可以赋值给{string | number} 类型
    console.log(x[5].toString()); //ok,'string' 和 'number' 都有toString

    x[6] = true; //error, 布尔值不是{string | number}类型
- 枚举 enum
    enum Color{Red,Green,Blue}
    let c:Color = Color.Green;

    默认情况下，都是从0开始，
    也可以改为从1开始
    enum Color{Red=1,Green,Blue}
    let c:Color=Color.Green

    当然也可以全部都手动赋值

    enum Color {Red = 1, Green, Blue}
    let colorName: string = Color[2];
    
    alear(colorName) //显示为Green ,因为上面的代码中它的值是2
- 任意值 any
    我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。 那么我们可以使用any类型来标记这些变量：
    let notSure: any = 4
    notSure = "maybe a string instead";
    notSure = false //okay,最终是个布尔值

    和object看起来相似，实际上并不一样，
    let notSure: any= 4
    notSure.ifItExists(); // okay, ifItExitsts或许此时可以运行
    notSure.toFixed(); //okay , toFixed也可能可以，最终编译的时候并不检查

    let prottySure : Object  = 4
    prottySure.toFixed(); //Error,prottySure是一个object类型

    当你只知道部分数据的类型的时候，any类型也是有用的
    let list:any[]=[1, true, "free"]

    list[1]= 100
- 空值 
    functionwarnUser():void {
        alert('..')
    }
    被声明成void 的变量的值只有 undefined 和 null
- Null 和 Undefined
    这两个都有自己的类型分别是null 和 undefined .  和void 类似，但本身类型用处不大
    let u:undefined = undefined
    let n:null = null

    默认情况下，null 和 undefined是任何类型的子集，也就是可以把null ,undefined 赋值给number 类型
    let a:numer = null

    但是如果指定了 --strictNullChecks 标记，null和undefined只能赋值给他们各自
    鼓励尽可能地使用--strictNullChecks
- Never
    表示用不存在的值类型，是那些总是抛出异常或者根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型；
    变量也可以使nerver类型

    //返回never的函数必须存在无法达到的终点
    function error(message:string):nerver{
        throw new Error(message);
    }

    //推断的返回类型为never
    function fail(){
        return error("Something failed");
    }

    //返回never的函数必须存在无法达到的终点
    function infiniteLoop(): nerver{
        whild(true){

        }
    }
- 类型断言
    类型断言好比其它语言里的类型转换
    但是不进行特殊的数据检查和解构
    尖括号法
    let someValue: any = "this is a string";
    let strLength: number = (<string>someValue).length;


    另一个为as语法：
    let someValue: any = "this is a string";
    let strLength: number = (someValue as string).length;

    两种形式是等价的。 至于使用哪个大多数情况下是凭个人喜好
    然而，当你在TypeScript里使用JSX时，只有as语法断言是被允许的。

- 联合类型
    let a:number | null | undefined
    console.log(a);//undefined
    a = 1
    console.log(a);// 1 
    a = null
    console.log(a);// null

函数
函数声明
function fun(){
    ...
}

匿名函数
let fun=function(){
    ...
}

ts中
函数声明
function fun():string{
    return "string" //必须返回指定的string类型
}

匿名函数
let fun=function():number{
    return 111; //必须返回number类型
}

ts 中定义方法传参
function getInfo(name:string,age:number):string{
    return `${name} --- ${age}`;
}
getInfo("张三",18) //okay,不过必须按照类型传递

没有返回值得方法
function fun():void{
    console.log("没有返回值")
}

在ts中实参和形参必须一致，如果不一样就需要配置可选参数
function getInfo(name:string,age:number):string{
    if(age){
        return `${name}---${age}`
    }else{
        return `${name}---年龄未知`
    }
}
getInfo("张三") // error， 要求必须传入

function getInfo(name:string,age?:number):string{
    if(age){
        return `${name}---${age}`
    }else{
        return `${name}---年龄未知`
    }
}
getInfo("张三") //okay, age?:numbe 是个可选参数

***可选参数必须配置到参数的最后面***

默认参数
在es5没办法设置默认参数,但是在es6和ts中都可以设置默认参数
function getInfo(name:string,age:number=20):string{
    if(age){
        return `${name}---${age}`
    }else{
        return `${name}---年龄未知`
    }
}
getInfo("张三") // okay 输出的结果是"张三---20"

剩余参数
function sum(a:number,b:number,c:number,d:number):number{
 return a+b+c+d
}
sum(1,2,3,4) //okay 
sum(1,2,3,4.5,6) //error

function sum(a:number,b:number,c:number,d:number,...result:number):number{
    var sum=0
    for(let i=0;i<result.length;i++){
        sum+=result[i]
    }
    return a+b+c+d+sum
}
sum(1,2,3,4) //okay
sum(1,2,3,4,5,6) //okay

## 函数重载
为了兼容es5 和 es6 重载的写法，和java中有区别

es5 的写法，下面的会把上面的顶替掉
function css(config){

}

function css(config,value){

}


ts的重载
function getInfo(name:string):string;
function getInfo(age:string):number;
function getInfo(str:any):any{
    if(typeof(str==="string")){
        return "名字是-"+str
    }else{
        return "年龄是"+str
    }
}

getInfo("张三") //okay ,输出结果"张三"
getInfo(20) //okay, 输出结果20
getInfo(true) // error, 没有匹配的写法


function getInfo(name:string):string;
function getInfo(name:string,age:number):string;
function getInfo(name:any,age?:any):any{
    if(age){
        return `${name}---${age}`
    }else{
        return `${name}---NULL`
    }
}
getInfo("张三") // okay , 输出结果"张三---NULL"
getInfo(123) // error,错误的写法


箭头函数
setTimeout(function(){
    console.log("unput")
},1000)

箭头函数的this指向上下文
setTimeout(()=>{
    console.log("unput")
},1000)


## 类

        