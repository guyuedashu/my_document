# Dom 操作

## DOM 结构树（继承关系）

- Node  -- 原型为 EventTarget 原型为 Object 原型为 null

    - Document (文档)

        - HTMLDocument  document文档

        - XmlDoucment  xml文档

    - CharacterData 

        - Text --> 文本

        - Comment -->注释

    - Element(文档中的元素)

        - HTMLElement --> 元素超集

            - HTMLHeaderElement

            - HTMLBodyElement

            - HTMLTitleElement 

            - HTMLParagraphElement --> <p></p>

            - HTMLInputElement 

            - HTMLHDivElement

            - ........

    - Attr

## 节点（所有元素的超集接口）的四个属性

- nodeName: 节点名称 只读

- nodeValue : 节点的内容可读可写  只有注释节点和文本节点有，其他为null

- nodeType : 节点类型 只读

    - 元素节点 - 1 就是dom元素 例如：div、span、p等

    - 属性节点 - 2  dom.attributes 该元素的属性节点集合   dom.attributes[0].name  dom.attributes[0].value  可改变其值，不能改变名字

    - 文本节点 - 3  包括空格回车等

    - 注释节点 - 8    <!-- 888 -->

    - document - 9 一个 Document 节点。

    - 文档类型节点 -10  描述文档类型的 DocumentType 节点。例如 <!DOCTYPE html>  就是用于 HTML5 的。

    - documentFragment - 11  一个 DocumentFragment 节点

    - 还有一些已经弃用的

## 遍历节点树 (都为属性) 兼容性好 但是会选出来文本或者注释

- parentNode --> 父节点 只有一个 最顶级的节点为 document

- childNode --> 所有的儿子节点 

- firstChild --> 第一个节点

- lastChild --> 最后一个子节点

- nextSibling --> 紧接着的后一个兄弟节点

- previousSilbing --> 紧接着的前一个兄弟节点

## 遍历元素节点树 (都为属性) 不兼容都为IE9及以下不兼容

- parentElement --> 父元素节点 只有一个 最顶级的节点为 null不是document  （IE不兼容）

- children --> 所有的儿子元素节点 

- firstElementChild --> 第一个元素子节点（IE不兼容）

- lastElementChild --> 最后一个元素子节点 （IE不兼容）

- nextElementSibling --> 紧接着的后一个兄弟元素节点   （IE不兼容）

- previousElementSilbing --> 紧接着的前一个兄弟元素节点  （IE不兼容）

## 查找元素

- getElementById() 定义在Document.prototype 上，即Element节点不能访问

- getElementsByName() 定义在HTMLDocument.prototype上，即非html元素不能使用（例：xml,element）

- getElementsByTagName() 定义在Document.prototype上，和Element.prototype 兼容性最好

- HTMLDocument.prototype上定义了常用属性（例如：body,head）分别指向文档中的<body>和<head>标签

- Document.prototype定义了documentElement属性，指代文档根元素即 <html>标签

- getElementsByClassName 、querySelectorALl  、querySelector 在Document.prototype 和 Element.prototype 中都有定义。

## 增加元素 (document 对象的方法)

- document.createElement();

- document.createTextNode();

- document.createComment();

- document.createDocumentFragment();创建一个文档片段，当追加到文档中时，此元素会消失，不显示出来

## 插入元素 

- parentNode.appendChild(); (Node 对象的方法)  向父元素中加入一个子元素，只能为（Node）不能是（DOMString）只能传入一个参数  可以将已有的元素剪切到，另一个地方

- parentNode.append(); (Element 对象的方法)  是实验中的方法有兼容性问题，可以接收（DOMString、Node类型）参数可以为多个

- parentNode.insertBefore(a,b); 在parentNode元素中的 b元素之前插入a元素；且b必须已经在dom结构中；插入a在b之前

## 删除元素   

- parent.removeChild(son);  (Node 对象的方法)  返回被删除的对象
 
- dom.remove();  (Element 对象的方法)  没有返回值

## 替换   (Node 对象的方法)

- parent.replaceChild(new ,old);  会将旧元素返回

## Element

### 常用属性

- innerHTML 复制会覆盖其他元素

- innerText 赋值会覆盖其他元素（老火狐不兼容）常用

- textContent 和 innerText相同 （老IE不兼容 IE9 下）

### 常用方法

- setAttribute();

- getAttribute();

- getBoundingClientRect() 返回一个对象属性如下：但IE没有width 和 height (可以通过两个相减见得到) 兼容性很好  ** 但是不常用 **

    - left | top : 左上角坐标

    - bottom | right : 右下角坐标

    - windth | height 该元素宽高

    - x | y 貌似就是左上角一样

    ~ 返回得结构为静态快照并不会随之改变，其坐标相对于视口

- offsetWidth | offsetHeight  ** 常用 ** 视觉上得尺寸

- offsetLeft | offsetTop  求出相对于定位父元素的位置,如果没有就是body元素

- offsetParent 返回最近有定位的父元素没有则为null


![DOM 结构树](https://img2020.cnblogs.com/blog/1708982/202004/1708982-20200405191000886-1768397487.png)
