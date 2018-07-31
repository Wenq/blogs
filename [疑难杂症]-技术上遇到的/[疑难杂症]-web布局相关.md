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
