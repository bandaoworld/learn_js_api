# 1. DOM简介
## 1.1 什么是DOM
文档对象模型（Document Object Model，简称 DOM），是 W3C 组织推荐的处理可扩展标记语言（HTML或者XML）的标准编程接口
W3C 已经定义了一系列的 DOM 接口，通过这些 DOM 接口可以改变网页的内容、结构和样式。
## 1.2 DOM树
1. 文档
   1. 根元素`<html>`
      1. 元素`<head>`
         1. 元素`<title>`
            1. 文本“文档标题”
      2. 元素`<body>`
         1. 元素`<a>`
            1. 文本“我的链接”
            2. 属性：href
         2. 元素`<h1>`
            1. 文本”我的标题“

- 文档：一个页面就是一个文档，DOM中使用doucument来表示
- 元素：页面中的所有标签都是元素，DOM中使用 element 表示
- 节点：网页中的所有内容都是节点（标签，属性，文本，注释等），DOM中使用node表示

# 2. 获取元素
## 2.1 如何获取页面元素
DOM在我们实际开发中主要用来操作元素。
我们如何来获取页面中的元素呢?
获取页面中的元素可以使用以下几种方式:
- 根据 ID 获取
- 根据标签名获取
- 通过 HTML5 新增的方法获取
- 特殊元素获取

## 2.2 根据ID获取
使用  getElementByld()  方法可以获取带ID的元素对象
`doucument.getElementByld('id名')`
使用  console.dir()  可以打印我们获取的元素对象，更好的查看对象里面的属性和方法。
```html
<div id="time">
    2022-5-27
</div>
<script>
    // 1. 因为我们文档页面从上往下加载，所以先得有标签 所以我们script写到标签的下面
    // 2. get 获得 element 元素 by 通过 驼峰命名法 
    // 3. 参数 id是大小写敏感的字符串
    // 4. 返回的是一个元素对象
    var timer = document.getElementById("time");
    console.log(timer);
    console.log(typeof timer);
    // 5. console.dir 打印我们返回的元素对象 更好的查看里面的属性和方法
    console.dir(timer)
</script>
```
## 2.3 根据标签名获取
根据标签名获取，使用  getElementByTagName()  方法可以返回带有指定标签名的对象的集合
`doucument.getElementsByTagName('标签名');`
- 因为得到的是一个对象的集合，所以我们想要操作里面的元素就需要遍历
- 得到元素对象是动态的
- 返回的是获取过来元素对象的集合，以伪数组的形式存储
- 如果获取不到元素，则返回为空的伪数组(因为获取不到对象)
```html
<ul>     
   <li>知否知否，应是等你好久</li>    
   <li>知否知否，应是等你好久</li>    
   <li>知否知否，应是等你好久</li>    
   <li>知否知否，应是等你好久</li>    
   <li>知否知否，应是等你好久</li>
</ul> 
<script>     
   // 1.返回的是获取过来元素对象的集合 以伪数组的形式存储     
   var lis = document.getElementsByTagName('li');     
   console.log(lis);     
   console.log(lis[0]);    
   // 2.依次打印,遍历     
   for (var i = 0; i < lis.length; i++) {         
      console.log(lis[i]);     
   }     
   // 3.如果页面中只有 1 个 li，返回的还是伪数组的形式     
   // 4.如果页面中没有这个元素，返回的是空伪数组 
</script>
```
## 2.4 根据标签名获取
还可以根据标签名获取某个元素（父元素）内部所有指定标签名的子元素,获取的时候不包括父元素自己
注意：父元素必须是单个对象(必须指明是哪一个元素对象)，获取的时候不包括父元素自己
```html
element.getElementsByTagName('标签名') 
ol.getElementsByTagName('li'); 
<script>   
   //element.getElementsByTagName('标签名'); 父元素必须是指定的单个元素     
   var ol = document.getElementById('ol');     
   console.log(ol.getElementsByTagName('li')); 
</script> 
```
## 2.5 通过H5新增方法获取
### 2.5.1 getElementsByClassName
根据类名返回元素对象合集 `document.getElementsByClassName('类名')`
### 2.5.2 document.querySelector
根据指定选择器返回第一个元素对象 `document.querySelector('选择器'); `
```html
<div class="box">盒子1</div>
<script>
   // 2. querySelector 返回指定选择器的第一个元素对象  切记 里面的选择器需要加符号 .box  #nav
   var firstBox = document.querySelector('.box');
   console.log(firstBox);
</script>
```
### 2.5.3 document.querySelectorAll
根据指定选择器返回所有元素对象 `document.querySelectorAll('选择器'); `
注意：querySelector  和  querySelectorAll  里面的选择器需要加符号,比如:  document.querySelector('#nav');
### 2.5.4 例子
```js
// 1. getElementsByClassName 根据类名获得某些元素集合
var boxes = document.getElementsByClassName('box');
console.log(boxes);
// 2. querySelector 返回指定选择器的第一个元素对象  切记 里面的选择器需要加符号 .box  #nav
var firstBox = document.querySelector('.box');
console.log(firstBox);
var nav = document.querySelector('#nav');
console.log(nav);
var li = document.querySelector('li');
console.log(li);
// 3. querySelectorAll()返回指定选择器的所有元素对象集合
var allBox = document.querySelectorAll('.box');
console.log(allBox);
var lis = document.querySelectorAll('li');
console.log(lis);
```
## 2.6 获取特殊元素
### 2.6.1 获取body元素
返回body元素对象 `document.body; `
### 2.6.2 获取html元素
返回html元素对象 `document.documentElement;`
# 3. 事件基础
## 3.1 事件概述
JavaScript 使我们有能力创建动态页面，而事件是可以被 JavaScript 侦测到的行为。
简单理解： 触发— 响应机制。
网页中的每个元素都可以产生某些可以触发 JavaScript 的事件，例如，我们可以在用户点击某按钮时产生一个事件，然后去执行某些操作。
## 3.2 事件三要素
1. 事件源(谁)
2. 事件类型(什么事件)
3. 事件处理程序(做啥)
```html
<button id="btn">唐伯虎</button>
<script>
   // 点击一个按钮，弹出对话框
   // 1. 事件是有三部分组成  事件源  事件类型  事件处理程序   我们也称为事件三要素
   //(1) 事件源 事件被触发的对象   谁  按钮
   var btn = document.getElementById('btn');
   //(2) 事件类型  如何触发 什么事件 比如鼠标点击(onclick) 还是鼠标经过 还是键盘按下
   //(3) 事件处理程序  通过一个函数赋值的方式 完成
   btn.onclick = function () {
      alert("bandao")
   };
</script>
```
## 3.3 执行事件的步骤
1. 获取事件源
2. 注册事件(绑定事件)
3. 添加事件处理程序(采取函数赋值形式)
```js
// 点击div 控制台输出 我被选中了
// 1. 获取事件源
var div = document.querySelector('div');
// 2.绑定事件 注册事件
// div.onclick 
// 3.添加事件处理程序 
div.onclick = function () {
   console.log('我被选中了');
}
```
## 3.4 鼠标事件
|  鼠标事件   |     触发条件     |
| :---------: | :--------------: |
|   onclick   | 鼠标点击左键触发 |
| onmouseover |   鼠标经过触发   |
| onmouseout  |   鼠标离开触发   |
|   onfocus   | 获得鼠标焦点触发 |
|   onblur    | 失去鼠标焦点触发 |
| onmousemove |   鼠标移动触发   |
|  onmouseup  |   鼠标弹起触发   |
| onmousedown |   鼠标按下触发   |
# 4. 操作元素
JavaScript 的 DOM 操作可以改变网页内容、结构和样式，我们可以利用 DOM 操作元素来改变元素里面的内容 、属性等。注意以下都是属性
## 4.1 改变元素内容
从起始位置到终止位置的内容，但它去除html标签，同时空格和换行也会去掉。`element.innerText`
起始位置到终止位置的全部内容，包括HTML标签，同时保留空格和换行。`element.innerHTML `
```html
<div></div>
<p>
   我是文字
   <span>123</span>
</p>
<script>
   // innerText 和 innerHTML的区别 
   // 1. innerText 不识别html标签 非标准  去除空格和换行
   var div = document.querySelector("div");
   // div.innerText = '<strong>今天是：</strong> 2019';
   // 2. innerHTML 识别html标签 W3C标准 保留空格和换行的
   div.innerHTML = '<strong>今天是：</strong> 2019';
   // 这两个属性是可读写的  可以获取元素里面的内容
   var p = document.querySelector('p');
   console.log(p.innerHTML);
   console.log(p.innerText);
</script>
```
## 4.2 改变元素属性
```js
// img.属性 
img.src = "xxx"; 
input.value = "xxx"; 
input.type = "xxx"; 
input.checked = "xxx";
input.selected = true / false; 
input.disabled = true / false; 
```
## 4.3 改变样式属性
我们可以通过 JS 修改元素的大小、颜色、位置等样式。
- 行内样式操作
```js
// element.style 
div.style.backgroundColor = 'pink'; 
div.style.width = '250px';
```
- 类名样式操作
```js
// element.className 
```
注意：
1. JS里面的样式采取驼峰命名法，比如 fontSize ，backgroundColor
2. JS 修改 style 样式操作 ，产生的是行内样式，CSS权重比较高
3. 如果样式修改较多，可以采取操作类名方式更改元素样式
4. class 因为是个保留字，因此使用className 来操作元素类名属性
5. className 会直接更改元素的类名，会覆盖原先的类名
```html
<body>     
   <div class="first">文本</div>     
   <script>         
      // 1. 使用 element.style 获得修改元素样式  如果样式比较少 或者 功能简单的情况下使用
      var test = document.querySelector('div');         test.onclick = function() {             
         // this.style.backgroundColor = 'purple';             
         // this.style.color = '#fff';             
         // this.style.fontSize = '25px';             
         // this.style.marginTop = '100px';             
         // 让我们当前元素的类名改为了 change             
         // 2. 我们可以通过 修改元素的className更改元素的样式 适合于样式较多或者功能复杂的情况             
         // 3. 如果想要保留原先的类名，我们可以这么做 多类名选择器             
         // this.className = 'change';             
         this.className = 'first change';         
      }     
   </script> 
</body>
```
## 4.4 总结
操作元素
1. 操作元素内容
   - innerText
   - innerHTML
2. 操作常见元素属性
   - src、href、 title、 alt等
3. 操作表单元素属性
   - type、value、 disabled等
4. 操作元素样式属性
   - element.style
   - className











