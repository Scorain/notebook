
## css���ض���ʼ�



#### �ṹ�벼��ƪ

###### ����1���������Ӧ�ڲ�Ԫ��

ʹfigureԪ�صĿ������Ӧimg�Ŀ�Ȳ�����
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

���˼·���£�
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

>**min-content**�ؼ��ֿɲο�[������ĸ��˲���](http://www.zhangxinxu.com/wordpress/2016/05/css3-width-max-contnet-min-content-fit-content/)

###### ����2����ȷ���Ʊ���п�

```
table {
	table-layout: fixed;
	width: 100%;
}
```

>**table-layout**�ؼ��ֿɲο�[CSS TRICKS](https://css-tricks.com/fixing-tables-long-strings/)

###### ����3�������ֵ�Ԫ�ص�������������ʽ

���б�����4����ʱ��ѡ�������
```
li:first-child:nth-last-child(4),
li:first-child:nth-last-child(4) ~ li {
}
```

���б��е���������4ʱ��ѡ�������
```
li:first-child:nth-last-child(n+4),
li:first-child:nth-last-child(n+4) ~ li {
}
```

���б��е���������2С��6ʱ��ѡ�������
```
li:first-child:nth-last-child(n+2):nth-last-child(-n+6),
li:first-child:nth-last-child(n+2):nth-last-child(-n+6) ~ li {
}
```

>**nth-child**��**nth-of-type**�ؼ��ֿɲο�[������ĸ��˲���](http://www.zhangxinxu.com/wordpress/2011/06/css3%E9%80%89%E6%8B%A9%E5%99%A8nth-child%E5%92%8Cnth-of-type%E4%B9%8B%E9%97%B4%E7%9A%84%E5%B7%AE%E5%BC%82/)

###### ����4�������ı��������������

ʵ��һ��������ȳ��������ӿڣ����ݿ��Ϊ900px�Ҿ��е�ҳ�Ų���
```
<footer></footer>
```

��ʽ�ļ����£�
```
footer {
	padding: 1em;
	padding: 1em calc(50% - 450px);
	background: #333;
}
```

>**calc**�ؼ��ֿɲο�[Airen�Ĳ���](https://www.w3cplus.com/css3/how-to-use-css3-calc-function.html)

###### ����5����ֱ����

���ھ��Զ�λ�Ľ������

```
main {
	position:absolute;
	top:50%;
	left:50%;
	margin-top: -height/2;
	margin-left: -width/2;
}
```
���ַ��������ڹ̶���ߵ�Ԫ��

���ھ��Զ�λ����εĽ������

```
main {
	position:absolute;
	top:50%;
	left:50%;
	transform:translate(-50%,-50%);
}
```
���ַ�����Ԫ�صĿ��û������

�����ӿڵ�λ�Ľ������

```
main {
	margin: 50vh auto 0;
	transform: translateY(-50%);
}
```
���ַ���ֻ�������ӿھ��еĳ���

����Flexbox�Ľ������
```
.container {
	display:flex;
	justify-content:center;
	align-items:center;
}
```
���ַ���Ϊ���е���ѽ��˼·

>**vh**�ؼ��ֿɲο�[���S�Ĳ���](https://www.w3cplus.com/css/simplify-your-stylesheets-with-the-magical-css-viewport-units.html);
**Flexbox**�ؼ��ֿɲο�[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes);
 
###### ����6�������ײ���ҳ��

HTML�ṹ���£�
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

�̶��߶ȵĽ��˼·
```
main {
	min-height: calc(100vh - headerHeight - footerHeight);
	box-sizing: border-box;
}
```

Flexbox�Ľ��˼·
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


***

#### ��״ƪ

###### ����1������Ӧ��Բ

��Բ
```
div {
	border-radius: 50%;
}
```

����Բ
```
div {
	border-top-left-radius: 50% 100%;
	border-top-right-radius: 50% 100%;
}
```

�ķ�֮һ��Բ
```
div {
	border-top-left-radius: 100%;
}
```

>**border-radius**�ؼ��ֿɲο�[MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius)

###### ����2��ƽ���ı���

Ƕ��Ԫ�ط���

```
<div>
    <p>click me</p>
</div>
```

```
div {
    width:50px;
	height:20px;
	background-color:red;
    transform: skew(45deg);
}
div>p {
    transform: skew(-45deg);
}
```

ΪԪ�ط���
```
<div></div>
```

```
div {
    width:50px;
	height:20px;
	position:relative;
}
div::before {
	content:"";
	position:absolute;
	top:0; left:0; bottom:0; right:0;
	background-color:red;
    transform: skew(-45deg);
}
```

###### ����3������ͼƬ

���ڱ��εķ���

```
<div class="picture">
	<img src="test.jpg" />
</div>
```

```
.picture {
	width:400px;
	transform:rotate(45deg);
	overflow:hidden;
}
.picture > img {
	max-width:100%;
	transform:rotate(-45deg) scale(1.42);
}
```

���ڲ���·���ķ���

```
div {
	clip-path:polygon(50% 0,100% 50%,50% 100%,0 50%);
}
```

