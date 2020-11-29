# 1、相对定位 position: relative;

```css
	<style type="text/css">
		.box1{
			width: 200px;
			height: 200px;
			background-color: red;
			/*如果对当前元素仅仅设置相对定位，那么与标准流下的盒子没有什么区别*/
			position: relative;
			/*设置相对定位 我们就可以使用四个方向的属性  top left right bottom

			相对定位：相对于自己原来的本身定位 top:20px; 那么盒子相对于原来的位置向下移动。相对定位仅仅的微调我们元素的位置
			*/
			top: 20px;
			left: 30px;
		}
	</style>
</head>
<body>
	 <div class="box1"></div>
</body>
```

## 特性

```
		div{
			width:200px;
			height: 200px;
		}
		
		.box1{
			background-color: red;
		}
		.box2{
			background-color: green;
			position: relative;
			top: 50px;
			left: 100px;
		}
		.box3{
			background-color: blue;
		}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203161031563.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)

```
蓝色盒子并没有挤上去，绿色盒子移动之后没有脱离标准流，留下了空白，还有原位置的空白，产生了压盖效果，但是不要这么用。
```

## 用途

-  1.微调元素位置
-  2.做绝对定位的参考（父相子绝）

```
<style type="text/css">
		*{
			padding: 0;
			margin: 0;
		}
		div{
			margin: 100px;
		}
		.user{
			font-size: 25px;
		}
		.btn{
			position: relative;
			top: 3px;
			left: 5px;
		}

	</style>
</head>
<body>
	<!-- 微调我们元素位置-->

	<div>

		<input type="text" name="username" class="user">
		<input type="button" name="" value="点我" class="btn">
	</div>

```



# 2、绝对定位 position: absolute;

-  1.脱标，做遮盖效果，提升层级
-  2.设置绝对定位之后，不区分行内元素和块级元素，都能设置宽高。

```
*{
			padding: 0;
			margin: 0;
		}
		div{
			width: 200px;
			height: 200px;

		}
		.box1{
			background-color: red;

			position: absolute;
		}
		.box2{
			width: 250px ;
			background-color: green;

		}
		.box3{
			background-color: blue;
		}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203170317715.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)

```
span{
			width: 100px;
			height: 100px;
			background-color: pink;
			
			position: absolute;
		}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203170808396.jpg)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203170815441.jpg)
效果与diapaly，浮动比较：

```
span{
			width: 100px;
			height: 100px;
			background-color: pink;
			
		}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2019020317102376.jpg)

```
span{
			width: 100px;
			height: 100px;
			background-color: pink;
			display: block;
		}
123456
span{
			width: 100px;
			height: 100px;
			background-color: pink;
			float: left;
		}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203171048439.jpg)

## 绝对定位参考点

单独盒子绝对定位参考点：

-  1.top属性描述, 是以页面的左上角，并不是body，而是页面html左上角为参考点来调整位置。滚动条滚动时，距离页面左上角位置不变。
-  2.使用bottom属性描述,是以首屏页面左下角为参考点来调整位置。

```
<div class="box1"></div>
	<div class="box2"></div>
12
body{
			width: 100%;
			height: 2000px;
			border: 10px solid green;
		}

		.box1{
			width: 200px;
			height: 200px;
			background-color: red;
			position: absolute;
			top: 100px;
		}
		
		以绿色盒子作为参考说明不是以body为参考点，而是页面
		.box2{
			width: 200px;
			height: 200px;
			background-color:green;
			margin-left: 100px;
			margin-top: 100px;
		}
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203181241962.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)
top属性描述，滚动条滚动，与页面位置不变，跟浏览器位置没关系：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203181304825.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)
bottom属性描述时，以首屏页面左下角为参考点
如果浏览器不动，滚动条动的时候，红色盒子跟随页面动，红绿盒子间距不变。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203192521777.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)
页面顶端与浏览器顶端重合时，移动浏览器底部，红色盒子距离浏览器底部距离不变。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203192533958.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)

父辈元素设置了相对定位，则子元素绝对定位以父辈元素为参考点。

-  父相子绝，父绝子绝，父固子绝,都是以父辈元素为参考点。父绝子绝，因为绝对定位脱离标准流，影响页面的布局。父相子绝是常用的布局方案。（如果父辈有边框，则以内沿边界为起点）
-  绝对定位的盒子无视父辈的padding。

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title></title>
	<style type="text/css">
		*{
			padding: 0;
			margin: 0;
		}
		.box{
			width: 300px;
			height: 300px;
			border: 5px solid red;
			margin: 100px;
			/*父盒子设置相对定位*/
			position: relative;
			padding: 50px;
		}
		.box2{
			width: 300px;
			height: 300px;
			background-color: green;
			position: relative;
			
		}

		.box p{
			width: 100px;
			height: 100px;
			background-color: pink;
			/*子元素设置了绝对定位*/
			position: absolute;
			top: 0;
			left: 0;
		}

		

	</style>
</head>
<body>
	<div class="box">

		<div class="box2">
			<p></p>
		</div>
	</div>
	
</body>
</html>
123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203195139158.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)
上一层没有再往上找：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203195212733.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)

## 绝对定位水平居中

-  设置绝对定位之后，margin:0 auto;不起任何作用
-  设置子元素绝对定位，然后left:50%; margin-left等于元素宽度的一半

```
	<style type="text/css">
		*{
			padding: 0;
			margin: 0;
		}
		.box{
			width: 100%;
			height: 69px;
			background: #000;
		}
		.box .c{
			width: 960px;
			height: 69px;
			background-color: pink;
			/*margin: 0 auto;*/
			position: absolute;
		
			left: 50%;
			margin-left: -480px;

			}


	</style>
</head>
<body>
	<div class="box">
		<div class="c"></div>
	</div>

</body>
</html>
1234567891011121314151617181920212223242526272829303132
```

# 3、固定定位

-  1.脱标
-  2.提升层级
-  3.固定不变

```
		*{
			padding: 0;
			margin: 0;
		}
		p{
			width: 100px;
			height: 100px;
			background-color: red;
			/*固定定位：固定当前的元素不会随着页面滚动而滚动，
			特性：1.脱标 2.提升层级 3.固定不变 不会随页面滚动而滚动

			参考点：设置固定定位，用top描述。那么是以浏览器的左上角为参考点
			如果用bottom描述，那么是以浏览器的左下角为参考点

			作用： 1.返回顶部栏 2.固定导航栏 3.小广告

			*/
			position: fixed;
			top: 30px;
			left: 40px;
		}
	</style>
</head>
<body>

	<div>
		<p></p>
		<img src="1_light__1024.ico" alt="">
		<img src="1_light__1024.ico" alt="">
		<img src="1_light__1024.ico" alt="">
		<img src="1_light__1024.ico" alt="">
		<img src="1_light__1024.ico" alt="">
		<img src="1_light__1024.ico" alt="">
		<div></div>
		<img src="1_light__1024.ico" alt="">
		<div></div>
		<img src="1_light__1024.ico" alt="">
		<div></div>
		<img src="1_light__1024.ico" alt="">
		<img src="1_light__1024.ico" alt="">
		<div></div>
		<img src="1_light__1024.ico" alt="">
		<div></div>
		<img src="1_light__1024.ico" alt="">

	</div>
</body>
</html>
123456789101112131415161718192021222324252627282930313233343536373839404142434445464748
```

之前：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203204511717.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)
之后脱标：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203204540391.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)
定在屏幕上：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190203204630970.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpZ2h0X18xMDI0,size_16,color_FFFFFF,t_70)

## 参考点

用top描述，以浏览器的左上角为参考点
用bottom描述，以浏览器的左下角为参考点，无论滚动条动还是浏览器底部上下移动，固定定位盒子与底部距离始终不变。

```
	<title>固定导航栏</title>
	<style type="text/css">
		*{
			padding: 0;
			margin: 0;
		}
		ul{
			list-style: none;
		}
		a{
			text-decoration: none;
		}
		body{
			/*给body设置导航栏的高度，来显示下方图片的整个内容*/
			padding-top: 49px;
		}
		.wrap{
			width: 100%;
			height: 49px;
			background-color: #000;
			
			/*设置固定定位之后，一定一定要加top属性和left属性，
			固定定位脱标，填充图片会被遮挡，设置body的padding之后导航栏会随之下移
			固定定位以浏览器为参考，设置top和left之后定在浏览器顶部
			*/
			position: fixed;
			top: 0;
			left: 0;

			
		}
		.wrap .nav{
			width: 960px;
			height: 49px;
			margin: 0 auto;

		}
		.wrap .nav ul li{
			float: left;
			width: 160px;
			height: 49px;
			
			text-align: center;
		}
		.wrap .nav ul li a{
			width: 160px;
			height: 49px;	
			display: block;
			color: #fff;
			/*大小行高一起写*/
			font: 20px/49px "Hanzipen SC";
			background-color: purple;
		}
		.wrap .nav ul li a:hover{
			background-color: red;
			font-size: 22px;
		}

		
	</style>
</head>
<body>
	<div class="wrap">
		<div class="nav">
			<ul>
				<li>
					<a href="#">网页开发</a>
				</li>
				<li>
					<a href="#">网页开发</a>
				</li>
				<li>
					<a href="#">网页开发</a>
				</li>
				<li>
					<a href="#">网页开发</a>
				</li>
				<li>
					<a href="#">网页开发</a>
				</li>
				<li>
					<a href="#">网页开发</a>
				</li>
			</ul>
		</div>
	</div>
```