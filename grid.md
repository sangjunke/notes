## grid布局
### grid布局将容器划分为行和列，产生一个一个的单元格，将项目制定到所需单元格 比flex布局更加强大
### 行和列：与表格类似，n行m列，将会有n*m个单元格，比如5行6列，会有30个单元格
### 网格线 n行会有n+1条网格线 m列会有m+1列网格线
### 容器属性
* __display:grid;__ 设置一个容器采用网格布局;也可设置display:inline-grid;设置行内元素
* __grid-template-columns;__ 划分列 ，设置每一列的列宽 如：__grid-template-columns:100px 50px 30px;__
* __grid-template-rows;__ 划分行 设置每一行的行高 如：__grid-template-rows:100px 50px 30px;__
>* __repeat(n,m)__ 重复值的快速写法 n表示重复的次数，m表示重复的值；比如：__grid-template-rows:repeat(3,100px);__ 生成3行行高为100px的表格
>* __auto-fill__ 关键字;单元格大小固定，但容器大小不确定；设置该属性，可以让每一行每一列尽可能多的容纳单元格 自动填充；比如：__grid-template-rows:repeat(auto-fill,100px);__
>* __fr__ 关键字 (fraction缩写，意为片段)；如果两列的宽度分别为 1fr 2fr，表示后者是前者的两倍；比如：__grid-template-rows:1fr 2fr;__ fr可以结合长度单位使用比如 __grid-template-rows:150px 1fr 2fr;__
>* __minmax(n,m)__ 产生一个长度范围  n表示最小值，m表示最大值
>* auto 关键字 自动
>* 网格线的名称 使用方括号 [c1];比如：__grid-template-rows:[c1 c5] 100px [c2 c7] 100px [c3];__ 网格线可以有一个或者多个名字
* __grid-row-gap;__ 设置行间距
* __grid-column-gap;__ 设置列间距
* __grid-gap__ 是行间距和列间距的缩写
* __grid-template-areas;__ 定义指定区域;如果某些区域不使用 用 __.__代替
```css
grid-template-areas:'header header header'
                    'left center right '
                    'footer . footer';
``````
* __grid-auto-flow__ 设置排列顺序 默认值(row)：先行后列 从左往右
>* __grid-auto-flow:column;__ 先列后行
>* __grid-auto-flow:row dense|column dense;__ 某些项目指定位置之后，剩下的项目怎么放
* __justify-items:start | end | center | stretch;__ 设置单元格内容在水平方向的位置 ;__stretch(默认值)__表示拉伸占满单元格的宽度
>* __align-items__ 设置单元格内容在垂直方向上的内容
>* __place-items__ 是 __justify-items__和__align-items__ 两个属性的 合并简写
* __justify-content:start | end | center | stretch | space-around | space-between | space-evenly;__ 整个内容区域在容器里水平方向的位置;__space-evenly__ 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔；__space-around__    每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
* __align-content:start | end | center | stretch | space-around | space-between | space-evenly;__ 整个内容区域在容器里垂直方向的位置
* __grid-auto-columns|grid-auto-rows__ 属性 当项目指定位置在网格外部时使用，自动创建多于单元格
* __grid-template;__是grid-template-columns、grid-template-rows和grid-template-areas这三个属性的合并简写形式。
* __grid__ 是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow这六个属性的合并简写形式。
### 项目属性
* __grid-column-start;__ 左边框所在的垂直网格线 
* __grid-column-end;__ 右边框所在的垂直网格线
* __grid-row-start;__ 上边框所在的水平网格线
* __grid-row-end;__ 下边框所在的水平网格线
>* __grid-column-start;__,__grid-column-end;__,__grid-row-start;__,__grid-row-end;__ 四个属性可以设置项目在容器的位置以及大小 __grid-column-start;__ , __grid-column-end;__ 决定项目在列上的位置；__grid-row-start;__,__grid-row-end;__ 决定项目在行上的位置
>* __grid-column-start;__,__grid-column-end;__,__grid-row-start;__,__grid-row-end;__ 还可以设置网格线的名字；比如 __grid-column-start: header-start;__;
>* __grid-column-start;__,__grid-column-end;__,__grid-row-start;__,__grid-row-end;__ 四个属性的值还可以使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格;
>* 注意:使用这四个属性，如果产生了项目的重叠，则使用z-index属性指定项目的重叠顺序。
* __grid-column;__ 是 __grid-column-start__ 和 __grid-column-end__ 的合并简写形式
* __grid-row;__ 是__grid-row-start__ 和__grid-row-end__ 的合并简写形式
* __grid-area;__ 项目指定在那一区域 
>* __grid-area;__ 还可用作grid-row-start、grid-column-start、grid-row-end、grid-column-end的合并简写形式；比如：__grid-area: 1 / 1 / 3 / 3;__
* __justify-self;__ 设置项目的内容在水平方向上的位置 
* __align-self;__ 设置项目得内容在垂直方向上的位置
* __place-self;__ 是 justify-self和align-self的合并简写形式