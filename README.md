# Interview-questions
Some question  i have come acrossed  in the interviews
本文旨在记录最近在面试中遇到的一些问题，解答来自于网络搜集，不具备解释上的权威性。

开放性问题：
1.问题介绍
2.项目介绍
3.希望从实习中获得哪些方面的成长
4.未来对自己的技术栈的学习规划是什么样的

技术性问题：
面试公司：caiCloud
js中实现异步编程的模式都有哪些

简单介绍一下原型链

js中解决跨域问题的技术都有哪些（答了一个JSONP，原理没有答清楚）

常见的兼容性问题
png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理.

浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。）

#box{ float:left; width:10px; margin:0 0 0 100px;}

这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入
_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

渐进识别的方式，从总体中逐渐排除局部。


  首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。

  接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

  css

      .bb{

       background-color:#f1ee18;/*所有识别*/

      .background-color:#00deff\9; /*IE6、7、8识别*/

      +background-color:#a200ff;/*IE6、7识别*/

      _background-color:#1e0bd1;/*IE6识别*/

      }


怪异模式问题：漏写DTD声明，Firefox仍然会按照标准模式来解析网页，但在IE中会触发
怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写DTD声明的好习惯。现在
可以使用[html5](http://www.w3.org/TR/html5/single-page.html)推荐的写法：`<doctype html>`

面试公司：IBM CDL
js中三种通知框分别是哪三种


js中的事件冒泡机制


Ajax的工作原理


ready()和onload()函数的区别

面试公司：触宝科技
主流浏览器的内核都有哪些？

es6新特性？
新增模板字符串（为JavaScript提供了简单的字符串插值功能）、箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。）、for-of（用来遍历数据—例如数组中的值。）arguments对象可被不定参数和默认参数完美代替。ES6将promise对象纳入规范，提供了原生的Promise对象。增加了let和const命令，用来声明变量。增加了块级作用域。let命令实际上就增加了块级作用域。ES6规定，var命令和function命令声明的全局变量，属于全局对象的属性；let命令、const命令、class命令声明的全局变量，不属于全局对象的属性。。还有就是引入module模块的概念

null和undefined的区别
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

面试公司:浦和数据
js中的深复制和浅复制？

js中的垃圾回收机制
标记清除（mark and sweep）

这是JavaScript最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。

垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了

引用计数(reference counting)

在低版本IE中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个 变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加1，如果该变量的值变成了另外一个，则这个值得引用次数减1，当这个值的引用次数变为0的时 候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为0的值占用的空间。

在IE中虽然JavaScript对象通过标记清除的方式进行垃圾回收，但BOM与DOM对象却是通过引用计数回收垃圾的， 也就是说只要涉及BOM及DOM就会出现循环引用问题。

什么是Event loop？

Promise中共有哪三种状态？工作机制是什么样的？

面试公司：EditorAi
forEach和Map的区别？

"..."在es6中的作用是什么？

虚拟DOM

变量提升的解释

sessionStorage和LocaleStorgae的区别

CSS中的Flex属性

箭头函数与function函数的区别



