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