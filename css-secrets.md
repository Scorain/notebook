
## css揭秘读书笔记



#### 结构与布局篇

###### 案例1：宽度自适应内部元素

使figure元素的宽度自适应img的宽度并居中
```
<p>some text ...</p>
<figure>
	<img src="test.jpg" />
	<figcaption>
		the great sir adam catlace was named after countess ...
	</figcaption>
</figure>
<p>more text ...</p>
```

解决思路如下：
```
figure {
	max-width: 300px;
	max-width: min-content;
	margin: auto;
}
figure > img {
	max-width: inherit;
}
```

>**min-content**关键字可参考[张鑫旭的个人博客](http://www.zhangxinxu.com/wordpress/2016/05/css3-width-max-contnet-min-content-fit-content/)

###### 案例2：精确控制表格列宽

```
table {
	table-layout: fixed;
	width: 100%;
}
```

>**table-layout**关键字可参考[CSS TRICKS](https://css-tricks.com/fixing-tables-long-strings/)

###### 案例3：根据兄弟元素的数量来设置样式

当列表中有4个项时，选中所有项：
```
li:first-child:nth-last-child(4),
li:first-child:nth-last-child(4) ~ li {
}
```

当列表中的项数大于4时，选中所有项：
```
li:first-child:nth-last-child(n+4),
li:first-child:nth-last-child(n+4) ~ li {
}
```

当列表中的项数大于2小于6时，选中所有项：
```
li:first-child:nth-last-child(n+2):nth-last-child(-n+6),
li:first-child:nth-last-child(n+2):nth-last-child(-n+6) ~ li {
}
```

>**nth-child**与**nth-of-type**关键字可参考[张鑫旭的个人博客](http://www.zhangxinxu.com/wordpress/2011/06/css3%E9%80%89%E6%8B%A9%E5%99%A8nth-child%E5%92%8Cnth-of-type%E4%B9%8B%E9%97%B4%E7%9A%84%E5%B7%AE%E5%BC%82/)

###### 案例4：满幅的背景、定宽的内容

实现一个背景宽度充满整个视口，内容宽度为900px且居中的页脚布局
```
<footer></footer>
```

样式文件如下：
```
footer {
	padding: 1em;
	padding: 1em calc(50% - 450px);
	background: #333;
}
```

>**calc**关键字可参考[Airen的博客](https://www.w3cplus.com/css3/how-to-use-css3-calc-function.html)

###### 案例5：垂直居中

基于绝对定位的解决方案

```
main {
	position:absolute;
	top:50%;
	left:50%;
	margin-top: -height/2;
	margin-left: -width/2;
}
```
这种方案适用于固定宽高的元素

基于绝对定位与变形的解决方案

```
main {
	position:absolute;
	top:50%;
	left:50%;
	transform:translate(-50%,-50%);
}
```
这种方案对元素的宽高没有限制

基于视口单位的解决方案

```
main {
	margin: 50vh auto 0;
	transform: translateY(-50%);
}
```
这种方案只适用于视口居中的场景

基于Flexbox的解决方案
```
.container {
	display:flex;
	justify-content:center;
	align-items:center;
}
```
这种方案为居中的最佳解决思路

>**vh**关键字可参考[晓婼的博客](https://www.w3cplus.com/css/simplify-your-stylesheets-with-the-magical-css-viewport-units.html);
**Flexbox**关键字可参考[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes);
 
###### 案例6：紧贴底部的页脚

HTML结构如下：
```
<header>
	<h1>Site name</h1>
</header>
<main>
	<p>A long text ... </p>
</main>
<footer>
	<p>&copy 2017 No rights reserved.</p>
</footer>
```

固定高度的解决思路
```
main {
	min-height: calc(100vh - headerHeight - footerHeight);
	box-sizing: border-box;
}
```

Flexbox的解决思路
```
body {
	display: flex;
	flex-flow: column;
	min-height:100vh;
}
main {
	flex: 1;
}
```
