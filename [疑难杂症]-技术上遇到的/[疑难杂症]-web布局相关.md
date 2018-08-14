0728:
关键词： 拖拽 鼠标事件 Drag MouseUp  
问题描述：
        拖拽浏览器中特定元素，触发浏览器的默认拖拽行为，从而导致开始时按下鼠标触发了mouseDown，之后移动鼠标触发了drag（浏览器默认），但drag触发后，在drag过程中松开鼠标，浏览器无法触发mouseUp。直接导致在mouseDown-mouseUp过程中的逻辑无法结束。
解决方法：

20180730:
1. 父容器的display:flex,position:abosolute,子元素positiong:abosolute时会怎样？

答：子元素会相对父容器进行布局，效果跟父容器是position:relative，子元素是position:abosolute的效果一样。 在chrome浏览器中，父容器的flex还会影响子元素,如果子元素只设置了right/left，没有设置top/bottom的话。

20180731:
1.父容器使用了transform，在父容器下的子元素(比如弹窗)如果使用了fixed布局，会导致子元素显示位置混乱。

答：结果造成了fixed布局相对transform变成了abosolute布局效果。不再相对页面了。

20180801:
1.pre页面元素，支持自动换行且支持内容中带的换行符‘\r\n’.

20180802:
1. react中元素使用props：dangerouslySetInnerHTML，引发xss(跨站脚本攻击)安全性问题。
解决方案：对输出的内容做xss安全性过滤，防止执行了脚本。

dangerouslySetInnerHTML使用方法：<div className={className} dangerouslySetInnerHTML={{__html: html}} ></div>
//这里要对'html'内容过滤，才能防止xss攻击
作用：保留原始html标签，比如换行标示'<br/>'符等。

注：react.js 避免使用 dangerouslySetInnerHTML,可以在大部分情况下避免 XSS 攻击。

20180804:
1. 设置了父容器透明度，再去设置该容器的子元素透明度，导致子元素透明效果与父容器透明叠加。即子元素透明被父容器透明度影响。
问题重现：父容器透明度设置：opacity：0.7; 子元素透明度设置：0.9； 结果子元素透明度是0.7x0.9的效果。（这有疑惑？是效果重叠还是子继承了父的透明度）
解决办法：设置父容器的透明度采用：rgba(x,x,x,0.7)方式，而不是直接设置opactiy属性。

20180807:
1. web页面双击，会自动选中文本，图片等html元素，元素上会自动附加一层背景色。但有时不想产生这种效果，怎么办呢？
答：设置元素的css样式‘user-select’为‘none’即可，这种方法比较通用，对各类浏览器兼容性较好。
其他作用：禁止用户选中页面上内容的效果等。
参考帖子：http://www.w3cui.com/?p=141

20180810:
1.client往server发送请求，怎样自动带上cookie？
2.怎样支持跨域访问？？

答：1.前端进行数据请求有：普通的ajax(json)请求，jsop跨域请求，cors跨域请求，fetch请求...PC端这些请求方式中，普通的ajax(json)请求和jsop跨域请求是默认携带cookie的，而cors跨域请求和fetch请求默认是不携带cookie的。因此，当我们的请求需要携带cookie时，我们就要对cors跨域请求和fetch请求这两中请求方式进行特殊配置处理。
      针对ajax不支持自带cookie的，需要对ajax进行配置：credentials: 'include'。
      2. 两步配置：(1).配置client端，支持跨域访问； (2).配置服务端，支持跨域访问。
fetch请求方式：
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
我们要在请求头中添加上这个配置：
credentials: 'include'
cors跨域请求方式：
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
我们要在请求头中添加上这个配置：
　　xhrFields: {
        withCredentials: true
    },
    crossDomain: true
配上对应的特殊配置后，cookie就会被带上去请求数据了
以上参考链接：https://www.cnblogs.com/zhuotiabo/p/6230521.html

其他：同源不跨域要求：协议，域名，端口一致。 eg：http://www.example.com:81
跨域的目的：1.共享cookie；2.跨域获取dom; 3.读写其他窗口的LocalStorage; 
ajax实现跨域几种方法：

（1）JSONP （2）WebSocket （3）CORS

以上参考链接：https://blog.csdn.net/u013084331/article/details/51114288

20180814:
web平台，前端怎样支持二开，在不影响本身标准产品的前提下渲染客户自己开发的组件？
答：方案一：在标准产品中开发一个自定义组件，允许配置需要动态加载的js，css文件。之后在渲染这个自定义组件时，动态加载配置的js，css文件并把一个dom节点塞进去，让动态加载的js以此dom节点进行组件渲染，想要什么就渲染什么并可自己控制样式，同时可以暴露一些通信api进去共调用。
    方案二：？