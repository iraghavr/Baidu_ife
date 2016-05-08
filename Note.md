## Learn JS NoteBook

### 基本概念

1.变量：

(1)js的变量是松散类型的，可以用来保存任何类型的数据。定义变量要用var操作符。
```javascript
var a = 1;
var a = "abc";
var a = 1,b = "a";
```

(2)用var修饰和不用var修饰的变量区别：

使用`var`操作符定义的变量将成为定义该变量作用域的局部变量。
```javascript
function test(){
            message = "hi";
        }
        test();
        alert(message);
```
使用var修饰的变量不可delete，无var修饰的变量可以delete


2.数据类型

(1)js中有5种基本数据类型：Undefined,Null,Boolean,Number,String.
还有一种复杂数据类型Object(无序的名值)
i
(2)typeof操作符测试变量的数据类型,括号可以不写
undefined：这个值未定义
boolean：布尔值
string：字符串
number:数值
object：对象或者null
function:这个值是函数

```javascript
    function test(){
            var message = "hi",age = 29;
            var b;
            alert(c);//报错
            alert(typeof b);//undefined
            alert(typeof c);//undefined
        }
        test();
```

(3)var修饰的变量在函数内的定义是处处有定义的
```javascript
        var a = "abc";
        var b = 1;
        c= 2;
        function test(){
            alert(a);//undefined
            alert(b);//1
            alert(c);//2
            var a = "bcd";
            b = 2;
            c =3;
            alert(a);//bcd
            alert(b);//2
            alert(c);//3
        }
        test();
        //以上代码相当于在函数test()函数的第一行自动添加 var a;
   ```

(4)null和undefined在用==判断总是想等，返回true;
```javascript
 var a = null;
        function test(){
            var message = "hi",age = 29;
            var b;
            alert(b==a); //true;
        }
        test();
```

(5)NaN,Infinity,-Infinity
```javascript
    var a =1/0;
    alert(a);
    var b = -1/0;
    alert(b);
    alert(isNaN(NaN));
    alert(isNaN("10"));
    alert(isNaN("abc"));
    alert(isNaN(true));
    var s = "sd";
    alert(s/2);
```

4.操作符与语句(略)

`==`和`===`

逗号操作符
```javascript
    function test(){
        var a = (1,2,3,4);
        alert(a);
    }
    test(); //4
```
`for-in`语句：循环输出的属性名顺序是不可预测的
```javascript
    function test(){
//        var a = [1,2,3,4,5,6];
//        for(var b in a){
//            alert(a[b]);
//        }
        var person = {
            name:"Mike",
            age:29,
            5:true
        }
        for(var b in person){
            alert(person[b]);
        }
    }
    test();
```

5.函数
(1)理解参数
js函数不介意传递进来多少个参数，也不在乎参数的类型，固没有重载的概念。也就是说
，即使你定义的函数只能传递只接收两个参数，在调用这个函数时也未必传递两个参数。
在函数体内，可以通过arguments对象访问参数数组，即第一个元素就为arguments[0].

(2)当没有参数时，小括号可以省略`var person = new Object;`

### 变量，作用域和内存问题

1.复制变量值
```javascript
        var person = new Object();
        person.name = "Mike";
        var p = person;
        p.name = "Jack";
        alert(person.name);
        alert(p.name);
```

2.没有块级作用域，对应`var修饰的变量在函数内的定义是处处有定义的`
```javascript
function test(){
            var a = 1;
            if(a==1){
                var b = 2;
            }
            alert(b);
        }
        test();
```

### 引用类型

1.创建Object实例的方法

(1)new操作符后跟Object构造函数
```javascript
 var person = new Object();
 person.name = "Mike";
 person.age = 29;
 var s = "name";
 alert(person["name"]);
 alert(person.name);
 alert(person[s]);
```

(2)对象字面量表示法
```javascript
var person = {
    name:"Mike",
    age:29,
    5:true   //数值属性会自动转换成字符串
}
var p = {};  //相当于var p = new Object();
```

2.Array类型(数组)

创建数组的方式
(1)使用Array构造函数
```javascript
var a = new Array();
var b = new Array(20);
var c = new Array("Mike");
var d = new Array(1,2,3,4,5);
```
(2)数组字面量表示法
```javascript
var colors = ["red","blue","green"];
var a = [];
```
数组length属性
数组的length不是只读的，可以设置这个属性进行移除,增加项
```javascript
var colors = ["red","blue","green"];
colors.length = 2;
alert(colors[2]);
colors[colors.length] = "brown";
alert(colors[2]);
```

栈方法，队列方法
push,pop
push,shift

重排序方法
reverse:反转数组
sort：根据字符串升序排序

toString,valueOf,join方法

3.Function类型

(1)js里Function就是个对象，因此函数名就是指向函数对象的指针，不会与某个函数绑定
```javascript
function f1(num1,num2){   //函数声明定义函数
            return num1 + num2;
        }
        var a = f1;
        alert(a(10,10));
var sum = function(num1,num2){  //函数表达式定义函数
            return num1 + num2;
        };
```

(2)函数声明与函数表达式
解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。
解析器会率先读取函数声明，并使其在执行任何代码之前可用(可以访问),至于
函数表达式，则必须等到执行器执行到它所在的代码行，才会真正被解释执行。
```javascript
//以下代码完全可以正常运行
alert(sum(10,10));
function sum(num1,num2){
    return num1 + num2;
}
//以下代码会在运行期间产生错误
alert(sum(10,10));
var sum = function(num1,num2){
              return num1 + num2;
          };
```

(3)函数的内部属性：arguments和this

利用arguments.callee进行递归解耦

```javascript
function f1(num){ //输出0
            if(num<=1) return 1;
            else return num * f1(num-1);
        }
        var f2 = f1;
        f1 = function(num){
            return 0;
        }
        alert(f2(5));
function f1(num){//输出120
            if(num<=1) return 1;
            else return num * arguments.callee(num-1);
        }
        var f2 = f1;
        f1 = function(num){
            return 0;
        }
        alert(f2(5));
```

4.基本包装类型

(1)为了便于操作基本类型值，js还提供了3个特殊的的引用类型Boolean,Number,和String.

```javascript
var s1 = "Dumplings";
var s2 = s1.substring(2);
```
(2)引用类型与基本包装类型区别
```
 var people = "sd";
 people.name = "Jack";
 alert(people.name);
```

(3)使用new调用基本包装类型和直接调用同名转型函数区别
```javascript
    function test(){
        var value = "25";
        var number = value; //(value);
        alert(typeof number); //string
        var num = new Number(25);
        alert(typeof num); //Object
    }
    test();
```

(4)Boolean类型
```javascript
    var f = new Boolean(false);
    var result = f && true;
    alert(result); //true
    var f = false;
    result = f && true;
    alert(result);  //false
```

(5)String类型
charAt charCodeAt concat slice substring substr indexOf lastIndexOf split localeCompare
对于`slice substring substr`，在传递给这些方法是负值的情况下，slice会将传入的负值与字符串的长度相加。
substr会将第一个参数加上字符串的长度，将第二个参数转换成0，substring会把所有参数转换成0。

```javascript
  var a = "abcdefgh";
    alert(a.slice(-3));
    alert(a.substring(-3));
    alert(a.substr(-3));
    alert(a.slice(3,-4));
    alert(a.substring(3,-4));
    alert(a.substr(3,-4));
```

### 面向对象
1.理解对象
```javascript
var person = {
       name:"Mike",
       age:22,
       sayName:function(){
           alert(this.name);
       }
   }
    person.sayName();
```
2.创建对象
(1)工厂模式
```javascript
   function createPerson(name,age,job){
       var o = new Object();
       o.name = name;
       o.age = age;
       o.job = job;
       o.sayName = function(){
           alert(this.name);
       }
       return o;
   }
    var p1 = createPerson(1,2,3);
    var p2 = createPerson(4,5,6);
```
无法搞清是哪个对象的实例
(2)构造函数模式
```javascript
 function Person(name,age,person){
        this.name = name;
        this.age = age;
        this.person = person;
        this.sayName = function(){
            alert(this.name);
        }
    }
    var p1 = new Person(1,2,3);
    var p2 = new Person(4,5,6);
```
sayName创建多次
```javascript
 function Person(name,age,person){
        this.name = name;
        this.age = age;
        this.person = person;
        this.sayName = sayName;
    }
    function sayName(){
        alert(this.name);
    }
    var p1 = new Person(1,2,3);
    var p2 = new Person(4,5,6);
    p1.sayName();
```
sayName在全局创建一次，内部sayName相当于指针
(3)原型模式
```javascript
 function Person(){
    }
    Person.prototype.name = "Mike";
    Person.prototype.age = 29;
    Person.prototype.job = "Engineer";
    Person.prototype.sayName = function () {
        alert(this.name);
    }
    var p1 = new Person();
    p1.age = 2222;
    alert(p1.age);
    alert(p1.hasOwnProperty("age"));
```
```javascript
function Person(){
    }
    Person.prototype = {
        name:"Mike",
        age:29,
        job:"engineer",
        sayName: function () {
            alert(this.name);
        }
    };
```
原型模式的问题
```javascript
function Person(){
    }
    Person.prototype = {
        name:"Mike",
        friends:["A","B"]
    };
    var p1 = new Person();
    p1.friends.push("C");
    var p2 = new Person();
    alert(p2.friends);
```
(4)组合使用构造函数模式和原型模式
```javascript
function Person(name,age,job){
        this.name = name;
        this.age = age;
        this.job = job;
        this.friends = ["A","B"];
    }
    Person.prototype = {
        constructor:Person,
        sayName: function () {
            alert(this.name);
        }
    }
    var p1 = new Person("Mike",29,"engineer");
    var p2 = new Person("Jack",27,"student");
    p1.friends.push("C");
    alert(p1.friends);
    alert(p2.friends);
```
(5)动态原型模式
(6)寄生构造函数模式
(7)稳妥构造函数模式

3.继承
(1)原型链
```javascript
 function superType(){
        this.property = true;
    }
    superType.prototype.getSuperValue = function(){
        return this.property;
    }
    function SubType(){
        this.subproperty = false;
    }
    SubType.prototype = new superType();
    SubType.prototype.getSubValue = function () {
        return this.subproperty;
    }
    var instance = new SubType();
    alert(instance.getSuperValue());
    alert(instance.getSubValue());
```
原型链的问题
```javascript
function superType(){
        this.property = ["A","B"];
    }
    superType.prototype.getSuperValue = function(){
        return this.property;
    }
    function SubType(){
    }
    SubType.prototype = new superType();
    SubType.prototype.getSubValue = function () {
        return this.subproperty;
    }
    var instance1 = new SubType();
    instance1.property.push("C");
    var instance2 = new SubType();
    alert(instance2.property);
```
(2)借用构造函数
```javascript
  function sum(num1,num2){
        return num1 + num2;
    }
    function callSum1(num1,num2){
        return sum.call(this,num1,num2);
    }
    alert(callSum1(1,2));
```
```javascript
    var color = "red";
    var o = {color:"blue"};
    function sayColor(){
        alert(this.color);
    }
    sayColor.call(o);
```
```javascript
    function A(){
        this.colors = {"red","blue","green"};
    }
    function B(){
        A.call(this);
    }
    var instance1 = new B();
    instance1.colors.push("black");
    alert(instance1.colors);
    var instance2 = new B();
    alert(instance2.colors);
```

```javascript
function A(name){
        this.name = name;
        this.sayName = function(){
            alert("haha");
        }
    }
    function B(){
        A.call(this,"Mike");
        this.age = 29;
    }
    var instance = new B();
    instance.sayName();
```
(3)组合继承
使用原型链实现对原型属性和方法的继承，通过借用构造函数实现对实例属性的继承
```javascript
function A(name){
        this.name = name;
        this.colors = ["red","blue","green"];
    }
    A.prototype.sayName = function () {
        alert(this.name);
    };
    function B(name,age){
        A.call(this,name);
        this.age = age;
    }
    B.prototype = new A();
    var instance1 = new B("Mike",29);
    instance1.colors.push("black");
    alert(instance1.colors);
    var instance2 = new B("Jack",22);
    alert(instance2.colors);
```
(4)原型式继承
(5)寄生式继承
(6)寄生组合式继承

###函数表达式
1.匿名函数(拉姆达函数)

2.闭包
(1)闭包指有权访问另一个函数作用域中的变量的函数，创建闭包最常见的方式，就是在函数内部创建另一个函数
```javascript
function f1(p){
             return function (ob1,ob2){
                 var value1 = ob1[p];
                 var value2 = ob2[p];
                 if(value1<value2) return -1;
                 else if(value1>value2) return 1;
                 else return 0;
             };
         }
```
(2)闭包只能取得包含函数中任何变量的最后一个值，闭包所保存的是整个变量对象
```javascript
    function f1(){
        var result = new Array();
        for(var i = 0;i<10;i++){
            result[i] = function(){
                return i;
            }
        }
        return result;
    }
    var s = f1();
    for(var i = 0;i< s.length;i++){
        alert(s[i]());
    }
```

```javascript
    function f1(){
        var result = new Array();
        for(var i = 0;i<10;i++){
            result[i] = (function(num){
                return function () {
                    return num;
                };
            })(i);
        }
        return result;
    }
    var s = f1();
    for(var i = 0;i< s.length;i++){
        alert(s[i]());
    }
```

(3)匿名立即执行函数
```javascript
 var f1 = function(){
        alert("sdsad");
    };
    f1();
    (function(){
        alert("sdsad");
    }());
    (function(){
        alert("sdsad");
    })();
```

### BOM
BOM：Browser Object Model(浏览器对象模型)
1.window对象
window是BOM的核心对象，它表示一个浏览器的实例，既是js访问浏览器窗口的接口，
也是js规定的Global(全局)对象
(1)全局作用域
在全局作用域中声明的变量，函数都会变成window对象的属性和方法。
```javascript
    var age = 29;
    function sayAge(){
        alert(this.age);
    }
    alert(window.age);
    sayAge();
    window.sayAge();
    //age = 29 相当于 window.age = 29
```
window对象定义的属性可以delete,var定义的变量无法delete
```javascript
 var age1 = 1;
 window.age2 = 2;
 delete window.age2;
 alert(window.age2);
```
(2)窗口位置
```javascript
    var left = window.screenLeft;
        var tops = window.screenTop;
        alert(left);
        alert(tops);
```
(3)窗口大小
```javascript
        alert(window.innerHeight);
        alert(window.innerWidth);
        alert(window.outerHeight);
        alert(window.outerWidth);
```
(4)系统对话框
alert,confirm,prompt
```javascript
if(confirm("Are you ok")){
       alert("选择了是");
   }else {
       alert("选择了取消");
   }
   window.print();
```
```javascript
    var result = prompt("什么是一阶线性非齐次微分方程?","不会");
    if(result===null){
        alert("取消");
    }else{
        alert("Your answer is："+result);
    }
```
2.location对象
既是window对象的属性，又是document对象的属性
```javascript
 //window.location = "http://www.baidu.com";
    location.href = "http://www.baidu.com";
    document.location = "http://www.baidu.com";
```
3.navigator对象
包含浏览器的属性和方法，不同浏览器属性不同。例如产品名称，版本信息，浏览器主语言等等..

4.screen对象
表明客户端能力，不同浏览器属性不同，如屏幕像素高度，DPI(屏幕点数)属性等等..

5.history对象
保存用户上网的历史纪录
```javascript
    history.go(-1);//后退一页
    history.go(1);//前进一页
    history.go(2);//前进两页
```

### DOM
DOM：Document Object Model(文档对象模型)
DOM可以将任何HTML文档描绘成一个由多层节点构成的结构
```html
<html>
<head>
    <title>Sample Page</title>
</head>
<body>
<p>Hello World！</p>
</body>
</html>
```
文档节点是每个文档的根节点，以上文档结点只有一个子节点，即<html>元素，我们称
之为文档元素文档元素是文档的最外层元素，每个文档只能有一个文档元素,在HTML中
始终是<html>

(1)childNodes属性,nodeName,nodeType(节点类型的值),nodeValue(文本节点的值)
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<script type="text/javascript">
    var a = document.documentElement;
    for(var i = 0;i< a.childNodes.length;i++){
        alert(a.childNodes[i].nodeName);
    }
</script>
</body>
</html>
```

浏览器兼容问题：重点，初学者先忽略。

(2)每个节点都有一个parentNode属性，指向文档树的父节点。
   包含在childNodes列表中的每个节点都是同胞兄弟，有相同的parentNode，
   并可以通过previousSibling和nextSibling属性访问同意列表其他结点，
   第一个结点的previousSibling属性为null，最后一个节点的nextSibling属性也为null

(3)操作结点
可以将DOM树看成由一系列指针连接起来，任何DOM结点不能同时出现在文档的多个位置
appendChild:
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p>123</p>
<p>456</p>
<p>789</p>
<script type="text/javascript">
    var a = document.body.firstChild.nextSibling;
    var b = a.nextSibling.nextSibling;
    var result = document.body.appendChild(b);
</script>
</body>
</html>
```
除了appendChild,还有insertBefore,replaceChild,removeChild,cloneNode
cloneNode接收一个参数，true，false。表示是否执行深复制(包含子节点true)，浅复制(不包含子节点false)

(4)Document类型
Document表示文档，document是HTMLDocument的一个实例，表示整个HTML页面,document也是window对象的
一个属性.可做全局对象来访问,Document结点具有以下属性
nodeType = 9;
nodeName = "\#document"
nodeValue = null;
parentNode = null;
ownerDocument(返回元素的根元素) = null;

`document.documentElement`,`document.body`获得对`<html>``<body>`的引用

`document.title`,`document.URL`

(5)查找元素
document.getElementById
document.getElementByTagName
namedItem
document.getElementByName
```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p >123</p>
<p name = "myP">456</p>
<p>789</p>
<a href="http://www.baidu.com"></a>
<script type="text/javascript">
    var a = document.body.firstChild.nextSibling;
    var b = a.nextSibling.nextSibling;
    var c = document.getElementsByTagName("p");
    var d = document.getElementsByTagName("*");
    alert(c.namedItem("myP").childNodes[0].nodeValue);
    alert(d.length);
</script>
</body>
</html>
```
(6)文档写入`write`,`writeln`
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p>123</p>
<p>456</p>
<p>789</p>
<script type="text/javascript">
    document.write("<strong>"+"fsdfdsfdsfdsf"+"</strong>")
</script>
</body>
</html>
```
(7)Element类型
具有以下特性：
nodeType = 1
nodeName = 标签名
nodeValue = null
parentNode = Document或Element

html元素
id,title,dir,className

取得属性`getAttribute`(可获取自定义属性),`setAttribute`,`removeAttribute`

创建元素
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p id="a" dir="rtl" dd="adsad">123</p>
<p>456</p>
<p>789</p>
<script type="text/javascript">
    var div= document.createElement("div");
    div.id = "myDiv";
    document.body.appendChild(div);
</script>
</body>
</html>
```
(8)Text类型
Text结点具有以下特征
nodeType= 3;
nodeName = "\#text";
nodeValue = "包含的文本";
parentNode = 一个Element；
没有子节点

操作结点文本
```javascript
    var a = document.getElementById("a").childNodes[0];
    a.appendData("zzzz");
    a.deleteData(0,3);
    a.insertData(0,"0000");
    a.replaceData(0,3,"asdasd");
    a.splitText(1);
    a.substringData(1,2);
    alert(a.nodeValue);
    a.length;
```
创建文本节点
```js
    var a = document.getElementById("a");
    var t = document.createTextNode("Hello world");
    a.appendChild(t);
```
(9)Comment类型
注释在DOM中是通过Comment类型来表示的
具有以下特征
nodeType = 8;
nodeName = "\#comment"
nodeValue = 注释的内容
parentNode = Document或Element
没有子节点

Comment与Text具有相同的基类，因此操作方法相似
(10)DocumentType类型：包含着与文档doctype有关的信息
(11)DocumentFragment类型：文档片段
```javascript
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<ul id="myList"></ul>
<script type="text/javascript">
    var fra = document.createDocumentFragment();
    var ul = document.getElementById("myList");
    var li = null;
    for (var i = 0; i < 3; i++) {
        li = document.createElement("li");
        li.appendChild(document.createTextNode("Item"+(i+1)));
        fra.appendChild(li);
    }
    ul.appendChild(fra);
</script>
</body>
</html>
```
(12)Attr类型
元素的特性在DOM中以Attr类型表示，不推荐使用，推荐`setAttribute`,`getAttribute`,`removeAttribute`

### DOM扩展

1.CSS选择符

querySelector()方法：返回匹配的第一个元素
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p class="a">123</p>
<p class="a">456</p>
<p>789</p>
<script type="text/javascript">
    var body = document.querySelector("body");
    var a = document.querySelector(".a");
    alert(a.nodeName);
</script>
</body>
</html>
```

querySelectorAll()方法：返回匹配元素的NodeList.

2.预防空格的元素遍历

childElementCount：返回子元素个数，不包含文本节点和注释

firstElementChild：指向第一个子元素，对比于firstChild

lastElementChild, previousElementSibling, nextElementSibling

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p class="a">123</p>
<p class="a">456</p>
<p>789</p>
<script type="text/javascript">
    var a = document.body;
    alert(a.firstElementChild.nodeName);
</script>
</body>
</html>
```

3.HTML5新增

getElementByClassName()方法
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<div class="a" id="q">
    aaa
    <div class="b">
       b1b1b1
        <div class="b">
            b2b2b2
        </div>
    </div>
</div>
<div class="c">
    ccccc
    <div class="b">cbcbcb</div>
</div>
<script type="text/javascript">
   // var a = document.getElementsByClassName("a");
    //var a = document.getElementsByClassName("a b");
 //  var a = document.getElementById("q").getElementsByClassName("b");
 //  alert(a[1].childNodes[0].nodeValue);
</script>
</body>
</html>
```

焦点管理
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<button id="a">Button</button>
<script type="text/javascript">
    var a = document.getElementById("a");
    a.focus();
    alert(document.activeElement == a);
</script>
</body>
</html>
```

自定义数据属性
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<button id="a" data-age="17">Button1</button>
<script type="text/javascript">
   var a = document.getElementById("a");
   alert(a.dataset.age);
</script>
</body>
</html>
```

4.插入标记
**innerHTML**
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p id="a">111</p>
<script type="text/javascript">
    var b = document.getElementById("a");
    b.innerHTML = "<strong>asdasd</strong>";
</script>
</body>
</html>
```
**outerHTML**
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p id="a">111</p>
<script type="text/javascript">
    var b = document.getElementById("a");
    alert(b.outerHTML);
    b.outerHTML = "<div>222</div>"
</script>
</body>
</html>
```
5.scrollIntoView()

6.children属性
只包含元素子节点

7.插入文本
**innerText** 和 **outerText**
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Sample Page</title>
</head>
<body>
<p>pppp</p>
<div>divdivdiv</div>
<script type="text/javascript">
  var a = document.body;
  a.innerText = "newText";
    alert(a.innerText);
</script>
</body>
</html>
```
