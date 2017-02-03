
## css揭秘读书笔记

#### 第一章 引言

#### 第二章 背景与边框

###### 1.半透明边框

涉及属性：
*background-clip

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>半透明边框</title>
		<style>
			.example{
				width:100px;
				height:100px;
			}
			.shadow{
				border:10px solid rgba(255,255,255,.5);
				background:red;
				background-clip:padding-box;
			}
		</style>
	</head>
	<body>
		<div class="example shadow"></div>
	</body>
</html>
```

###### 2.多重边框

>方案1：

涉及属性：
*box-shadow

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>多重边框</title>
		<style>
			*{margin:0;padding:0;}
			.example{
				width:100px;
				height:100px;
				margin:20px;
				background:red;
			}
			.multi-border{
				box-shadow:0 0 0 5px green,
					0 0 0 15px blue;
			}
		</style>
	</head>
	<body>
		<div class="example multi-border"></div>
	</body>
</html>
```

>方案2：

涉及属性：
*outline

```
.multi-border{
	border:5px solid green;
	outline:10px solid blue;
}
```