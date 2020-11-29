# BootStrap

# 1.主要内容

# 2.BootStrap的安装和使⽤

## 2.1. BootStrap 介绍

​		官⽹：http://getbootstrap.com/
​		中⽂⽹：http://www.bootcss.com/
​		Bootstrap 是⼀套现成的 CSS 样式集合（做得还是很友好的）。是两个推特的员⼯⼲出来的。
​		Bootstrap 是最受欢迎的 HTML、CSS 和 JS 框架，⽤于开发响应式布局、移动设备优先的 WEB 项⽬。

## 2.2. BootStrap 特点

1. 简洁、直观、强悍的前端开发框架，html、css、javascript ⼯具集，让 web 开发更速、简单。
2. 基于html5、css3的bootstrap，具有⼤量的诱⼈特性：友好的学习曲线，卓越的兼容性，响应式设计，12列格⽹，样式向导⽂档。
3. ⾃定义 JQuery 插件，完整的类库，bootstrap3 基于Less，bootstrap4 基于 Sass 的 CSS 预处理技术
4. Bootstrap 响应式布局设计,让⼀个⽹站可以兼容不同分辨率的设备。Bootstrap 响应式布局设计，给⽤户提供更好的视觉使⽤体验。
5. 丰富的组件

## 2.3. 下载与使⽤

1. 下载：http://v3.bootcss.com/getting-started/
2. 下载完成后
拷⻉ dist/css 中的 bootstrap.min.css 到项⽬ css 中
拷⻉ dist/js 中的 bootstrap.min.js 到项⽬的 js 中
3. 下载 jquery.js
http://jquery.com/
4. 在 html 中模板为:

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<!--使⽤X-UA-Compatible来设置IE浏览器兼容模式 最新的渲染模式-->
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<!--
			viewport表示⽤户是否可以缩放⻚⾯；
			width指定视区的逻辑宽度；
			device-width指示视区宽度应为设备的屏幕宽度；
			initial-scale指令⽤于设置Web⻚⾯的初始缩放⽐例
			initial-scale=1则将显示未经缩放的Web⽂档
		-->
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>Bootstrap的HTML标准模板</title>
		<!-- 载⼊Bootstrap 的css -->
		<link href="bootstrap/dist/css/bootstrap.min.css" rel="stylesheet">
	</head>
	<body>
		<h1>Hello, world!</h1>
		<!-- 如果要使⽤Bootstrap的js插件，必须先调⼊jQuery -->
		<script src="js/jquery-3.5.1.js"></script>
		<!-- 包括所有bootstrap的js插件或者可以根据需要使⽤的js插件调⽤　-->
		<script src="bootstrap/dist/js/bootstrap.min.js"></script>
	</body>
</html
```

注意：
		<font color= "red">⽬前暂时不使⽤ jquery 的插件 可以不⽤引⼊ js ⽂件,这⾥是为了保证模板的完整性。</font>
说明：
		viewport 标记⽤于指定⽤户是否可以缩放Web⻚⾯
		width 和 height 指令分别指定视区的逻辑宽度和⾼度。他们的值要么是以像素为单位的数字，要么是⼀个特殊的标记符号。
		width 指令使⽤ device-width 标记可以指示视区宽度应为设备的屏幕宽度。
		height 指令使⽤ device-height 标记指示视区⾼度为设备的屏幕⾼度。
		initial-scale 指令⽤于设置Web⻚⾯的初始缩放⽐例。默认的初始缩放⽐例值因智能⼿机浏览器的不同⽽有所差异。通常情况下设备会在浏览器中呈现出整个Web⻚⾯，设为1.0则将显示未经缩放的Web⽂档.

# 3.布局容器和栅格⽹格系统

## 3.1布局容器

1、.container 类⽤于固定宽度并⽀持响应式布局的容器。

```html
<div class="container">
...
</div>
```

2、.container-fluid类⽤于100% 宽度，占据全部视⼝（viewport）的容器。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>布局容器</title>
		<link rel="stylesheet" type="text/css" href="bootstrap/dist/css/bootstrap.min.css"/>
	</head>
	<body>
		<!-- 
			1、.container 类⽤于固定宽度并⽀持响应式布局的容器。
			2、.container-fluid类⽤于100% 宽度，占据全部视⼝（viewport）的容器。
		 -->
		 <div class="container" style="height: 500px; background-color: #269ABC;">		 </div>
		 <!-- <div class="container-fluid" style="height: 800px; background-color: #269ABC;">		 </div> -->
	</body>
</html>

```

## 3.2. 栅格网格系统

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>栅格网格系统</title>
		<link rel="stylesheet" type="text/css" href="bootstrap/dist/css/bootstrap.min.css"/>
		
	</head>
	<body>
		<!-- 
			栅格网格系统
				
		 -->
		 <div class="container">
			 <div class="row">
				<div class="col-md-1" style="background-color: #006699;">1格</div>
				<div class="col-md-2" style="background-color: blue;">2格</div>
				<div class="col-md-4" style="background-color: red;">4格</div>
				<div class="col-md-5" style="background-color: pink;">5格</div>
				
			</div>
			<hr >
			 <div class="row">
			 	<div class="col-md-1" style="background-color: #006699;">1格</div>
			 	<div class="col-md-2" style="background-color: blue;">2格</div>
			 	<div class="col-md-4" style="background-color: red;">4格</div>
			 	<div class="col-md-3 col-md-offset-2" style="background-color: pink;">3格</div>
			 </div>
			 <hr >
			  <div class="row">
			  	<div class="col-md-1 col-md-push-2" style="background-color: #006699;">1格</div>
			  	<div class="col-md-2" style="background-color: blue;">2格</div>
			  	<div class="col-md-4" style="background-color: red;">4格</div>
			  	<div class="col-md-3 " style="background-color: pink;">3格</div>
			  </div>		  
		 </div>
		 <br>
		 <br>
		 
		<div class="row">
		  <div class="row">
			<div class="col-md-1" style="background-color: #000099;"></div>	  
		  </div>
		</div>
	</body>
</html>

```

