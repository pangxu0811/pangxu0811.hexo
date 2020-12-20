---
title: ES6的常用语法
categories:
- [编程开发,前端,JS]
tags:
- 开发
- 前端
- JS
---

  <h2><a name="t0"></a><a id="var_0"></a>var</h2>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">之前，js定义变量只有一个关键字：var
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>var有一个问题，就是定义的变量有时会莫名奇妙的成为全局变量。</p>
<p>例如这样的一段代码：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">for(var i = 0; i &lt; 5; i++){
    console.log(i);
}
console.log("循环外：" + i)
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>你猜下打印的结果是什么？<br>
<img src="https://img-blog.csdnimg.cn/20190217131801947.png" alt=""></p>
<h2><a name="t1"></a><a id="let_15"></a>于是就有了let</h2>
<p>let所声明的变量，只在let命令所在的代码块内有效。</p>
<p>我们把刚才的var改成let试试：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">for(let i = 0; i &lt; 5; i++){
    console.log(i);
}
console.log("循环外：" + i)
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p><img src="https://img-blog.csdnimg.cn/20190217132338186.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTU1Njk2Mw==,size_16,color_FFFFFF,t_70" alt=""></p>
<h2><a name="t2"></a><a id="const_27"></a>还有一个常量const</h2>
<p>const声明的变量是常量，不能被修改<br>
<img src="https://img-blog.csdnimg.cn/20190217132437531.png" alt=""></p>
<h2><a name="t3"></a><a id="_30"></a>重要的表达式（解构表达式）</h2>
<p><strong>数组解构</strong><br>
比如有一个数组：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">let arr = [1,2,3]
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>我想获取其中的值，只能通过角标。ES6可以这样：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">let [x,y,z] = arr;// x，y，z将与arr中的每个位置对应来取值
// 然后打印
console.log(x,y,z);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p><img src="https://img-blog.csdnimg.cn/20190217132942331.png" alt=""><br>
<strong>对象解构</strong><br>
例如有个person对象：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">const person = {
    name:"jack",
    age:21,
    language: ['java','js','css']
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>我们可以这么做：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">// 解构表达式获取值
const {name,age,language} = person;
// 打印
console.log(name);
console.log(age);
console.log(language);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p><img src="https://img-blog.csdnimg.cn/20190217133044814.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTU1Njk2Mw==,size_16,color_FFFFFF,t_70" alt=""><br>
如过想要用其它变量接收，需要额外指定别名：<br>
<img src="https://img-blog.csdnimg.cn/20190217133130644.png" alt=""><br>
{name:n}：name是person中的属性名，冒号后面的n是解构后要赋值给的变量。</p>
<h2><a name="t4"></a><a id="_69"></a>质的改变（函数优化）</h2>
<p><strong>函数参数默认值</strong><br>
在ES6以前，我们无法给一个函数参数设置默认值，只能采用变通写法：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)"> function add(a , b) {
        // 判断b是否为空，为空就给默认值1
        b = b || 1;
        return a + b;
    }
    // 传一个参数
    console.log(add(10));
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>现在可以这么写：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">function add(a , b = 1) {
    return a + b;
}
// 传一个参数
console.log(add(10));
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p><strong>箭头函数（类lamada表达式（单）箭头改成双箭头）</strong><br>
ES6中定义函数的简写方式：</p>
<p>一个参数时：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">var print = function (obj) {
    console.log(obj);
}  
function print (obj) {
    console.log(obj);
}
// 简写为：
var print2 = obj =&gt; console.log(obj);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>多个参数：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">// 两个参数的情况：
var sum = function (a , b) {
    return a + b;
}
// 简写为：
var sum2 = (a,b) =&gt; a+b;
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>代码不止一行，可以用{}括起来</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">var sum3 = (a,b) =&gt; {
    return a + b;
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p><strong>对象的函数属性简写</strong><br>
比如一个Person对象，里面有eat方法：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">let person = {
    name: "jack",
    // 以前：
    eat: function (food) {
        console.log(this.name + "在吃" + food);
    },
    // 箭头函数版：
    eat2: food =&gt; console.log(person.name + "在吃" + food),// 这里拿不到this
    // 简写版：
    eat3(food){
        console.log(this.name + "在吃" + food);
    }
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p><strong>箭头函数结合解构表达式</strong><br>
比如有一个函数：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">const person = {
    name:"jack",
    age:21,
    language: ['java','js','css']
}

function hello(person) {
    console.log("hello," + person.name)
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>如果用箭头函数和解构表达式</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">var hi = ({name}) =&gt;  console.log("hello," + name);
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<h2><a name="t5"></a><a id="_161"></a>模块化</h2>
<p><strong>什么是模块化</strong></p>
<p>模块化就是把代码进行拆分，方便重复利用。类似java中的导包：要使用一个包，必须先导包。</p>
<p>而JS中没有包的概念，换来的是 模块。</p>
<p>模块功能主要由两个命令构成：export和import。</p>
<ul>
<li>export命令用于规定模块的对外接口，</li>
<li>import命令用于导入其他模块提供的功能。</li>
</ul>
<p><strong>export</strong></p>
<p>比如我定义一个js文件:hello.js，里面有一个对象：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">const util = {
    sum(a,b){
        return a + b;
    }
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>我可以使用export将这个对象导出：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">const util = {
    sum(a,b){
        return a + b;
    }
}
export util;
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>当然，也可以简写为：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">export const util = {
    sum(a,b){
        return a + b;
    }
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>export不仅可以导出对象，一切JS变量都可以导出。比如：基本类型变量、函数、数组、对象。</p>
<p>当要导出多个值时，还可以简写。比如我有一个文件：user.js：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">var name = "jack"
var age = 21
export {name,age}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>省略名称</p>
<p>上面的导出代码中，都明确指定了导出的变量名，这样其它人在导入使用时就必须准确写出变量名，否则就会出错。</p>
<p>因此js提供了default关键字，可以对导出的变量名进行省略</p>
<p>例如：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">// 无需声明对象的名字
export default {
	sum(a,b){
        return a + b;
    }
}
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>这样，当使用者导入时，可以任意起名字</p>
<p><strong>import</strong></p>
<p>使用export命令定义了模块的对外接口以后，其他 JS 文件就可以通过import命令加载这个模块。</p>
<p>例如我要使用上面导出的util：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">// 导入util
import util from 'hello.js'
// 调用util中的属性
util.sum(1,2)
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style=""></ul></pre>
<p>要批量导入前面导出的name和age：</p>
<pre class="prettyprint"><code class="has-numbering" onclick="mdcp.copyCode(event)">import {name, age} from 'user.js'
console.log(name + " , 今年"+ age +"岁了")
<div class="hljs-button {2}" data-title="复制"></div></code><ul class="pre-numbering" style="">

                 
