# 前端模块化

- 优点：模块化，按需加载、更好的分离、提高复用性和维护性

- 缺点：请求数量过多、顺序不能随意切换；

> 演进过程

- function模式； 
```javascript
    function a(){
        console.log();
    }
```

- namespace模式; 但是属性容易被更改，没有私；直接暴漏在window上
```javascript
    var obj = {
        age:88,
        say:function(){
             console.log();
        }
    }
```

- IIFE（立即执行）模式; JQ为典型,传入window为形参
```javascript
   (function(w){
       w.age = {
            age:88,
            say:function(){
                console.log();
            }
       }
   })(window)
```

## 模块化规范

1. Common.js

### 说明

> 特点 ： 每个文件都可以当作一个文件；

> node.js 基于此规范；

> 服务端：模块的加载时，运行去同步加载的，

> 浏览器端：模块需要提前打包处理；（不可能，运行时才去由浏览器发送请求，会造成页面卡顿、白屏、闪烁）；require模块浏览器不支持

- 暴露模块

   - module.exports = value;

   - exports.xxx = value;

   - exports 属性本身就是空对象，暴漏的本质就是向此对象上加属性或者覆盖exports对象。

- 引入模块

    - require(../xxx.js) 填入路径 | 模块名 

    - 第三方模块： xxx模块名

    - 自定义模块：xxx.js所在的文件路径

### 实现

- 服务端：

- 浏览器端：

    - browserify



2. Amd

3. ES6

4. CMD (了解)