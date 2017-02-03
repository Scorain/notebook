
## css���ض���ʼ�

#### ��һ�� ����

#### �ڶ��� ������߿�

###### 1.��͸���߿�

�漰���ԣ�
*background-clip

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>��͸���߿�</title>
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

###### 2.���ر߿�

>����1��

�漰���ԣ�
*box-shadow

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>���ر߿�</title>
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

>����2��

�漰���ԣ�
*outline

```
.multi-border{
	border:5px solid green;
	outline:10px solid blue;
}
```