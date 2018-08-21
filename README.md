# Interview-questions
本文仅仅是对面试问题的一个汇总和解答，解答不具备权威性。  
开放性问题：  
1.问题介绍  
2.项目介绍  
3.希望从实习中获得哪些方面的成长  
4.未来对自己的技术栈的学习规划是什么样的  

# 技术性问题：
# 面试公司：caiCloud

# js中实现异步编程的模式都有哪些
1，回调函数  

2，时间监听  

3，发布/订阅  

4，Promise对象  

详情请看：http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html  

# 简单介绍一下原型链
原型链的存在针对是JavaScript中“万物皆对象”与不存在“继承”概念所带来的属性继承的问题。  

比如：创建一个dog对象，指定其name属性，并创建此对象的两个实例  

`function dog(name){`  
    `this.name = name`  
`}`  

`var dog1 = new dog("小黑")`  
`var dog2 = new dog("小花")`  
这样我，我们添加属性species时，  

`this.species = "犬类"` 
当修改dog1的实例属性时  

`dog1.species = "猫科"` 
由于两个实例是相互独立的，dog1的实例属性的修改不会对dog2产生影响  

为此，原型属性可以解决这个问题  

`dog.prototype = "猫科"`  
这样的话，创建实例属性的时候可以共享prototype属性了。  

理解可参考：http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html

# js中解决跨域问题的技术都有哪些（答了一个JSONP，原理没有答清楚）
### JSONP：  

原理是：动态插入script标签，通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。  

由于同源策略的限制，XmlHttpRequest只允许请求当前源（域名、协议、端口）的资源，为了实现跨域请求，可以通过script标签实现跨域请求，然后在服务端输出JSON数据并执行回调函数，从而解决了跨域的数据请求。  

优点是兼容性好，简单易用，支持浏览器与服务器双向通信。缺点是只支持GET请求。  

JSONP：json+padding（内填充），顾名思义，就是把JSON填充到一个盒子里  

`<script>`  
    `function createJs(sUrl){`  
        `var oScript = document.createElement('script');`  
        `oScript.type = 'text/javascript';`  
        `oScript.src = sUrl;`  
        `document.getElementsByTagName('head')[0].appendChild(oScript);`  
    `}`  
    `createJs('jsonp.js');`  
    `box({`  
       `'name': 'test'`  
    `});`  
    `function box(json){`  
        `alert(json.name);`  
    `}`  
`</script>`  


### CORS

服务器端对于CORS的支持，主要就是通过设置`Access-Control-Allow-Origin`来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。  

通过修改`document.domain`来跨子域  

将子域和主域的`document.domain`设为同一个主域.前提条件：这两个域名必须属于同一个基础域名!而且所用的协议，端口都要一致，否则无法利用`document.domain`进行跨域  

主域相同的使用`document.domain`

使用`window.name`来进行跨域  

window对象有个name属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个`window.name`的，每个页面对`window.name`都有读写的权限，`window.name`是持久存在一个窗口载入过的所有页面中的  

使用HTML5中新引进的`window.postMessage`方法来跨域传送数据  

还有flash、在服务器上设置代理页面等跨域方式。个人认为window.name的方法既不复杂，也能兼容到几乎所有浏览器，这真是极好的一种跨域方法。  

# 常见的兼容性问题
png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理.  

浏览器默认的margin和padding不同。解决方案是加一个全局的`*{margin:0;padding:0;}`来统一。  

IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。  

浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了`margin-left`或`margin-right`，margin值会加倍。  

`#box{ float:left; width:10px; margin:0 0 0 100px;}`  

这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入
_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

渐进识别的方式，从总体中逐渐排除局部。


  首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。

  接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

css
      `.bb{`  

       `background-color:#f1ee18;`/*所有识别*/  

      `.background-color:#00deff\9;` /*IE6、7、8识别*/  

      `+background-color:#a200ff;`/*IE6、7识别*/  

      `_background-color:#1e0bd1;`/*IE6识别*/  
      `}` 

怪异模式问题：漏写DTD声明，Firefox仍然会按照标准模式来解析网页，但在IE中会触发  
怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写DTD声明的好习惯。现在  
可以使用[html5](http://www.w3.org/TR/html5/single-page.html)

# 面试公司：IBM CDL

# js中三种通知框分别是哪三种
警告对话框：`alert()`   

确认对话框：`confirm()`    

提示框：`prompt()`    

# js中的事件冒泡机制
通俗易懂的来讲，事件冒泡就是当一个子元素的事件被触发的时候（如onclick事件），该事件会从事件源（被点击的子元素）开始逐级向上传播，触发父级元素的点击事件。  

理解可参考：https://www.cnblogs.com/qq9694526/p/5653728.html  

# Ajax的工作原理
Ajax的全称为Asynchronous JavaScript and XML，即为异步的JavaScript和XML。Ajax的原理简单来说通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。  

顺便讲一下Ajax实现的过程;  

(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.  

(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.  

(3)设置响应HTTP请求状态变化的函数.  

(4)发送HTTP请求.  

(5)获取异步调用返回的数据.  

(6)使用JavaScript和DOM实现局部刷新  

顺便再讲一下同步和异步的区别：  

同步是面向比特的传输，单位是帧，要求发送方和接收方需要在时钟上保持一致。  

而异步是面向字符的传输，单位是字符，异步是通知浏览器去做，但仅仅是通知，会继续执行下一步，等到结果返回回来了，浏览器会通知js执行回调。  

# ready()和onload()函数的区别
两个函数在功能上的作用都是：在页面加载的时候去执行这个函数或者动作，但是在如下三个方面有着比较大的区别  

1.执行时间
　　`window.onload`必须等到页面内包括图片的所有元素加载完毕后才能执行。 
　　`$(document).ready()`是DOM结构绘制完毕后就执行，不必等到加载完毕。

2.编写个数不同
　　`window.onload`不能同时编写多个，如果有多个window.onload方法，只会执行一个 
　　`$(document).ready()`可以同时编写多个，并且都可以得到执行

3.简化写法

　　`window.onload`没有简化写法 
　　`$(document).ready(function(){})`可以简写成`$(function(){})`

# 面试公司：触宝科技

# 主流浏览器的内核都有哪些？
主要介绍五大主流浏览器的内核：  

1、IE浏览器内核：Trident内核，也是俗称的IE内核；  

2、Chrome浏览器内核：统称为Chromium内核或Chrome内核，以前是Webkit内核，现在是Blink内核；  

3、Firefox浏览器内核：Gecko内核，俗称Firefox内核；  

4、Safari浏览器内核：Webkit内核；  

5、Opera浏览器内核：最初是自己的Presto内核，后来加入谷歌大军，从Webkit又到了Blink内核；  

# es6新特性？
新增模板字符串（为JavaScript提供了简单的字符串插值功能）、箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。）、for-of（用来遍历数据—例如数组中的值。）arguments对象可被不定参数和默认参数完美代替。ES6将promise对象纳入规范，提供了原生的Promise对象。增加了let和const命令，用来声明变量。增加了块级作用域。let命令实际上就增加了块级作用域。ES6规定，var命令和function命令声明的全局变量，属于全局对象的属性；let命令、const命令、class命令声明的全局变量，不属于全局对象的属性。。还有就是引入module模块的概念  

# null和undefined的区别
null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。  

当声明的变量还未被初始化时，变量的默认值为undefined。  

null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。  

undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：  

（1）变量被声明了，但没有赋值时，就等于undefined。  
（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。  
（3）对象没有赋值的属性，该属性的值为undefined。  
（4）函数没有返回值时，默认返回undefined。  
null表示"没有对象"，即该处不应该有值。典型用法是：  

（1） 作为函数的参数，表示该函数的参数不是对象。  

（2） 作为对象原型链的终点。  

# 面试公司:浦和数据

# js中的深复制和浅复制？
浅复制：只拷贝了基本的数据类型，仅仅指向被复制的内存地址，如果原地址的对象改变了，浅复制的对象也会改变  

深复制：在计算机中开辟了新的内存地址用于存放和复制对象  

js中的垃圾回收机制
标记清除（mark and sweep）  

这是JavaScript最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。  

垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了  

引用计数(reference counting)  

在低版本IE中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个 变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时 候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。  

在IE中虽然JavaScript对象通过标记清除的方式进行垃圾回收，但BOM与DOM对象却是通过引用计数回收垃圾的， 也就是说只要涉及BOM及DOM就会出现循环引用问题。  

# 什么是Event loop？ 
简单说，是在程序中设置两个线程：一个负责程序本身的运行，成为“主线程”；另一个负责主线程与其他线程之间的通信，被称为“Event loop”  

每当遇到IO时候，主线程会让event loop线程去通知相应的I/O程序，然后接着往后运行，所以不存在等待时间。等到I/O程序完成操作，Event loop线程会把结果返回给主线程。  

Promise中共有哪三种状态？工作机制是什么样的？

# 面试公司：EditorAi

# forEach和Map的区别？
1、forEach()返回值是undefined，不可以链式调用。  

2、map()返回一个新数组，原数组不会改变。  

3、没有办法终止或者跳出forEach()循环，除非抛出异常，所以想执行一个数组是否满足什么条件，返回布尔值，可以用一般的for循环实现，或者用Array.every()或者Array.some();  

4、$.each()方法规定为每个匹配元素规定运行的函数，可以返回 false 可用于及早停止循环。  

# "..."在es6中的作用是什么？
可参考：https://blog.csdn.net/qq_30100043/article/details/53391308

# 虚拟DOM
虚拟DOM就是将真实的DOM抽象成一个JavaScript对象。  

虚拟DOM具有批处理和高效的Diff算法，可以无需担心性能问题而随时“刷新”整个页面，因为虚拟DOM可以确保只对界面上真正变化的部分进行实际的DOM操作。  

变量提升的解释

# sessionStorage和LocaleStorgae的区别
LocaleStorage的生命周期是永久性的，即使关闭浏览器，数据也不会消失，除非采取主动删除数据的方法。  

SessionStorage的生命周期是在浏览器关闭之前，在整个浏览器关闭之前，数据时一直存在的。  

# 箭头函数与function函数的区别
1.箭头函数作为匿名函数,是不能作为构造函数的,不能使用new  

2.箭头函数不绑定arguments,取而代之用rest参数…解决  

3.箭头函数会捕获其所在上下文环境的 this 值，作为自己的 this 值  

# 面试公司：爱奇艺

# JS和JQuery中分别是如何删除DOM节点的方法
JQuery: 1.empty()方法：移除元素中的所有节点，并且清除元素中的所有文本，但是标记仍存在于DOM中  

        2.remove()方法：将元素自身移除，同时也会移除元素内部的一切。  

JS: removeChild()方法

如何通过CSS实现页面的三列布局？

# 面试公司:京东金融  

# 在浏览器地址栏输入，www.baidu.com到页面渲染完成这一过程经历了什么？
1.解析域名，找到目标主机的ip，缓存查找，若无--本地hosts文件查找，若无--网络查找，若无--DNS递归解析  

2.浏览器与网站建立TCP连接，这个过程就是你不得不了解的“三次握手”  

3.浏览器发起包含访问的url的get请求  

4.显示页面或者返回其他，返回状态码为200时表示服务器可以响应请求，返回报文。但很多情况下，会返回重定向码，在响应报文中找到重定向地址，重复第一次访问，这样做是为了负载均衡或者导入流量。  

# 如何通过CSS实现垂直居中？（好好做总结！）
1.`display:table`,利用table的text-align属性来实现  

2.只需要设置`line-height`等于目标对象的高度，比如height:200px,line-height:200px  

3.top设为50%，`margin-top`设为内容的一半，定位为绝对定位，当然要求是div的高度是固定的。  
