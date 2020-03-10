## flex布局
### __flex__ 布局是Flex 是 Flexible Box 的缩写，表示‘弹性布局’，用来为盒状模型提供最大的灵活性。任何一个容器都可以是定位flex布局
```css
.box{
    display:flex;
    display: -webkit-flex; /* Webkit 内核的浏览器，必须加上-webkit前缀。 */
}
``````
### 容器的属性设置
* __flex-direction__; 设置主轴的方向 可取的值：
>* __row;__ (默认值) 水平方向；从左向右
>* __row-reverse;__ 水平方向 从右向左
>* __column;__ 垂直方向 从上到下
>* __column-reverse;__ 垂直方向 从下到上

* __flex-wrap;__ 设置换行 取值：
>* __nowrap__ (默认) 不换行
>* __wrap__ 换行  第一行在上方
>* __wrap-reverse__ 换行 第一行在下方
* __flex-flow;__ 是flex-direction属性和flex-wrap属性的简写形式
* __justify-content;__ 设置项目在主轴的对齐方式
>* __flex-start;__ 开始位置
>* __flex-end;__ 结束位置
>* __center;__ 居中
>* __space-between;__ 两端对齐，项目之间的间隔都相等
>* __space-around;__ 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

* __align-items;__ 设置项目在交叉轴的对齐方式 取值：
>* __flex-start;__
>* __flex-end;__
>* __center;__
>* __baseline;__
>* __stretch;__

* __align-content;__ 设置多行排列时的对齐方式 取值：
>* __flex-start;__
>* __flex-end;__
>* __center;__
>* __space-between;__
>* __space-around;__
>* __stretch;__ (默认) 轴线占满整个交叉轴
### 项目的属性设置
* __order;__ 设置项目排列顺序; 数值越小越靠前
* __flex-grow;__ 设置项目的放大比例 默认值为0;表示即使存在剩余空间也不放大;如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。
* __flex-shrink;__ 设置项目缩小比例 默认为1，表示空间不足时，项目自动缩小 与flex-grow 类似
* __flex-basis;__ 设置了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
* __flex;__ 是flex-grow, flex-shrink 和 flex-basis的简写
* __align-self;__ 允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性