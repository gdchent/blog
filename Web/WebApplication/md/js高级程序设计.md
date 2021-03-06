# js高级程序设计阅读笔记

### 第一章 js的简介

js是一门专门为网页设计的脚本语言

###### 一 ：js的实现

1.ECMAscript组成：语法，类型，语句，关键字，保留字  操作符  对象。

什么是ECMAscript兼容：支持Unicode兼容，提供核心语言功能。

2.dom(文档对象模型) ：提供访问和操作网页内容和接口

3.bom(浏览器对象) ：提供跟浏览器交互的方法和接口 比如 navicator

二：js的版本

##### 第二章 在HTML中使用js

一： 使用<script>元素 该元素有6个属性

 1.async：可选。不是必须的表示应该立即下载脚本  只针src指向的外部js文件有效 ，对自己的包含无效。

2.charset：可选。

3.src  指向外部脚本js文件

4.defer  相当于window.onload属性 等文档全部加载完成的时候 再加载该js脚本  仅限外部使用

5 type      可选。可以看成是language的替代属性；表示编写代码使用的脚本语言的内容类型（也称为MIME类型）。虽然text/javascript和text/ecmascript都已经不被推荐使用

6 language   已废弃。原来用于表示编写代码使用的脚本语言。大多数浏览器会忽略这个属性，因此也没有必要在用了

######  注意：

带有src属性的<script>元素不应该在其<script>和\</script>中包含额外的js代码。

如果包含了嵌入的js代码，则只会下载并执行src指向的外部脚本文件，嵌入的代码会被忽略

为什么页面引入js的script标签要放在 body的最后面，是因为如果放置在head中，要先加载

js文件，然后再加载body中的html代码显示，就会导致页面出现一段时间的空白.

##### 第三章 基本数据类型

##### 一 ：Undefined

undefined :声明变量但是没有使用的时候就是undefined

例如 var message ; //undefined

###### 二：Null 

声明了一个变量 初始化的时候推荐给null

var message=null; 

type of message  //object

###### 三： Number类型

##### 1：基本数值字面量

可以保存 八进制  十进制  十六进制数

var num=0xA //16进制输出 10   

var  num=079   //输出79

八进制字面量在严格模式下是无效的，会导致js引擎抛出错误

##### 2：浮点数据类型

在js中永远不要测试浮点数,因为不准确

例如 0.1+0.2 >0.3   0.2+0.4>0.6  0.4+0.8>1.2   0.3+0.6<0.9

0.1+0.1=0.2

##### 3：数值范围

例如:Number.MAX_VALUE+Number.MAX_VALUE  //Ininity 正无穷  返回的结果就无法进行下一步运算

##### 4：NaN

什么是NaN它是一个Number类型的值，可以通过type of 来检测基本数据类型。

##### NaN有2个特点：

1.就是任何涉及NaN的+ - *  /操作的结果都是NaN

2.就是任何的NaN都是不相等的，包括NaN本身.

console.log(NaN==NaN)  //false

为了针对以上情况，ECMAScript定义了 isNaN函数，该函数接收了一个参数，该参数可以是任何类型，而函数会帮我们确定这个参数是不是数字.

isNaN(NaN)  //返回true 

isNaN('abc')  //也是返回true 为什么？因为字符串abc强转Number为NaN，所以这里返回true

isNaN('123')  //false   ‘123’  转化为数字123 

##### 特别注意：

总结：在js中，当一个对象要转化为数字的时候，首先会调用valueOf方法 ，这个时候返回了一个结果，如果这个值是原始值则返回，否则继续调用自己的toString方法。如果此时返回的还不是原始值则抛出错误.

###### 5 数值转换：

在js中有3个函数可以将其它类型的值转化为整型

方法1： parseInt()  //解析成整型,

方法2:通过包装类 Number('123')

方法3：parseFloat()  //转化成浮点数据类型

###### Number类型的转换规则如下：

如果是boolean  只有true跟false,分别转化为1跟0

如果是数字。只是简单的传入或者返回

如果是null   返回的是 0

如果是undefined 直接转化为NaN

如果是字符串要将字符串转化为数值类型规则如下：

第一种情况：如果字符串中 只包含数字，那么首先调用valueOf方法  直接转化为十进制数据

第二种情况：如果字符串中包含有浮点数据类型，那么则将其直接转化为浮点数据类型

第三种情况：如果包含有十六进制的数据时候，那么直接转化为相同大小的十进制数据

第四种情况：如果字符串是空的“ ” ，这个时候直接转化为0.

第五种情况：如果字符串中包含除上述格式之外的字符，则将其转换为NaN。

第六种情况：如果是对象，则调用对象的valueOf方法，然后依照前面的规则转换返回的值。如果转换的结果是NaN,则调用对象的toString方法，然后再次依照前面的规则转换返回的字符串值。

Number函数在转换字符串时比较复杂而且不够合理，因此在处理整数的时候更常用的是

parseInt函数

parseInt("")  //返回NaN

Number(" ")// 返回 0

##### 四：String类型

在js中字符串用双引号（”）或单引号(')都可以 不会有什么不同。

##### 字符串字面量

String数据类型包含一些特殊的字符字面量，也叫转义序列，用于表示非打印字符，或者具有其他用途的字符。这些字符字面量如下表所示：

![image](https://github.com/gdchent/blog/blob/master/前端/JavaScript/assets/字符串字面量.png)

字符串的特点

在ECMAScript中的字符串是不可变的，也就是说，字符串一旦被创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串。

#####  js的逻辑操作符

举其中一个例子：

```javascript
<script type="text/javascript">
        //逻辑与 有一个不是boolean值的情况下 遵循以下原则
        var result = true && false;
        console.log('result', result); //输出 false 
        //逻辑与：只有2个同时为true的时候才为true
        const obj = {}
        var test2 = obj && false;
        console.log(test2)  //false
        var test3 = obj && true;
        console.log(test3); // true  如果第一个为对象 则返回第二个操作数

        //如果第一个数是字符串 返回第二个数
        var test4 = "string" && false
        console.log('test4', test4) // false

        //如果第二个数据是对象
        var test5 = true && {}
        console.log('test5', test5) // 输出  {}

        //如果第二个数据是字符串
        var test6 = true && 'abc';
        console.log('test6', test6) //输出 abc 
        //逻辑与  就是a和b2个同时满足的情况下 才为true 如果第一个为true 才对第二个值进行操作

        //如果第二个数是字符串 则返回第二个数
        var test7='字符串test7' ;
        console.log(false && test7) ;
        console.log(true && test7) ;

        //如果2个数同时为对象则返回第二个数
        //如果第一个操作数是null ,则返回null 
        // 如果第一个操作数是NaN，则返回NaN
        //如果第一个操作数是undefined,则返回underfined 

        //详情参见js高级程序设计 3.5.3 布尔操作符
        console.log(65/11)
        
```

... 总结：js高级程序设计第三章讲的基本数据类型，个人感觉要全部记清楚是一个非常头疼的问题，这个要靠平常实战项目开发的日积月累。

&& （逻辑与）：2个全部为true的时候才返回true. 如果有一个不为布尔值  可以看上面的示例代码，或者自己

在控制台输出测试。

个人在开发中一般会比较常用的是 逻辑非 强行转化为布尔值，因为安全不会报错,按照js高级程序设计上所说的也是，任何类型的数据都可以通过逻辑非转话为true或者false.不多说了，直接第四章走起。

##### 第四章 变量作用域和内存问题

###### 4.1基本数据类型和引用数据类型

6种基本数据类型：Undefined，Null,Boolean,Number,String,Symbol.基本数据类型也叫原始数据类型。

引用数据类型：对象,数组，Date等。type of用于检测是不是对象.

###### 注意: js跟Java这里有所不同，在Java中。字符串是引用数据类型。Java定义了一个String类。

###### 4.1.1动态属性

定义基本数据类型跟定义引用数据类型的方式是基本上相同的。但是在为变量进行赋值的时候，基本数据类型跟

引用数据类型的时候，两者是不同的。

###### 应用类型示例代码如下：

```javascript
var person=new Object() ;//创建一个对象
//为对象添加属性
person.name="张三" ;
console.log(person.name);//输出张三
```

以上代码创建了一个对象，然后将其保存在变量person中。然后我们为其添加了一个person的属性。

并将其字符串给了name这个属性。如果对象不被销毁，那么该属性name将一直存在。

###### 基本数据类型示例代码如下：

```javascript
//声明一个数
var name='张三';
name.age=36 ;
console.log(name.age);//输出undefined
```

###### 4.1.2 复制变量值

```javascript
var num1=5 ;
var num2=num1;
```

基本数据类型是复制值。如果是引用类型的话这里就是2个类型变量指向同一个地址，

这个跟Java没什么区别。

总之就是 对象存在于堆内存中，基本数据类型.

###### 4.1.3传递参数

基本数据类型传参情况:

```javascript
function addTen(num){ //函数参数num
    num+=10 ;
    return num;
}
var count=20 ; //定义一个变量
var result=addTen(count) ;
console.log(count) ;//输出 20 说明 基本数据类型传递参数不是按照引用传递
```

引用数据类型传参情况:

示例代码如下：

```javascript
function setName(obj){
    obj.name="zhangsan" ；
}
var person=new Person() ;
setName(person); //传入的是引用
console.log(person.name); // zhangsan
```

注意：这里的obj是引用地址值的拷贝

4.1.4检测类型

type of用来检测基本数据类型。type of检测函数会返回 ‘function’

type of检测对象没意义，用处不大，instanceof用来检测对象。

###### 4.2执行环境以及作用域

执行环境：定义变量或者函数有权访问其它数据，决定了各自的行为。  

每个执行环境都有一个与之关联的**变量对象**。在web浏览器中，**全局执行环境被认为是一个window对象**，**因此所有全局变量和函数都是作为window对象的属性和方法创建的**。当某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁。

每个函数都有自己的**执行环境**。当执行流进入一个函数的时候，函数的环境就会被推入一个环境栈中。而在函数执行完之后，栈将其环境弹出，把控制权返回给之前的执行环境。

当代码在一个环境中执行时，会创建变量对象的一个**作用域链**。作用域链的作用是保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端，始终指向当前执行代码所在的环境的变量对象。如果这个环境是函数，则将其**活动对象**作为变量对象。作用域链：简单的说就是先访问自己所在的执行环境，然后依次类推，如果还找不到就执行到全局作用域中去查找变量对象。

总之：外部执行环境无法访问到内部执行环境变量对象，而内部执行环境对象可以访问外部执行环境变量对象，

全局执行环境变量对象始终都是作用域的最后一个对象。

作用域链的最前端其实就是当前执行环境的作用域，最后端就是最外面的全局执行环境。

###### 垃圾收集

js跟Java一样具有自动回收垃圾机制，也就是说当前执行环境会负责管理代码执行过程中使用的内存。

1.标记清除法

2.引用计数法

##### 第五章 引用类型

###### 5.1.1Object类型

创建对象的2种方式

var obj=new Object() ; 

var obj={} ; //字面量  推荐方式

示例代码:

```javascript
function displayInfo(args){
    var output="" ;
    if(typeof args.name=="string"){
        output+="Name:"+args.name+"\n";
    }
    if(typeof args.age=="number"){
        output+="Age:"+args.age+"\n";
    }
    console.log(output)
}
//调用函数
displayInfo({ 
  name:'Nicholas'，
  age:29
})
displayInfo({
    name:'Greg'
})
//以上代码说明了 字面量对象的优势，当我们在写一个函数的时候，如果一个函数的参数过多，因为函数参数的顺序
//必须保持一致，这个时候我们非常优雅的写法可以用字面量对象 {} 来作为可选参数
```

一般来说访问对象的属性时都是使用点表示法，很多面向对象语言也是这样的。在js中还可以使用方括号表示来访问对象的属性。在使用方括号语法时，要访问的属性以字符串的形式放在放括号种。

示例代码如下：

```javascript
var person=new Person() ;
person.name="张三" ；// 类似于面向对象的点表示法
person['age']=13 ; //括号表示法
从功能上来说 这两种访问方式没有任何的区别，但方括号语法的优点是可以通过变量来访问属性。
例如：
var propertyName="zhangsan" ;
console.log(person[propertyName])  //输出结果
通常情况下 ，除非使用变量来表示访问属性，否则建议使用点表示法，看起来优雅。
```

###### 5.1.2Array类型

在js中我们经常操作对象跟数组。在js中的数组跟其它编程语言的数组有着很大的区别

示例代码：

**java**中的数组

```java
//我们来看看Java中的数组
int [] intArray=new int[]{22,33,66};
int [] intArray2={
    11,
    22,
    33
}
String [] strArray=new String[]{
    "数据1",
    "数据2",
    "数据3"
}
String [] strArray2={
     "数据1",
    "数据2",
    "数据3"
}
//在java中数组中的数据必须是同一个类型的
```

**javascript**中的数组

```javascript
function method(){
    console.log('我是method函数')
}
var jsArray=['数据1','数据2',333,999,NaN,method]
//js的数组可以是任意类型
//调用函数
jsArray[jsArray.length-1]() ;//调用method函数
```

###### 创建数组的基本方式有2种

第一种是使用Array构造函数，例如下面的代码所示。

```javascript
var colors=new Array(); //创建一个数组  
var colors=new Array(20) ; //创建一个数组长度为20的数组
var colors=new Array(
  "red",
    "green",
    "blue"
);
//new 操作符可以生路
var colors=Arrays('colors1','colors2') ;

```

**注意** ：如果只传递一个数字，那么表示的是这个数组的长度 。

第二种方式：var arr=["color","color2"] ;//跟对象一样使用 字面量方式。

## 字面量方式创建对象或数组都不会调用Object/Array的构造函数，js高级程序设计第五章

###### js的数组的一些特殊的特点：

var colors=['red','blue','green'] ;

colors.length=4;

console.log(colors[3]); //输出undefined

总结：可以通过设置length长度值来增加或者删除数组里面的值。

##### 5.2.1检测数组

1.instanceof 检测数组

instanceof操作符的问题：如果一个网页种包含有多个框架，那么就存在2个不同的全局执行环境，从而存在2个不同的构造函数。

2.Array.isArray(value) 也可以检测数组

3.constructor属性：arr.constructor

###### 5.2.2转换方法

所有对象都具有toLocaleString(),toString(),valueOf()方法。

示例代码：

```javascript
   		var colors = ['red', 'blue', 'green'];
        console.log(colors.toString()); //red,blue,green
        console.log("colors", colors.valueOf()); //[red,bule,green]
        var res=colors.toString();
		var resJoin1=colors.join('||')
        var resJoin2=colors.join('||') 
        console.log(resJoin1) //red,blue,green
        console.log(resJoin2) //red||blue||green
		//如果数组里面还有对象 会 var colors = ['red', 'blue', 'green',{name:'a'}];
        //数据1 : red,blue,green,[object Object]
        //数据2： red||blue||green||[object Object]
```

Array的join方法只接收一个参数，用于分隔符的字符串。

js数组的一些操作。

push()  //插入 

pop() //弹出 并且返回弹出的第一个元素 这个是删除 

unshift() //在数组的前面添加

shift()  //在数组的第一个元素 不删除

splice()  //可以增加 删除 替换

slice() //这个是删除 返回一个新的数组 不改变原始数组

sort() //排序

reverse() // 数组倒过来

js数组示例代码如下：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>javascript高级程序设计数组骚操作</title>
</head>

<body>

    <div class="container">

    </div>
    <script type="text/javascript">

        //定义一个数组
        var arrData = ['数据1', 22, 33, "数据2"]
        const delData = arrData.slice(0, 1)
        console.log(delData);  //获取删除的数组
        console.log(arrData)  //输出原始数组  说明不改变原始数组
        arrData.splice(2, 0, "new1", "new2", 'new3')
        console.log(arrData)
        var colors = ['red', 'blue', 'green']
        colors.unshift('yellow', 'dark') //从头部插入一个参数列表
        console.log('colors', colors)
        colors.shift()
        console.log(colors)

        //sort使用 
        var values = [0, 99, 996, 5, 10, 15]
        values.sort();  //数组排序
        console.log(values)
        //数组翻转
        values.reverse();
        console.log(values)
        var res = values.join('|')
        console.log('res', res)
        console.log('=====================javascript的set使用,es6使用,可以作数组去重====================================')
        var set = new Set([10, 66])
        console.log('set', set)

        console.log('============js数组的of循环一般很少使用==================')
        var array2 = [33, 99, 66, 10.22]
        //of遍历数组
        for (let v of array2) {
            console.log('v', v)
        }
        console.log('map的使用==============map键值对=======================对应Java的map差不多');
        var map = new Map();
        console.log(map.size)
        map.set('key1', 'value1')
        map.set('key2', 'value2')
        console.log(map.size)
        map.clear()
        console.log(map.size)


        console.log('=======================js数组的every函数的用法===============================')
        //every() 对数组的每一项都返回true则返回true 否则返回false
        var everyList = [10, 15, 19, 99, 36, 4]
        var resEvery = everyList.every(function (value, index) {
            console.log('item遍历项', value)
            return value < 19
        })
        console.log(everyList)
        console.log(resEvery)   // 输出遍历了3次  当 遍历到item=19的时候返回false

        console.log('=======================js数组的every函数的用法===============================')
        //如果这个数组里面有一个东西返回为true则 立即终止 不再遍历 
        var someList = [10, 15, 19, 99, 36, 4]
        someList.some(function (value, index) {
            console.log("item",value); //输出 10  15  19  99  因为99>19
            return value > 19
        })
        console.log('===============javascript的reduce用法===========')

        var reduceArray=[
             1,
             2,
             3,
             4,
             5
        ];
        var reduceRes=reduceArray.reduce(function(prev,cur,index,array){
            return prev+cur
        })
        console.log(reduceRes)
        //reduce练习题 可以计算1+2+3+..+99
        var forReduceArray=[]
        for(let i=0;i<100;i++){
            forReduceArray.push(i)
        }
        var forReduceRes=forReduceArray.reduce(function(prev,cur,index,array){
             return prev+cur;
        })
        console.log('forReduceRes结果',forReduceRes)
    </script>
</body>

</html>
```

js的Date示例代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>js高级程序设计Date</title>
</head>
<body>
        <script type="text/javascript">
             var someDate=new Date(Date.parse("March 25,2019"))
             console.log(someDate)
             //日期格式化方法
             var date=new Date();
             console.log(date.toDateString())  //输出星期 月 日 年
             console.log(date.toTimeString())  //输出 时 分 秒 时区
             console.log(date.getTime())   //输出毫秒数 与valueOf返回的相同
             console.log(date.getFullYear()) ;//获取年份 
             console.log(date.getMonth())  //获取月份  月份—1   从0开始
             console.log(date.getHours())   //获取小时
             console.log(date.getMinutes())  //获取分钟
             console.log(date.getSeconds()) ;//获取秒数
             console.log(date.getMilliseconds())  //获取毫秒数

        </script>
</body>
</html>
```

js正则表达式示例代码如下：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>js高级程序设计正则表达式</title>
</head>

<body>
    <script type="text/javascript">
        // 正则表达式
        //var expression=/pattern/flags  ;  
        //.flags  g  表示全局搜索  i表示不区分大小写  m表示多行模式

        var p = /[bc]at/g;//
        var regExp = new RegExp('[bc]at', 'g'); //跟上面是等价的
        console.log(p.global)
        console.log(regExp.global)  //表示是否设置了  g标志
        console.log('reg', regExp.ignoreCase)
        console.log('multiline', p.multiline) //是否设置了m标志
        console.log('lastIndex', p.lastIndex) //整数
        var res = regExp.test('ckkdkdkbatddd');
        console.log(res)
    </script>
</body>

</html>
```

##### 5.5 Function类型

```javascript
//函数声明方式
function sum(num1,num2){
    return num1+num2;
}
//函数表达式 方式
var sum=function(num1,num2){
    return num1+num2;
}
//具名函数表达式
var sum=function sumMethod(num1,num2){
    return num1+num2;
}

//不推荐方式
var sum=new Function('num1','num2','return num1+num2');//不推荐  影响性能

```

##### 5.5.1 没有重载（深入理解）

```javascript
function addSomeNumber(num){
		return num+100;
}
```

函数名仅仅是指向函数的指针，因此函数名与包含对象指针的其它变量，没有什么不同。

js中函数没有重载.

##### 5.5.2 函数声明与函数表达式

```javascript
//第一步 声明函数
function sum(sum1,sum2){
     return  num1+num2;
}
//调用函数
console.log(sum(10,10)) ;//输出结果为20 

//定义一个变量 指向一个函数  用一个变量指针 指向函数变量指针 其实就是复制了一个函数变量指针而已。
var anotherSum=sum;
console.log(anotherSum(10,10)); //输出20
//置空变量 sum
sum=null;   //虽然变量置空了，这里只是置空的是变量指针，而sum的函数还是存在的
console.log(anotherSum(10,10)) ; //依然输出
a
```

同时声明2个同名函数，后面的函数会覆盖前面的函数。

*函数声明示例代码：

```javascript
console.log(sum(10,10)) ;//调用函数  输出20
//函数声明
function sum(num1,num2){
    return num1+num2
}
//以上示例说明了在js中是函数声明可以提升，可以先调用后声明，实际上是在js引擎会自动提升function
//先自动把函数提升到最前面。
```

*函数表达式：

```javascript
console.log(sum(10,10)) ;//先调用函数
//如果这里使用的是函数表达式 在调用之后 这里会抛出异常
var sum=function(){
     return sum1+sum2 ;
}；
//以上代码运行直接报错 因为sum是变量 按照js的词法作用规则会左边进行lhs查询 是在编译阶段执行。 右边是在执行阶段进行的rhs查询
```

###### 总结：以上代码说明js函数声明可以提前，并且函数和变量同名的时候，函数会被js引擎自动提升到最前面.

##### 5.5.3 作为值的函数

在ECMAscript中函数本身就是变量，所以函数也可以当作值来使用。也就是说在js中函数可以当作值来传递参数，传递个另外一个函数。

示例代码：

```javascript
//声明一个函数接收2个参数
function callSomeFunction(someFunction,someArgument){
    return someFunction(someArgument);
}
function add10(num){
     return num+10;
}
//其实这个例子中重点就是这个add10 这个add10是这个函数本身，而不需要加上（）,加上括号是函数的返回值.
var result1=callSomeFunction(add10,10);
function getGreeting(name){
     return "Hello,"+name;
}
var result2=callSomeFunction(getGreeting,'Nicholas')；
console.log(result2) ; //输出 "Hello, Nicholas"
```

##### 排序：js中数组的sort方法直接排序有问题，所以它支持了一个带函数的参数。即使js比较的是整型的数组，也是会把数字转化为字符串来比较。

```javascript
var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
function  createComparisonFunction(propertyName){
    return function(object1,object2){
        var value1=object1[propertyName];
        var value2=object2[propertyName]；
        if(value1<value2){
            return -1; //表示前面一个数小于后面的数
        }else if(value1>value2){
            return 1; //表示前面一个数字大于后面一个数
        }else {
             return 0 ;// 表示2个相等
        }
    }
}
//调用数组的排序方法
data.sort(createComparisonFunction('name')) ;
console.log(data[0].name);

```

##### 5.5.4函数内部属性

递归 ：就是自己调用自己 ，例如求阶乘

##### arguments.callee

递归示例：

```javascript
function factorial(num){
    if(num<=1){
        return 1;
    }
    return num*factorial(num-1) ; //或者使用return num*arguments.callee(num-1);
}
```

**注意：函数的名字仅仅是一个包含指针的变量而已。因此，即使在不同环境中执行，全局环境的函数跟对象中的函数指向的依然是同一个对象。**

##### caller属性

```javascript
function outer(){
     inner();
}
function inner(){
    console.log(inner.caller); //
    innerIn();
}
function innerIn(){
     console.log(innerIn.caller); // 指向了inner函数 
}
outer(); //inner.caller指向了outer()
//说明function.caller指向了调用它的函数
```



bind函数的用法

```javascript
window.color="red" ;
var o={color:'blue'};
function sayColor(){
    console.log(this.color);
}
var objectSayColor=sayColor.bind(o);
objectSayColor(); //blue
```

##### 5.6：js的包装类型：

```javascript
var s1="some text" ;//字符串
var s2=s1.substring(2);
s1=null;
//以上代码其实做了三件事情
//1 创建String类型的一个实例
//2 在实例上调用指定的方法
//3 销毁这个实例
//等同于一下代码
var s1=new String('some text');
var s2=s2.substring(2);
s1=null;
 //区别
```

##### 总结：2个的区别，使用new操作符创建的实例，在离开当前作用域之前会一直保存在内存中，而自动创建的基本包装类型的对象则只存在于一行代码的执行瞬间，然后立即销毁（这里指的是销毁的堆内存），所以不能在运行时候添加属性和方法。

Object的构造函数也会像工厂方法一样。根据传入值的类型返回相应基本包装类型的实例.

```javascript
var obj=new Object('some text');
console.log(obj instanceof String);
//把字符串传给Object类型，就会创建String实例,而传入数值参数会得到Number的实例，传入boolean就会得到boolean的实例。
var value='25';
var number=Number(value) ;//转型函数 将字符转化为整型 
console.log(typeof number) // "number"
var obj=new Number(value) //构造函数
console.log(typeof obj); // "object"
```

num.toFixed(num.toFixed());//

包装类js跟Java这里好像有点区别：

在js中  var  num=22 ; // 相当于会执行  var num=new Number(22) ;

在Java中执行 int num=22 ; //在Java里面好像是不会的，在自己定义一个包装类型的对象时，如下：

//Integer i1 = 40;//Java在编译的时候会执行将代码封装成Integer i1=Integer.valueOf(40)

##### 5.6.3 String类型

字符串链接:

```javascript
var sringValue="hello ";
var result =stringValue.concat('world');
console.log(result); //结果  "hellw world"
console.log(stringValue); // ”hello“
```

##### 5.7.3单体内置对象

Global对象：

URL地址处理编码解码方法：

编码： encodeURI()encodeURIComponent()

解码：decodeURI()和 decodeURIComponent()

##### 第六章 js面向对象程序设计

##### 6.1 理解对象

```javascript
var person=new Object(); //创建对象
person.name="Nicholas" ;
person.age=29 ;
//这个是函数表达式了 
person.sayName=function(){
	console.log(this.name);
}

//字面量方式创建对象
var person={
    name:'Nicholas',
    age:29,
    job:'Software Enginner',
    sayName:function(){
        console.log(this.name)
    }
}
```

##### 2.访问器属性：

访问器属性不包含数据值；它们包含一对儿 getter 和 setter 函数（不过，这两个函数都不是必需的）。 

在读取访问器属性时，会调用 getter 函数，这个函数负责返回有效的值；在写入访问器属性时，会调用 

setter 函数并传入新值，这个函数负责决定如何处理数据。访问器属性有如下 4 个特性。 

 [[Configurable]]：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特 

性，或者能否把属性修改为数据属性。对于直接在对象上定义的属性，这个特性的默认值为 

true。 

 [[Enumerable]]：表示能否通过 for-in 循环返回属性。对于直接在对象上定义的属性，这 

个特性的默认值为 true。 

 [[Get]]：在读取属性时调用的函数。默认值为 undefined。 

 [[Set]]：在写入属性时调用的函数。默认值为 undefined。 

```javascript
 var person={
             name:'zhangsan',
             sayName:function(){ 
                 console.log('说名字')
             }
        }
       
        //delete person.name
        console.log('sayName',person.name)
        //这个函数接收3个参数  
        Object.defineProperty(person,'name',{
            writable:false, //能否修改属性值  默认返回为true 表示可以修改 这里设置为false表示对象不能被修改
            value:'lisi'  //这个value是表示你要修改的值，
        }) ;//这个方法接收3个参数
        //defineProperty这个函数 接收3个参数 第一个参数为 要修改的对象，第二个参数为要修改的对象的属性 
        //第三个参数 是描述对象 ，用来描述对象的属性， 这个描述对象的属性 必须是  configurable,enumerable,wretable,value.
        console.log(person)
        person.name="wangwu"
        console.log(person)
        for(let item in person){
            console.log('item',item)
        }
	
		
		//set跟get的用法
 		var book = {
            _year: 2004,
            edition: 1
        };
        Object.defineProperty(book, "year", {
            get: function () {
                return this._year;
            },
            set: function (newValue) {
                if (newValue > 2004) {
                    this._year = newValue;
                    this.edition += newValue - 2004;
                }
            }
        });
        book.year = 2005;
        console.log(book.edition); //2

```

##### 6.2创建对象

###### 6.2.1 工厂模式

工厂模式示例代码：

```javascript
 var o = new Object(); 
 o.name = name; 
 o.age = age; 
 o.job = job; 
 o.sayName = function(){ 
 alert(this.name); 
 }; 
 return o; 
} 
var person1 = createPerson("Nicholas", 29, "Software Engineer"); 
var person2 = createPerson("Greg", 27, "Doctor");
```

**缺点:工厂模式虽然解决了创建 多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）**

###### 6.2.2构造函数模式

```javascript
  function Person(name, age, job) {
            this.name = name;
            this.age = age;
            this.job = job;
            this.sayName =sayName
        }
		//说名字
        function sayName(){
            console.log(this.name);
        }
        var person1 = new Person("Nicholas", 29, "Software Engineer");
        var person2 = new Person("Greg", 27, "Doctor");
        person1.sayName();
        person2.sayName();
```

**构造函数模式跟工厂模式的区别：**

1.没有显式地创建对象。

2.直接将属性和方法赋给了 this 对象。

3.没有 return 语句

**构造函数的创建会经历4个步骤：**

(1) 创建一个新对象； 

(2) 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）； 

(3) 执行构造函数中的代码（为这个新对象添加属性）； 

(4) 返回新对象。

###### 6.3.1原型模式

我们知道每个函数都有一个prototype(属性),这个是属性是一个指针，指向一个对象。

我们可以通过代码证明：

```javascript
//声明一个test函数
function test(){
     
}
//输出函数的prototype
console.log(test.prototype) //可以发现输出一个对象 也就是prototype指向的这个对象
// 必须包含有2个属性 constructor属性 是一个函数 也就是函数本身 test，另一个属性__prototype__ 

//声明一个Person函数
function Person(){
    
}
var p1=new Person();
console.log(p1); //输出p1
//当用new关键字创建对象的时候，会给对象一个__prototype__属性指向原型对象
{
    __prototype__:{
        constuctor:f,
            __prototype:{ //这个对象是Object对象
                   constructor:f ,   //f是Object本身
                   xxxx:xxx,
                   yyyy：yyy, 
            }    
    }
}

```



遍历对象操作可以用in操作符，可以用hasOwnProperty方法和in操作符就可以确定该属性到底是存在于对象中还是存在于原型中。示例代码如下：

```javascript
function hasPrototypeProperty(object,name){
     //如果name不属于原型Object 并且name是传进来的对象的属性 那该对象就存在于对象中
    return !Object.hasOwnProperty(name)&&(name in object);
}
```

更简单的原型语法

```javascript
function Person(){
    
}
Person.prototype={
    name:'Nicholas',
    age:23,
    job:'Software',
    sayName:function(){
        console.log(this.name);
    }
}
```

示例代码：

```javascript
var friend=new Person();
console.log(friend instanceof Object);  //true
console.log(friend instanceof Person);   //true
console.log(friend.constructor==Person) ;// false
console.log(friend.constructor==Object) ;  // true
```

//重设构造函数，只适用于es5兼容的浏览器

```javascript
Object.defineProperty(Person.prototype, "constructor", { 
enumerable: false, 
value: Person 
});
```

##### 原始的动态性

```javascript
function Person(){
    
}
var friend=new Person();
//这个是给原型增加属性。 其实就相当于Java的类 声明方法
Person.prototype.sayHi=function(){
	console.log("hi")
 }
friend.sayHi();//hi 
//但是如果像下面这样写
Person.prototype={
    constructor:Person,
    sayHi=function(){
        
    }
};
friend.sayHi();//这里调用就会报错 
//报错的原因是什么？ 因为这里重写了Person的原型 导致的
```

##### 重写原型对象之后

##### 原生对象的原型：

原生引用类型：Object,Array,String,等等都在其构造函数的原型上定义了方法。

```javascript
console.log(typeof Array.prototype.sort); //function
console.log(typeof String.prototype.substring)  //function
```

###### 原型对象的问题

1.它省略了为构造函数传递初始化参数的环节，结果所有实例在默认情况下都将取得相同的属性值。

最大的问题是由其共享的本性所导致的。

### 6.3 js继承

##### js组合继承方式

实例代码:

```javascript
//第一步 先写一个父类
function SuperType(name){
    this.name=name;
    this.colors=[
        'red',
        'blue',
        'green',
    ]
}
//其实就是给父类写一个原型方法 就相当于在Java的父类里面增加一个方法而已
SuperType.prototype.sayName=function(){
    console.log(this.name);
}

//再写一个类 相当于java的 class SubType{}
function SubType(name,age){
    SupterType.call(this,name) ; //其实就是在子类的构造器里面调用 super方法 相当于Java这个意思
    this.age=age;
}

//继承 父类的 方法  就是让子类的 原型有父类的方法，这样的话如果自己有重写这个方法就不会去父类里面调用该方法
SubType.prototype=new SuperType() ;// 在js中当new SuperType()的时候 它会在它的内部自然拥有一个__prototype__的属性指向自己的原型 从而形成原型链 
//SubType.prototype.constructor 
SubType.prototype.constructor=SubType; //指向SubType自己 
SubType.prototype.sayAge=function(){
    console.log(this.age);
}
//
var instance1=new SubType('Nicholas',29);
instance1.colors.push('添加方法');// 给子类实例添加

```

总结：这种思想跟Java的oop思想很像，很好理解。


##### 6.3.1原型式继承

直接上示例代码：

```javascript
function object(obj){
     function F(){}
     F.prototype=o;
     return new F();
}

var person={
    name:'Nicholas',
    friends:[
        'Shelby',
        'Court',
        'Van',
    ]
}
var anotherPerson=object(); //注意 这里不是new object哦，如果new了每次创建的时候会多创建一个对象
//根据之前学过的知识 参数obj复制了一个obj的指针值 也就是进行指针的复制 是浅拷贝
var anotherPerson = object(person); 
anotherPerson.name = "Greg"; 
anotherPerson.friends.push("Rob"); 
var yetAnotherPerson = object(person); 
yetAnotherPerson.name = "Linda"; 
yetAnotherPerson.friends.push("Barbie");
console.log(person.friends)  //"Shelby,Court,Van,Rob,Barbie"


```

以上代码与Object.create()创建的对象跟上面的对象很像。

看下Object.create方法示例代码：

```javascript
var person = { 
name: "Nicholas", 
friends: ["Shelby", "Court", "Van"] 
}; 
var anotherPerson = Object.create(person); 
anotherPerson.name = "Greg"; 
anotherPerson.friends.push("Rob"); 
var yetAnotherPerson = Object.create(person); 
yetAnotherPerson.name = "Linda"; 
yetAnotherPerson.friends.push("Barbie"); 
console.log(person.friends); //"Shelby,Court,Van,Rob,Barbie"
```

Object.create()方法的第二个参数与Object.defineProperties()方法的第二个参数格式相 同：每个属性都是通过自己的描述符定义的.

示例代码如下：

```javascript
var anotherPerson = Object.create(person, { 
name: { 
value: "Greg" 
} 
});
```

##### 6.3.5寄生式继承

```javascript
//工厂方法创建对象
function object(obj){
     function F(){}
     F.prototype=o;
     return new F();
}
//传递对象方式创建对象
function createAnother(original){ 
 var clone = object(original); //通过调用函数创建一个新对象
 clone.sayHi = function(){ //以某种方式来增强这个对象
 console.log("hi"); 
 }; 
 return clone; //返回这个对象
}
//在这个例子中，createAnother()函数接收了一个参数，也就是将要作为新对象基础的对象。然
//后，把这个对象（original）传递给 object()函数，将返回的结果赋值给 clone。再为 clone 对象
//添加一个新方法 sayHi()，最后返回 clone 对象
```

###### 总结：使用寄生式继承来为对象添加函数，会由于不能做到函数复用而降低效率；这一 点与构造函数模式类似。

##### 6.3.6寄生组合式继承

示例代码如下：

```javascript
//父类
function SuperType(name){
 this.name = name; 
 this.colors = ["red", "blue", "green"]; 
} 
SuperType.prototype.sayName = function(){ 
 alert(this.name); 
};
//子类
function SubType(name, age){ 
 SuperType.call(this, name); //在子类的构造器方法中调用父类方法
 this.age = age; 
}
SubType.prototype.sayAge = function(){ 
 alert(this.age); 
};
function inheritPrototype(subType, superType){ 
 var prototype = object(superType.prototype); //创建对象
 prototype.constructor = subType; //增强对象
 subType.prototype = prototype; //指定对象
}
//这个示例中的 inheritPrototype()函数实现了寄生组合式继承的最简单形式。这个函数接收两
//个参数：子类型构造函数和超类型构造函数。在函数内部，第一步是创建超类型原型的一个副本。第二
//步是为创建的副本添加 constructor 属性，从而弥补因重写原型而失去的默认的 constructor 属性。
//最后一步，将新创建的对象（即副本）赋值给子类型的原型。这样，我们就可以用调用 inheritPrototype()函数/的语句，去替换前面例子中为子类型原型赋值的语句了

```



### 第七章 函数表达式

函数表达式示例代码：

```javascript
sayHi(); //调用函数
function sayHi(){ //声明函数
 alert("Hi!"); 
}
//在js中函数声明会被提升
```

函数表达式示例代码：

```javascript
sayHi(); //错误：函数还不存在
var sayHi = function(){ 
 alert("Hi!"); 
};
//函数表达式不能提升 因为右边是进行的rhs查询
```

##### 7.1 递归

递归求阶乘示例代码：

```javascript
function factorial(num){ 
 if (num <= 1){ 
 return 1; 
 } else { 
 return num * factorial(num-1); 
 } 
}
//以上代码没问题，但下面的代码却可能导致它出错
var anotherFactorial = factorial; 
factorial = null; 
console.log(anotherFactorial(4)); //出错！ ,因为递归里面还有factorial函数调用所以会报错
//可以用arguments.callee(num-1) 来替换
```

...省略  见不知道的js上卷笔记 

  ##### 7.4.2 模块模式

注意：js是以对象字面量方式来创建单例对象。

单例就是只有一个对象.

我们来看下Java的单例模式示例代码:

```java
public class RetrofitClient{
    private RetrofitClient retrofitClient
    public static RetrofitClient getInstance(){
        if(retrofitClient==null){
            retrofitClient ==new RetrofitClient();
        }
        return retrofitClient;
    }
    //调用其它方式来创建对象
    public void createApiService(){
        //逻辑代码
    }
}
//外部调调调用
class RetrofitTest{
    public static void main(String ...args){
        RetrofitClient.getInstance().createApiService();//
    }
}
```

以上是Java中单例模式一般的应用场景

示例代码：

```javascript
var singleton={
    name:'value',
    method:function(){
         //这里是方法的代码
    }
}

```

下面是使用模块方式创建对象方式:(就是把所有的属性或者方法全部丢在一个对象里)

```javascript
var singleton=function(){
     //添加私有变量
    var privateVariable=10;
    function privateFunction(){
        return false;
    }
    return {
        publicProperty: true,
        publicMethod : function(){ 
        privateVariable++; //内部函数引用外部函数变量 这里形成了闭包
        return privateFunction(); 
       }
    }
}
//window全局执行环境调用
singleton().publicProperty //true  
```

总结:以字面量方式创建单例对象时，这个单例对象是暴露给外部可以直接通过字面量对象直接调用，

而使用函数方式封装的模块模式 返回一个对象暴露给外部使用，这样就封装了内部的私有属性跟方法不能直接被外部使用，其实也就是通过js的闭包方式来间接的调用. 

模块模式应用场景：如果必须创建一个对象并以某些数据对其进行初始化，同时还要公开一些能够访问这些私有 数据的方法，那么就可以使用模块模式.以这种方式来创建的对象是单例的，其实就是间接的暴露一个

通过字面量创建单例，由它来访问私有属性跟方法。

##### 7.4.3 增强的模块模式

```javascript
var singleton=function(){
     var privateVariable=10 ;//私有变量和私有函数
     function privateFunction(){
          return false;
     }
    
     //创建私有对象
    var object=new Customtype();
     //添加特权/公有属性和方法
    object.publicProperty = true; 
    object.publicMethod = function(){ 
    privateVariable++; 
    return privateFunction(); 
 }; 
 //返回这个对象
 return object;
}
```

### 第八章 BOM

什么是BOM？ brower object model  浏览器对象模型。

##### 8.1 window对象

BOM的核心对象是window，它是用来表示浏览器的一个实例。在浏览器中。window既是一个浏览器窗口，同时也是ecmascript规定的global.

总结：浏览器窗口（window）作为global对象，网页中任何一个变量 对象 属性 方法都是在window中的，

所以可以访问parseInt方法

js=bom+dom+ecmascript 第一章讲过了。

window添加的属性 不可以 通过delete操作符被直接删除，因为它自带的 [[Configurable]]属性被设置为false。

##### 8.1.2 窗口关系以及框架

在之前有讲过。如果我们集成了第三方框架，因为每一个框架页面都有自己的全局执行环境的问题。

而在js中为每一个window对象提供了一个f'rames 属性(数组)来访问其它的框架的window，这样我们就可以通过window.frames的索引去获取到它，会根据页面的引入的从上往下的顺序依次获取子window对象.

示例代码入下：(比如frameset标签的嵌套问题)

```html
<html>
    <head>
        
    </head>
    <body>
         <frameset rows ="100,*">
              
          <framesrc="frame.htm"name="topFrame">
          <frameset cols="50%,50%">
          <framesrc="anotherframe.htm"name="leftFrame">
          <framesrc="anotherframeset.htm"name="rightFrame"></frameset>
        </frameset>
    </body>
</html>
```

##### 8.1.3窗口的位置

 //因为浏览器方式 IE Safari 

​        //opera浏览器虽然支持 sceeenLeft跟screenTop的 

​        //window窗口距离 总之一句话就是  由于浏览器之间有差异性

​        //获取 window的窗口距离 要使用三元运算符来

​        //这2个属性表示从屏幕的左边到 弹出显示窗口的距离 以及屏幕的上面到窗口顶部的距离

 示例代码：

```javascript
  var leftPos=typeof window.screenLeft =='number' ?window.screenLeft:window.screenX ;
  var topPos=typeof window.screenTop=='number' ? window.screenTop:window.screenY;
```



   #####   8.1.4 窗口的大小

针对window对象而言的

innerWidth:窗口本身的宽度

innerHeight:窗口本身的高度

outerWidth 和 outerHeight 返回浏览器窗口本身的尺寸
示例代码：

```javascr
//第一
 console.log('xxx',window.innerWidth) ;//我这个显示器 输出1920
 console.log('xxx',window.outerHeight) ;// 浏览器窗口本身尺寸
 
 //设置窗口大小
 //使用 resizeTo()和 resizeBy()方法可以调整浏览器窗口的大小
 window.resizeTo(100, 100); //将窗口调整到100*100
 console.log('xxx',window.innerWidth) ;//输出还是1920
 console.log('xxx',window.outerWidth) ;// 输出100
```

##### 8.1.5 导航和窗口

window.open()方法用于导航到特定的url地址，也可以打开一个新的窗口，

```javascript
window.open(
   'https://www.baidu.com',
    窗口目标, //比如frameset 的name='topFrame'
    '特性字符串',
    boolean, //表示是否取代当前页面
)
//上面等同于
<a href="https://www.baidu.com" target='topFrame'>百度</a>
```

##### 8.2 location对象

##### 8.3检测插件

浏览器是否安装了哪些插件?

```javascript
//检测插件（在 IE 中无效）
function hasPlugin(name){ 
 name = name.toLowerCase(); 
 for (var i=0; i < navigator.plugins.length; i++){ 
 if (navigator. plugins [i].name.toLowerCase().indexOf(name) > -1){ 
      return true; 
   } 
 } 
 return false; 
}
//检测Flash
console.log(hasPlugin('Flash'))
//检测 QuickTime
console.log(hasPlugin('QuickTime'))
```

##### 8.4  screen对象  

##### 8.5 history对象

//后退上一页

window.history.go(-1)

//前进一页

window.history.go(1)

//前进二页

window.history.go(2);

另外，还可以使用两个简写方法back()和forward()来代替go()。前进跟后退

