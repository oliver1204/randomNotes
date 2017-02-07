[html](#htm)

[css](#css)

[js](#js)

[其他](#其他)

<h2 id="html">html</h2>

* 页面导入样式时，使用link和@import有什么区别？

 ```
（1）link属于XHTML标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用；而@import是CSS提供的，只能用于加载CSS;
	ps:只有 rel 属性的 "stylesheet" 值得到了所有浏览器的支持。其他值只得到了部分地支持。

（2）页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;

（3）import是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;

 ```
* html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？

```
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
      绘画 canvas;
      用于媒介回放的 video 和 audio 元素;
      本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
      sessionStorage 的数据在浏览器关闭后自动删除;
      语意化更好的内容元素，比如 article、footer、header、nav、section;
      表单控件，calendar、date、time、email、url、search;
      新的技术webworker, websocket, Geolocation;

  移除的元素：
      纯表现的元素：basefont，big，center，font, s，strike，tt，u;
      对可用性产生负面影响的元素：frame，frameset，noframes；

* 支持HTML5新标签：
     IE8/IE7/IE6支持通过document.createElement方法产生的标签，
     可以利用这一特性让这些浏览器支持HTML5新标签，
     浏览器支持新标签后，还需要添加标签默认的样式。

     当然也可以直接使用成熟的框架、比如html5shim;
     <!--[if lt IE 9]>
        <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
     <![endif]-->

* 如何区分HTML5： DOCTYPE声明\新增的结构元素\功能元素

```

* HTML5的离线储存怎么使用及工作原理

```
在用户没有与因特网连接时，可以正常访问站点或应用，在用户与因特网连接时，更新用户机器上的缓存文件。
原理：HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。


如何使用：
1、页面头部像下面一样加入一个manifest的属性；
  <html manifest = "cache.manifest">
    ...
  </html>
2、在cache.manifest文件的编写离线存储的资源；
   CACHE MANIFEST
   #v0.11
   CACHE:
   js/app.js
   css/style.css
   NETWORK:
   resourse/logo.png
   FALLBACK:
   / /offline.html
3、在离线状态时，操作window.applicationCache进行需求实现。

在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
离线的情况下，浏览器就直接使用离线存储的资源。

```
详细的使用请参考：

[HTML5 离线缓存-manifest简介](http://yanhaijing.com/html/2014/12/28/html5-manifest/)

[有趣的HTML5：离线存储](https://segmentfault.com/a/1190000000732617)

* HTML5的form如何关闭自动完成功能？

```
给不想要提示的 form 或某个 input 设置为 autocomplete=off。
```
* 如何实现浏览器内多个标签页之间的通信? (阿里)

```
WebSocket,也可以调用localstorge、cookies等本地存储方式；

localstorge另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，
我们通过监听事件，控制它的值来进行页面信息通信；
注意quirks：Safari 在无痕模式下设置localstorge值时会抛出 QuotaExceededError 的异常；
```
* 页面可见性（Page Visibility API） 可以有哪些用途？

```
通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;
在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；

```

<h2 id="css">css</h2>
* 介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？


```
 (1）有两种， IE 盒子模型、W3C 盒子模型；
（2）盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)；
（3）区  别： IE的content部分把 border 和 padding计算了进去;

```
* CSS3新增伪类有那些？

```
举例：
    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。
    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。
    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。
    p:only-child        选择属于其父元素的唯一子元素的每个 <p> 元素。
    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。

    :after          在元素之前添加内容,也可以用来做清除浮动。
    :before         在元素之后添加内容
    :enabled        
    :disabled       控制表单控件的禁用状态。
    :checked        单选框或复选框被选中。

```
* 如何让 div 水平垂直居中？

```
（一）
	div {
    	position: absolute;     /* 相对定位或绝对定位均可 */
    	width:500px;
    	height:300px;
    	top: 50%;
    	left: 50%;
    	transform: translate(-50%, -50%);
	}

（二）
	div {
    	position: relative;     /* 相对定位或绝对定位均可 */
    	width:500px;
    	height:300px;
    	top: 50%;
    	left: 50%;
    	margin: -150px 0 0 -250px;      /* 外边距为自身宽高的一半 */
  	}

（三）
	.container {
    	display: flex;
    	align-items: center;        /* 垂直居中 */
    	justify-content: center;    /* 水平居中 */
	}

	.container div {
    	width: 100px;
    	height: 100px;
	}  

```
* position的值relative和absolute定位原点是？

```
  absolute
    生成绝对定位的元素，相对于值不为 static的第一个父元素进行定位（原文档流中的位置不做保留）。
  fixed （老IE不支持）
    生成绝对定位的元素，相对于浏览器窗口进行定位。
  relative
    生成相对定位的元素，相对于其正常位置进行定位（原文档流中的位置依然保留）。
  static
    默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）。
  inherit
    规定从父元素继承 position 属性的值。
```
[absolute和relative的区别](http://www.html-js.com/article/3044)

* 用纯CSS创建一个三角形的原理是什么？

```
把上、左、右三条边隐藏掉（颜色设为 transparent）
#demo {
  width: 0;
  height: 0;
  border-width: 20px;
  border-style: solid;
  border-color: transparent transparent red transparent;
}

```
* 对BFC规范(块级格式化上下文：block formatting context)的理解？

```
W3C CSS 2.1 规范中的一个概念,它是一个独立容器，决定了元素如何对其内容进行定位,以及与其他元素的关系和相互作用。）
 一个页面是由很多个 Box 组成的,元素的类型和 display 属性,决定了这个 Box 的类型。
 不同类型的 Box,会参与不同的 Formatting Context（决定如何渲染文档的容器）,因此Box内的元素会以不同的方式渲染,也就是说BFC内部的元素和外部的元素不会互相影响。
```
* css多列等高如何实现

[参考文档](http://codepen.io/yangbo5207/post/equh)

[大漠老师](https://www.w3cplus.com/css/creaet-equal-height-columns)

* 浏览器是怎样解析CSS选择器的？

```
样式系统从关键选择器开始匹配，然后左移查找规则选择器的祖先元素。
只要选择器的子树一直在工作，样式系统就会持续左移，直到和规则匹配，或者是因为不匹配而放弃该规则。
```
* ::before 和 :after中双冒号和单冒号 有什么区别？解释一下这2个伪元素的作用。

```
单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素。（伪元素由双冒号和伪元素名称组成）
双冒号是在当前规范中引入的，用于区分伪类和伪元素。不过浏览器需要同时支持旧的已经存在的伪元素写法，
比如:first-line、:first-letter、:before、:after等，
而新的在CSS3中引入的伪元素则不允许再支持旧的单冒号的写法。

想让插入的内容出现在其它内容前，使用::before，否者，使用::after；
在代码顺序上，::after生成的内容也比::before生成的内容靠后。
如果按堆栈视角，::after生成的内容会在::before生成的内

```
* 如何修改chrome记住密码后自动填充表单的黄色背景 ？

```
input:autofill,
textarea:autofill,
select:autofill {
  background-color: rgb(250, 255, 189);
  background-image: none;
  color: rgb(0, 0, 0);
}
```
* 你对line-height是如何理解的？

[segmentfault](https://segmentfault.com/a/1190000003038583)

* 设置元素浮动后，该元素的display值是多少？

```
自动变成了 display:block
```
* 让页面里的字体变清晰，变细用CSS怎么做

```
-webkit-font-smoothing: antialiased;
```
* position:fixed;在android下无效怎么

```
fixed的元素是相对整个页面固定位置的，你在屏幕上滑动只是在移动这个所谓的viewport，
原来的网页还好好的在那，fixed的内容也没有变过位置，
所以说并不是iOS不支持fixed，只是fixed的元素不是相对手机屏幕固定的。
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>

```
* 如果需要手动写动画，你认为最小时间间隔是多久，为什么？

```
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms

```
* display:inline-block 什么时候会显示间隙？

```
移除空格、使用margin负值、使用font-size:0、letter-spacing、word-spacing

```
* overflow: scroll时不能平滑滚动的问题怎么处理

```
-webkit-overflow-scrolling: touch;

```
[实现原理](http://blog.csdn.net/hursing/article/details/9186199)

* 清楚浮动的方式

```
目前最简单的方式：
.clearfix{
  overflow: auto;
  zoom: 1;   // 处理IE兼容性问题
}
二:
.clearfix {
  zoom: 1;
}
.clearfix :after {
  clear:both;
  content:'.';
  display:block;
  height: 0;
  visibility:hidden;
}

<h2 id="js">js</h2>

* 介绍js的基本数据类型。

```
 Undefined、Null、Boolean、Number、String、
 ECMAScript 2015 新增:Symbol(创建后独一无二且不可变的数据类型 )

```
* 介绍js有哪些内置对象？

```
Object 是 JavaScript 中所有对象的父对象

数据封装类对象：Object、Array、Boolean、Number 和 String
其他对象：Function、Arguments、Math、Date、RegExp、Error

```
[参考文档](http://www.ibm.com/developerworks/cn/web/wa-objectsinjs-v1b/index.html)

* JavaScript原型，原型链 ? 有什么特点？

```
每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，
如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
于是就这样一直找下去，也就是我们平时所说的原型链的概念。
关系：instance.constructor.prototype = instance.__proto__

特点：
JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。


 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，
 就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
    function Func(){}
    Func.prototype.name = "Sean";
    Func.prototype.getInfo = function() {
      return this.name;
    }
    var person = new Func();//现在可以参考var person = Object.create(oldObject);
    console.log(person.getInfo());//它拥有了Func的属性和方法
    //"Sean"
    console.log(Func.prototype);
    // Func { name="Sean", getInfo=function()}

```
* 如何将浮点数点左边的数每三位添加一个逗号，如12000000.11转化为『12,000,000.11』?

```
function commafy(num){
  return num && num
  .toString()
  .replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
     return $2 + ',';
  });
}

```
* Javascript如何实现继承？

```
1、构造继承
2、原型继承
3、实例继承
4、拷贝继承

原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。

function Parent(){
  this.name = 'wang';
}

function Child(){
  this.age = 28;
}
Child.prototype = new Parent();//继承了Parent，通过原型

var demo = new Child();
alert(demo.age);
alert(demo.name);//得到被继承的属性


```
*

```

```
*

```

```
<h2 id="其他">其他</h2>

*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
*

```

```
