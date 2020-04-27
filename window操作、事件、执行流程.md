## 滚动条距离

- window.pageXOffset | window.pageYOffset (IE8 集iE8 以下不兼容)

** 下面两组都是IE8 的解决方法 但是由于兼容性混乱 两种方法  俩组方法互斥，有一组方法有值的话另一组则为0 **

** 解决方法将两个值相加就可以解决问题 **

- document.body.scrollLeft |  document.body.scrollTop

- document.documentElement.scrollTop | document.documentElement.scrollLeft 

## 滚动条滚动

- window.srcoll(x,y) | window.scrollTo(x,y) 用法相同  滚动到指定位置

-  window.srcollBy(x,y) 会在当前滚动位置相加  可以为负数

## 标准模式和混杂、怪异模式

- html文档最上面的声明文档 （<!DOCTYPE html>）被删除掉就会启动怪异模式；

- 怪异模式下浏览器将会摒弃最新语法，向后兼容

- document.compatMode 两个取值可以判断标准还是怪异模式
    - CSS1Compat  标准模式
    - BackCompat  怪异模式

## 视口尺寸

- window.innerWinth | window.innerHeight  (IE8 及以下iE8 以下不兼容)

** 下面两组针对IE  **

- document.documentElement.clientWidth | document.documentElement.clientHeight    (标准浏览器都兼容)

- document.body.clientWidth | document.body.clientHeight  (适用于怪异模式的浏览器)



## CSS 查看以及操作

- dom.style.prop 可读可写；JS唯一可以写入样式的方法（间接改变）；写在行间才会获得此属性；获得值可能会与页面显示的不一样

- getComputedStyle(dom,pseudo); 
只读；获得的是浏览器解决样式冲突后最终显示在页面的属性值；获得值为转换过的绝对值；比如：颜色：为RGB；em : 100px;
    - dom 元素

    - pseudo 伪元素 可以获得伪元素，一般为null


> IE不兼容

- IE 方法：dom.currentStyle; 属性 只读； 获得值为原始值；就是写什么出来的就是什么；


## 事件

### 事件添加删除

- 行间

- dom.onclick

- dom.addEventLitener(type,fun,bubbling) | dom.removeEventListEvent(); 参数和绑定一致

    - IE9 以下不兼容；相同函数只会执行一次（有去重）；

> IE 

- attachEvent();  attachEvent('on' + click,function)  使用和addEventLitener相同但是，没有第三个参数

### 事件模型

- 事件冒泡 （结构嵌套即代码）

- 事件捕获 （IE没有老版本火狐没有）

> focus，blur，change，submit，reset，select 没有冒泡

> 执行顺序: 捕获事件 >> 事件执行 >> 事件冒泡  (两个事件同时存在时，安绑定顺序执行)

### 取消冒泡

>W3C 标准

- event.stopPropagation();  

> IE 特有

- event.cancelBubble = true;

### 阻止默认事件

> 默认事件：表单提交、a标签跳转、右键菜单等等。。。

- return false; 以句柄的方式注册事件才会有效 例如document.oncontextmenu = function(){return fasle}  兼容性最好

- event.preventDefault(); W3C标准，IE9以下不兼容

- event.returnValue = false;  兼容IE

>  \<a href="javascript:void(0);">dasdad</a>  0|false|'' 都可以取消跳转功能

### 事件对象

- 事件对象 event 系统会传入

- IE 在window.event 上

### 事件源对象

- event.target 火狐只有这个

- event.srcElement IE 只有这个

- chrome 都有

## event 属性

- pageX | pageY  相对于页面（body）的距离，包括了滚动条滚动过的距离

- screenX | screenY 相对于整个电脑屏幕的距离 ，包括了上面的导航栏

- offsetX | offsetY 相对于最近定位父类元素的x,y

- clientX | clientY 相对于可视区域的x，y坐标 也就是视口

- x | y  和  clientX相同


### 键盘事件

- onkeydown 除了fn都有, 但是监听不了大小写

- onkeypress  只能监听Ascii码有的键；字符类监听  有一个属性charCode 代表字符的ASCll 

- onkeyup  

### 其他事件

- focus 聚焦

- blur 失去焦点

- change 聚焦和失去焦点 内容相同不触发，不同才触发

- input 一直会触发

- srcoll document事件 可以实现fixed定位
### 移动端

- touchstart

- touchmove

- touchend

# Dom执行流程  JS时间线

1. 创建Document对象，开始解析web页面。解析HTML元素和文本。这个阶段document.readyState = 'loading'

2. 遇到link外部css，创建线程加载，并继续解析文档。

3. 遇到script外部JS，并没有设置async、defer，浏览器加载，阻塞，等待加载完，再解析文档

4. 遇到script外部JS，并设置了async、defer，浏览器创建线程加载，继续解析文档

    - async 加载完就执行 加载完就执行

    - defer html解析完，才执行 引入顺序依次执行

    - 脚本中禁止使用document.write Ps:他会清空文档流

5. 遇到img等，先正常细节dom结构，然后浏览器异步加载src，并继续解析文档

6. 当文档解析完成，document.readyState = 'interactive'

7. 文档解析完成后，所有设置有defer 的脚本会按照引入顺序，依次执行；

8. document对象触发DOMContentLoaded事件，这也标志程序执行从同步脚本执行阶段，到事件驱动阶段。也就是当前可以接受点击等，事件了。

9. 当所有async的脚本加载完成并执行后、img等加载完成后，document.readyState = complete 触发load事件。

10. 从此，以异步响应方式处理用户输入、网络事件等。


![](https://img2020.cnblogs.com/blog/1708982/202004/1708982-20200412145009176-767872613.webp)

