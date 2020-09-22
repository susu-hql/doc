## vConsole介绍

vConsole是一款由微信公众平台前端团队打造的前端调试面板，专治手机端看log难题。
请在手机上打开链接：http://wechatfe.github.io/vconsole/demo.html

目前vConsole自带有5个面板，默认为“日志”面板，负责展示log。默认情况下，vConsole的面板是隐藏起来的。我们可以点击右下角的“面板”悬浮按钮来显示vConsole面板。

### 日志面板
-----

第一个是日志面板(log)主要就是我们打印显示的一些数据，细心的同学可能会发现上方的log控制台上有四种类型的日志。
与电脑端的Developer Tools一样，开发者可以通过调用不同的方法来打出不同的颜色，以便快速区分日志类型：

```javascript
console.log('foo'); // 白底黑字  
console.info('bar'); // 白底紫字  
console.warn('foo'); // 黄底黄字  
console.error('bar'); // 红底红字
```

### “系统”面板
------------------------

第二个是“系统”面板(system)，vConsole会自动将一些基础信息（如系统版本）打印出来，方便开发者定位问题。
若页面是在微信内置浏览器中打开的，vConsole还会打印出微信版本号、当前网络类型等额外信息。

### Network面板
----------------------

第三个是Network面板，所有 XMLHttpRequest 请求都会被显示到 Network tab 中。
若不希望一个请求显示在面板中，可添加属性 _noVConsole = true 到 XHR 对象中：

```javascript
var xhr = new XMLHttpRequest();
xhr._noVConsole = true; // 不会显示到 tab 中
xhr.open("GET", 'http://example.com/');
xhr.send();
```

### Element面板
------------

第四个是Element面板，可以查看页面的dom结构。

### Storage面板
----------

第五个是Storage面板，可以查看本地存储的数据，包括Cookies、localStorage及sessionStorage。

注意点：

    vconsole 这个插件源码里面是依赖 html dom api 来实现的，如果你所使用的的环境不支持 dom，与原有的浏览器内核有差异，可能无法使用。
    一般的 web-view 嵌套网页是可以用的，或者手机浏览器都是OK的。如果是小程序或者第三方软件解析html需要查看一下原理。
    至于微信小程序为什么有，因为别人就是内置的，自己写适配了自己。
    
## vConsole使用

官方教程地址：https://github.com/Tencent/vConsole/blob/dev/doc/tutorial_CN.md

### 原生使用

也可以使用cdn方式引入，这里列举了所有版本的js地址，可以随意选择一个版本复制引入。然后在页面 里面加入初始化代码。

示例代码如下：

```javascript
<script src="https://cdn.bootcss.com/vConsole/3.3.4/vconsole.min.js"></script>
<script>
  // 初始化
  var vConsole = new VConsole();
  console.log('Hello world');
</script>
```

    为什么要在head引入，这样能尽量将你所有的的console都打印出来，vconsole原理是只有 new 初始化的时候才会插入dom，并改写监听console方法。

### es6 webpack使用

示例代码如下：

 ```javascript
 npm install vconsole
或者
cnpm install vconsole
或者
yarn add vconsole
 
然后设置个环境变量作为区分线上线下环境，比如：
 
import VConsole from 'vconsole';
 
const isDebug = true;
// 本地开发调试注入vConsole
if (isDebug) {
    new VConsole();
}
 ```
 
    引入模块后，vConsole会有一小段时间用于初始化工作，在渲染出面板HTML之前将无法立即打印log。
    因此，若要在引入模块后立即打印log，应使用vConsole.ready()方法：
 
 ```javascript
 vConsole.ready(function() { 
     console.log('Hello World'); 
 });
 ```
 
    手机前端开发调试工具介绍到这里就结束了。
 
 
 ## 更多扩展
  
Eruda 手机网页前端调试面板  https://www.oschina.net/p/eruda?hmsr=aladdin1e1
 
eruda官方教程    https://github.com/liriliri/eruda/blob/master/doc/README_CN.md

vConsole官方教程 https://github.com/Tencent/vConsole/blob/dev/doc/tutorial_CN.md
