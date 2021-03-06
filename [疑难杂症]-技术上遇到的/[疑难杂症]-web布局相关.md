### 20180728
**关键词**： 拖拽 鼠标事件 Drag MouseUp  
1. 拖拽浏览器中特定元素，触发浏览器的默认拖拽行为，从而导致开始时按下鼠标触发了mouseDown，之后移动鼠标触发了drag（浏览器默认），但drag触发后，在drag过程中松开鼠标，浏览器无法触发mouseUp。直接导致在mouseDown-mouseUp过程中的逻辑无法结束。

答:  答案丢了 ？？

---

### 20180730
1. 父容器的`display:flex,position:abosolute,`子元素`positiong:abosolute`时会怎样？

答：子元素会相对父容器进行布局，效果跟父容器是position:relative，子元素是position:abosolute的效果一样。 在chrome浏览器中，父容器的flex还会影响子元素,如果子元素只设置了right/left，没有设置top/bottom的话。

---

### 20180731
1.父容器使用了transform，在父容器下的子元素(比如弹窗)如果使用了fixed布局，会导致子元素显示位置混乱。

答：结果造成了fixed布局相对transform变成了abosolute布局效果。不再相对页面了。

---

### 20180801
1.pre页面元素，支持自动换行且支持内容中带的换行符‘\r\n’.

---

### 20180802
1. react中元素使用props：dangerouslySetInnerHTML，引发xss(跨站脚本攻击)安全性问题。
解决方案：对输出的内容做xss安全性过滤，防止执行了脚本。

dangerouslySetInnerHTML使用方法：
```
<div className={className} dangerouslySetInnerHTML={{__html: html}} ></div>
```
` //这里要对'html'内容过滤，才能防止xss攻 `
作用：保留原始html标签，比如换行标示'<br/>'符等。

注：react.js 避免使用 dangerouslySetInnerHTML,可以在大部分情况下避免 XSS 攻击。

---

### 20180804
1. 设置了父容器透明度，再去设置该容器的子元素透明度，导致子元素透明效果与父容器透明叠加。即子元素透明被父容器透明度影响。
问题重现：父容器透明度设置：`opacity：0.7; `子元素透明度设置：0.9； 结果子元素透明度是0.7x0.9的效果。（这有疑惑？是效果重叠还是子继承了父的透明度）

答：设置父容器的透明度采用：rgba(x,x,x,0.7)方式，而不是直接设置opactiy属性。

---

### 0180807
1. web页面双击，会自动选中文本，图片等html元素，元素上会自动附加一层背景色。但有时不想产生这种效果，怎么办呢？

答：设置元素的css样式‘user-select’为‘none’即可，这种方法比较通用，对各类浏览器兼容性较好。

其他作用：禁止用户选中页面上内容的效果等。
参考帖子：[w3cui](http://www.w3cui.com/?p=141)

---

### 20180810
1.client往server发送请求，怎样自动带上cookie？
2.怎样支持跨域访问？？

答：
*1. 前端进行数据请求有：普通的ajax(json)请求，jsop跨域请求，cors跨域请求，fetch请求...PC端这些请求方式中，普通的ajax(json)请求和jsop跨域请求是默认携带cookie的，而cors跨域请求和fetch请求默认是不携带cookie的。因此，当我们的请求需要携带cookie时，我们就要对cors跨域请求和fetch请求这两中请求方式进行特殊配置处理。
        针对ajax不支持自带cookie的，需要对ajax进行配置：`credentials: 'include'`。
*2. 两步配置：(1).配置client端，支持跨域访问； (2).配置服务端，支持跨域访问。
fetch请求方式：
```
fetch('/community/getCommunityActivityByCommunityId', {
    method: "POST",
    headers: {
        "Content-Type": "application/x-www-form-urlencoded"
    },
credentials: 'include',
    body:"communityId="+this.props.location.query.communityId
})
    .then((res) => { return res.json(); })
    .then((data) => {
       //请求成功
    })
    .catch((e) => {
//报错
    });
```
我们要在请求头中添加上这个配置：
```
credentials: 'include'
```
cors跨域请求方式：
```javascript
$.ajax({
    type: "post",
    url:"/activity/queryPrizeRecord",
    dataType: "json",
　　 xhrFields: {
        withCredentials: true
    },
    crossDomain: true,
    data:{},
    success:function(data){

    },
    error:function(e){
    }
})
```
我们要在请求头中添加上这个配置：
```
　　xhrFields: {
        withCredentials: true
    },
    crossDomain: true
```
配上对应的特殊配置后，cookie就会被带上去请求数据了
以上参考链接：[cnblogs-zhuotiabo](https://www.cnblogs.com/zhuotiabo/p/6230521.html)

其他：同源不跨域要求：协议，域名，端口一致。 eg：http://www.example.com:81
跨域的目的：1.共享cookie；2.跨域获取dom; 3.读写其他窗口的LocalStorage; 
ajax实现跨域几种方法：

>*（1）JSONP 
>*（2）WebSocket 
>*（3）CORS

以上参考链接：[csdn-u013084331](https://blog.csdn.net/u013084331/article/details/51114288)

---

### 20180814
1.web平台，前端怎样支持二开，在不影响本身标准产品的前提下渲染客户自己开发的组件？

答：
*方案一：在标准产品中开发一个自定义组件，允许配置需要动态加载的js，css文件。之后在渲染这个自定义组件时，动态加载配置的js，css文件并把一个dom节点塞进去，让动态加载的js以此dom节点进行组件渲染，想要什么就渲染什么并可自己控制样式，同时可以暴露一些通信api进去共调用。
*方案二：？

---

### 20180816(再编辑)
方案一(具体执行细节)：
 * 1.在要集成第三方组件A的地方动态加载A的js和其他相关文件；
 * 2.加载js后，第三方组件A会立即执行，并在页面全局window下挂接一个对象Aobj(这个名字是固定的，第三方组件A自己取的); 
 * 3.利用Aobj对象，调用其初始化接口，创建一个组件A的实例(创建实例时，传入一个页面元素的id，一般为div元素。作为组件A的实例对象的父元素，从而知道自己渲染在哪里，用户可以看到)；
 * 4.第三方组件A会暴露出一些接口，通过这些接口从而支持控制或回调，使得集成人员可以去第三方组件进行交互。

---

### 20180815
1. react生命周期，前后执行被自己忽略的细节整理：
答：
**componentWillMount**：
在这个方法内调用setState，render()知道state发生变化，并且只执行一次(不会引发多次render)。
**render()**: 
如果不想渲染可以返回null或者false，这种场景下，react渲染一个<noscript>标签，当返回null或者false时，ReactDOM.findDOMNode(this)返回null ;render()方法是很纯净的，这就意味着不要在这个方法里初始化组件的state，每次执行时返回相同的值，不会读写DOM或者与服务器交互。(即不要在render方法里获取dom对象或者与server端通信并处理数据)
**shouldComponentUpdate**：
这个方法在初始化render时不会执行，当props或者state发生变化时执行，并且是在render之前。

返回false时，就不会执行render()方法，componentWillUpdate和componentDidUpdate方法也不会被调用。

**componentWillUpdate**：
当props和state发生变化时执行，并且在render方法之前执行，当然初始化render时不执行该方法。

需要特别注意的是，在这个函数里面，你就不能使用this.setState来修改状态。

这个函数调用之后，就会把nextProps和nextState分别设置到this.props和this.state中。紧接着这个函数，就会调用render()来更新界面。

**componentDidUpdate**：
组件更新结束之后执行，在初始化render时不执行。

**componentWillReceiveProps**：
当props发生变化时执行，初始化render时不执行。(state变化时，不会触发)
在这个回调函数里面，你可以根据属性的变化，通过调用this.setState()来更新你的组件状态，旧的属性还是可以通过this.props来获取,这里调用更新状态是安全的，并不会触发额外的render调用(即不会引发多次重复的render调用)。

---

### 20180816
1.react，页面回流问题？什么是页面回流：?
解决方法：回流一定会重绘，但重绘不一定回流(回流之后会进行重绘, 重绘跟回流没有直接关系)。
回流=重排，即从新布局。

#### 【以下为摘抄】 ####
回流与重绘

* 1. 当render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流(reflow)。每个页面至少需要一次回流，就是在页面第一次加载的时候。在回流的时候，浏览器会使渲染树中受到影响的部分失效，并重新构造这部分渲染树，完成回流后，浏览器会重新绘制受影响的部分到屏幕中，该过程成为重绘。

* 2. 当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color。则就叫称为重绘。

#### 回流何时发生 ####：
当页面布局和几何属性改变时就需要回流。下述情况会发生浏览器回流：
* 1、添加或者删除可见的DOM元素；
* 2、元素位置改变；
* 3、元素尺寸改变——边距、填充、边框、宽度和高度
* 4、内容改变——比如文本改变或者图片大小改变而引起的计算值宽度和高度改变；
* 5、页面渲染初始化；
* 6、浏览器窗口尺寸改变——resize事件发生时；

#### 如何减少回流、重绘 ####
减少回流、重绘其实就是需要减少对render tree的操作（合并多次多DOM和样式的修改），并减少对一些style信息的请求，尽量利用好浏览器的优化策略。

参考链接：[css88](http://www.css88.com/archives/4996)

------
### 20180820
1. web，怎样让图片等比例缩小，从而防止显示失真？ 比如做头像的图片，头像是个正方形且设置border-redius变成了原形，如果上传的图片是矩形呢？
答：图片组件构成如下：
```javascript
<div><img src='/images/img01.jpg'/></div>
```
 情况分2种:
 * 1为：图片不限制大小，则图片本身多大，就把img和外层div撑多大。
 * 2为：如果设置了宽高，比如 width: 50px, height: 50px,  则div的样式为：{width:'50px', height:'50px'，overflow：hidden}, 而此时为了设置的图片被按原图或等比例显示在组件上，则可设置img元素样式为:{max-width: 50px}  注：如果组件设置的宽度>高度，就设置max-width，否则就设置max-height，此时如果设置图片尺寸比50x50小，则会按原图显示，否则会根据图片本身比例进行缩放.

---

### 20180823
1. web页面使用onMouseEnter与onMouseLeave有什么区别？ 都是鼠标离开时会触发的事件。
答：其区别为：
假设事件绑定在元素A上，A有子元素B。
## mouseout ##: 不论鼠标指针离开被选元素还是任何子元素，都会触发 mouseout 事件。
## mouseleave ##: 只有在鼠标指针离开被选元素时，才会触发 mouseleave 事件。即：鼠标只要在A元素或其子元素B上，都不会触发。在B上的leave不会冒泡到A上。

---

### 20180826
* 1.[经验]本地开发，如果从github拉取源代码并可以上传修改内容？
答：
*1.在github网站创建自己的github帐号；
* 2.在github上使用自己创建的帐号创建一个项目，从而得到该项目的'clone and download'链接，这里链接用‘ssh’方式的；
* 3. 本地安装git客户端工具(github官方有提供之类工具下载)，设置好git config中的user.name和user.email，同时在本地使用git生成一个ssh key，相关指令类似-》 设置：git config --global user.name "github登录用户名"，git config --global user.email "github注册时用的邮箱"，生成key：ssh-keygen -t rsa -C "github注册时用的邮箱"；
* 4. 找到生成的ssh-key的文件id_rsa.pub，复制里面内容设置到github网站的‘setting-SSH and GPG keys’页面，
设置好SSH keys，之后就可以使用之前创建项目链接，在本地git clone下来了。

---

### 20190515
1. 问题描述：给定一张图片，让图片显示为圆形(跟一般头像的圆形效果一样)，且图片宽高为34*34px，同时图片要保持等比例，不能因为拉伸而变形。
   答：外层套一个div，div内一个img：
   ```
   <div><img src='xxxx.png'/></div>;
   ```
   
   关键: div样式让内部img居中; img样式：`width: 100%`,  height不设置.
   ```
        div {
            display: flex;
            width: 34px;
            height: 34px;
            border-radius: 50%;
            justify-content: center;
            align-items: center;
            // border: 1px solid #FFFFFF;
            border-radius: 50%; //圆形
            flex-shrink: 0;
            overflow: hidden;
            img {
                width: 100%;
            }
        }
    ```
  
  这样最终图片等比例显示为圆形，且宽高都不超过34px.
   
---
   
   ### 20190705
   1. web页面元素的class属性(eg: calss='class1 class2 class3')，其中用空格分开的多个class其摆放顺序与其声明顺序的关系是怎么样的？
      答：结论如下：
      * 1、如果使用多个class去描述元素，css样式的优先级和使用时候的位置无关，只与声明的位置有关，比如class="a1 a2"和class="a2 a1"是等价的。
      * 2、css样式的优先级是在加载css文件的时候就确定下来的，而且是后来居上（后声明的样式优先级高）。
      
      参考链接如下：
      * [class(类)声明顺序](https://blog.csdn.net/qq_40415721/article/details/81410616)
      * [HTML中设置多个class属性的优先级](https://blog.csdn.net/u011320646/article/details/18152857) 
    
   2. react框架开发的component，其key的作用及指定的时机？
      答：key的作用：用于唯一标示一个component，key变了，component会销毁重建。
          key的指定时机：在元素元素##第一次创建##时指定才有效，其他时机如高阶包装等都无效。创建的地方一般为:
        ```
        react.createElement(component1, {key: id1, ...})
        ```
          or
        ```
        return <div key={id1} ...></div>
        ```
   
---

### 20190905
1. css3 pointer-events样式的作用？
答：阻止用户的点击动作产生任何效果；阻止缺省鼠标指针的显示；阻止CSS里的 hover 和 active 状态的变化触发事件；阻止JavaScript点击动作触发的事件。
    更重要的是：元素设置了样式为`style: {pointer-events: none}`，则click/hover该元素，就会穿透过去。
    [参考连接1](https://www.imooc.com/article/48022)
    [参考连接2](https://blog.csdn.net/qq_42606051/article/details/81808133)

---


   
