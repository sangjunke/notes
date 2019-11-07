```css
/* 设置input placeholder 字体颜色 */
input::-webkit-input-placeholder { /* WebKit, Blink, Edge */
    color:    #569FCA !important;
 }
 input::-moz-placeholder { /* Mozilla Firefox 4 to 18 */
    color:    #569FCA !important;
 }
 input:-moz-placeholder { /* Mozilla Firefox 19+ */
    color:    #569FCA !important;
 }
 input:-ms-input-placeholder { /* Internet Explorer 10-11 */
    color:    #569FCA !important;
 }
 /* 超出显示省略号 单行 */
 {  

     white-space: nowrap;
    -webkit-line-clamp: 1;
    text-overflow: ellipsis;
    overflow: hidden;
 }
 /* a 伪类 */
    (1)a:link	未访问前的超链接
	(2)a:visited 访问过后
	(3)a:hover	鼠标移到链接上
	(4)a:link	鼠标点击未释放
	(5)设置伪类的顺序：a:link - a:visited - a:hover - a:active
/* 清楚浮动 */
.clear:after{ display:block; content:''; clear:both;height: 0;}
.clear{ zoom:1;}
```