# JQuery

## 1、什么是JQuery？

​		为了简化JavaScript的开发，一些JavaScript库就诞生了，JQuery就是其中一种。JavaScript库封装了很多预定义的对象和实用函数。能帮助使用者建立有高难度交互的Wed2.0特性的富客户端页面, 并且兼容各大浏览器。

​		Jquery的理念是<font color=#FF0000 >写的少,做的多</font>，优势如下

- 轻量级
- 强大的选择器
- 出色的 DOM 操作的封装
- 可靠的事件处理机制
- 完善的 Ajax
- 出色的浏览器兼容性
- 链式操作方式

## 2、Jquery对象

​		jQuery 是⼀套兼容多浏览器的 javascript 脚本库.。核⼼理念是写得更少，做得更多，使⽤ jQuery 将极⼤的提⾼编写 javascript 代码的效率，帮助开发者节省了⼤量的⼯作，让写出来的代码更加优雅，更加健壮，"如⻁添翼"。同时⽹络上丰富的 jQuery 插件，也让我们的⼯作变成了"有了 jQuery，⼀切 soeasy。" -- 因为我们已经站在巨⼈的肩膀上了。
​		jQuery 在 2006 年 1 ⽉由美国⼈ John Resig 在纽约的 barcamp 发布，吸引了来⾃世界各地的众多JavaScript ⾼⼿加⼊，由 Dave Methvin 率领团队进⾏开发。如今，jQuery已经成为最流⾏的 javascript 框架，在世界前 10000 个访问最多的⽹站中，有超过 55%在使⽤ jQuery。

### 2.1 Jquery的核心

​		<font color=#FF0000 >$</font>符号在 jQuery 中代表对 jQuery 对象的引⽤， "jQuery"是核⼼对象。通过该对象可以获取jQuery对象，调⽤jQuery提供的⽅法等。只有jQuery对象才能调⽤jQuery提供的⽅法。

### 2.2 Dom对象 与 Jquery包装集对象

​		明确 Dom 对象和 jQuery 包装集的概念， 将极⼤的加快我们的学习速度。原始的 Dom 对象只有 DOM接⼝提供的⽅法和属性，通过js代码获取的对象都是 Dom 对象；⽽通过 jQuery 获取的对象是 jQuery 包装集对象，简称jQuery对象，只有jQuery对象才能使⽤jQuery提供的⽅法。

#### 2.2.1 Dom对象

​	javascript 中获取 Dom 对象，Dom 对象只有有限的属性和⽅法：

```javascript
var div = document.getElementById("testDiv");
var divs = document.getElementsByTagName("div");
```

#### 2.2.2 Jquery包装集对象

​		可以说是 Dom 对象的扩充。在 jQuery 的世界中将所有的对象， ⽆论是⼀个还是⼀组，都封装成⼀个jQuery 包装集，⽐如获取包含⼀个元素的 jQuery 包装集.

```javascript
var jQueryObject = $("#testDiv");
```

#### 2.2.3. Dom对象 转 Jquery对象

​		Dom 对象转为 jQuery 对象，只需要利⽤ $() ⽅法进⾏包装即可

```javascript
var domDiv = document.getElementById('mydiv'); // 获取Dom对象
mydiv = $(domDiv);
```

#### 2.2.4. Jquery对象 转 Dom对象

## 3、Jquery选择器

​		和使⽤ JS 操作Dom⼀样，获取⽂档中的节点对象是很频繁的⼀个操作，在jQuery中提供了简便的⽅式供我们查找|定位元素，称为jQuery选择器，选择器可以说是最考验⼀个⼈ jQuery 功⼒的地⽅，通俗的讲, Selector 选择器就是"⼀个表示特殊语意的字符串"。 只要把选择器字符串传⼊上⾯的⽅法中就能够选择不同的 Dom 对象并且以 jQuery 包装集的形式返回。
​		jQuery 选择器按照功能主要分为"选择"和"过滤"。 并且是配合使⽤的，具体分类如下。基础选择器掌握即可 ,其他⽤到再查阅。

### 3.1. 基础选择器

| 选择器         | 名称                          | 举例                                                 |
| -------------- | ----------------------------- | ---------------------------------------------------- |
| id选择器       | #id                           | $("#testDiv")选择id为testDiv的元素                   |
| 元素名称选择器 | element                       | $("div")选择所有div元素                              |
| 类选择器       | .class                        | $(".blue")选择所有class=blue的元素                   |
| 选择所有元素   | *                             | $("*")选择⻚⾯所有元素                               |
| 组合选择器     | selector1,selector2,selectorN | $("#testDiv,span,.blue")同时选中多个选择器匹配的元素 |

```html
<style type="text/css">
    .blue{
    background: blue;
    }
</style>
<body>
    <div id="mydiv1">id选择器1<span>span中的内容</span></div>
    <div id="mydiv2" class="blue">元素选择器</div>
    <span class="blue">样式选择器</span>
</body>
<script src="js/jquery-3.4.1.js" type="text/javascript" charset="utf-8"></script>
<script type="text/javascript">
    // id选择器
    console.log("======id====");
    var idSelecter = $('#mydiv1');
    console.log(idSelecter.html());
    console.log(idSelecter.text());
    // 元素选择器
    console.log("======name====");
    var nameSe = $('div'); // 有多个div元素
    nameSe.each(function(){
        // this是dom对象，$(this)是jquery对象
        console.log($(this).text());
    });
    // 类选择器，class
    console.log("======class====");
    var classSe = $('.blue'); // 有多个class=blue的元素
    classSe.each(function(){
    	console.log($(this).text());
    });
    // 通⽤选择器：*
    console.log("======所有元素====");
    var all = $("*");
    console.log(all.length);
    // 组合选择器
    console.log("======组合====");
    var unionSe = $('span, .blue,div');
    unionSe.each(function(){
    	console.log($(this).text());
    });
</script>
```

### 3.2. 层次选择器

| 选择器     | 名称                | 举例                                              |
| ---------- | ------------------- | ------------------------------------------------- |
| 后代选择器 | ancestor descendant | $("#parent div")选择id为parent的元素的所有div元素 |
| ⼦代选择器 | parent > child      | $("#parent>div")选择id为parent的直接div⼦元素     |
| 相邻选择器 | prev + next         | $(".blue + img")选择css类为blue的下⼀个img元素    |
| 同辈选择器 | prev ~ sibling      | $(".blue ~ img")选择css类为blue的之后的img元素    |

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>层次选择器</title>
        <script src="js/jquery-3.4.1.js" type="text/javascript"></script>
        <style type="text/css">
            .testColor{
            background: green;
            }
            .gray{
            background: gray;
            }
        </style>
    </head>
    <body>
        <div id="parent">层次择器
            <div id="child" class="testColor">⽗选择器
                <div class="gray">⼦选择器</div>
                <img src="http://www.baidu.com/img/bd_logo1.png"
                     width="270" height="129" />
                <img src="http://www.baidu.com/img/bd_logo1.png"
                width="270" height="129" />
             </div>
                <div>
                    选择器2<div>选择器2中的div</div>
            	</div>
        </div>
    </body>
    <script type="text/javascript">
        console.log("=========后代选择器-选择所有后代=====");
        var ancestorS = $('#parent div');
        ancestorS.each(function(){
        	console.log($(this).text());
        });
        console.log("=========⼦代选择器-选择⼉⼦辈=====");
        var child = $('#parent>div');
        child.each(function(){
        	console.log($(this).text());
        });
        console.log("=========相邻选择器=====");
        var pre_next = $(".gray + img");
        console.log(pre_next.length);
        console.log("=========同辈选择器,其后，（弟弟）=====");
        var pre_siblings = $(".gray ~ img");
        console.log(pre_siblings.length);
    </script>
</html>
```

## 4、Jquery Dom操作

​		jQuery也提供了对HTML节点的操作，⽽且在原⽣js的基础之上进⾏了优化，使⽤起来更加⽅便。常⽤的从⼏个⽅⾯来操作，查找元素（选择器已经实现）；创建节点对象；访问和设置节点对象的值，以及属性；添加节点；删除节点；删除、添加、修改、设定节点的CSS样式等。注意：以下的操作⽅式只适⽤于jQuery对象。

### 4.1. 操作元素的属性

#### 4.1.1. 获取属性

| ⽅法           | 说明                                                         | 举例                             |
| -------------- | ------------------------------------------------------------ | -------------------------------- |
| attr(属性名称) | 获取指定的属性值，操作 checkbox 时，<br/>选中返回 checked，没有选中返回 undefined。 | attr('checked')<br/>attr('name') |
| prop(属性名称) | 获取具有true和false两个属性的属性值                          | prop('checked')                  |

#### 4.1.2. 设置属性

| ⽅法                   | 说明                                                         | 举例                                            |
| ---------------------- | ------------------------------------------------------------ | ----------------------------------------------- |
| attr(属性名称，属性值) | 设置指定的属性值，<br/>操作 checkbox 时，<br/>选中返回 checked，<br/>没有选中返回 undefined | attr('checked',’checked’)<br/>attr('name',’zs’) |
| prop(属性名称，属性值) | 设置具有true和false的属性值                                  | prop('checked',’true’)                          |

#### 4.1.3. 移除属性

| ⽅法               | 说明           | 举例                  |
| ------------------ | -------------- | --------------------- |
| removeAttr(属性名) | 移除指定的属性 | removeAttr('checked') |



```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>操作元素的属性</title>
	</head>
	<body>
		<!-- 
			属性分类：
				1.固有属性
					元素自带属性
				2.自定义属性
					自己设置的属性名和属性值
				3.属性值为布尔类型的属性
					checked selected disable
				
			属性方法
				attr    可以操作固有属性和自定义属性
						获取布尔类型的属性值，如果存在就返回具体的值，如果不存在就返回undefined
				prop 	可以操作固有属性和不可以操作自定义属性
						获取布尔类型的属性值，如果存在就返回具体的值，如果不存在就返回undefined
						
			设置属性
				attr('属性名',"属性值");
				prop('属性名',"属性值");
		 -->
		<form action="" id="myform">
			<input type="checkbox" id="aa" data="标签1" name="ch" checked="checked" value="1"/> aa
			<input type="checkbox" id="bb" data="标签2" name="ch" value="2"/> bb
		</form>	
		
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8">	</script>
		<script type="text/javascript">
			var aa = $("#aa");
			var bb = $("#bb");
			//console.log(aa);
			
			//获取固有属性
			console.log(aa.attr("name")+"-->" +aa.attr("value"));//ch-->1
			console.log(bb.attr("name")+"-->" +bb.attr("value"));//ch-->2
			
			//获取自定义属性
			console.log(aa.attr("data"));//标签1
			console.log(bb.attr("data"));//标签2
			//prop不可以获取自定义属性
			console.log(aa.prop("data"));//underfined
			console.log(bb.prop("data"));//underfined
			
			//操作boolean类型的数据
			console.log(aa.prop("checked")+" "+ aa.attr("checked"));//true checked
			console.log(bb.prop("checked")+" "+ bb.attr("checked"));//false checked
			
			//设置属性
			var cc = $("[ name='ch']");
			//设置自定义属性
			cc.attr("data","biaoqian")
			cc.prop("data","biaoqian1")//无效果
			
			//设置固有属性
			cc.attr("id","1");//两个id变为1
			cc.prop("id","2");//两个id变为2 
			
			//操作布尔类型值的属性	
		</script>
	</body>
</html>

```

### 4.2. 操作元素的样式

​		对于元素的样式，也是⼀种属性，由于样式⽤得特别多，所以对于样式除了当做属性处理外还可以有专⻔的⽅法进⾏处理。

| ⽅法                   | 说明                          |
| ---------------------- | ----------------------------- |
| attr("class")          | 获取class属性的值，即样式名称 |
| attr("class","样式名") | 修改class属性的值，修改样式   |
| addClass("样式名")     | 添加样式名称                  |
| css()                  | 添加具体的样式                |
| removeClass(class      | 移除样式名称                  |

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>操作元素样式</title>
		<style type="text/css">
			div{
				padding: 8px;
				width: 180px;
			}
			.blue{
				background: blue;
			}
			.larger{
				font-size: 30px;
			}
			.green {
				background : green;
			}
		</style>
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<!--
			attr(“class”)					获取class属性的值，即样式名称
			attr(“class”,”样式名”)			修改class属性的值，修改样式     会覆盖原有样式
			addClass(“样式名”)				添加样式名称
			css()							添加具体的样式 
			removeClass(class)				移除样式名称
		 -->
		 <!--
		 	attr(“class”)					获取class属性的值，即样式名称
		 	attr(“class”,”样式名”)			修改class属性的值，修改样式     会覆盖原有样式
		 	addClass(“样式名”)				添加样式名称
		 	css()							添加具体的样式 
		 	removeClass(class)				移除样式名称
		  -->
		  <h3>css()方法设置元素样式</h3>
		 <div id="conBlue" class="blue larger">天蓝色</div>
		 <div id="conRed">大红色</div>
		 <div id="con" class="blue green">没有颜色</div>
		 <div id="remove" class="blue larger">天蓝色</div>
		 
		 <script type="text/javascript">
		 	//通过id获取元素
			var conBlue = $("#conBlue");
			var bclass = conBlue.attr("class");
			//console.log(bclass);//blue larger
			
			//修改class属性的值，修改样式
			conBlue.attr("class","blue");//去除了large效果
			
			
			//通过id获取元素
			var conRed = $("#conRed");
			//添加大字体样式
			conRed.addClass("larger");//字体变大
			
			var con = $("#con");
			//这里不会对已有的样式修改
			//con.addClass("blue");
			// con.addClass("green");
			
			//添加具体样式
			
			con.css("color","red")
			con.css({
				"background-color":"blue",
				"font-family":"华文新魏"
			});
			
			
			//移除样式
			var remove = $("#remove");
			//移除蓝色样式
			remove.removeClass("blue");
		 </script>
	</body>
</html>

```

### 4.3. 操作元素的内容

​		对于元素还可以操作其中的内容，例如⽂本，值，甚⾄是html。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<!--
			操作元素的内容
				1.设置、获取元素内容      识别html/标签内容
					获取：html();
					设置：html("内容");
				2.设置、获取纯文本内容   不能识别html/标签内容
					获取：text();
					设置：text("内容");
				3.设置、获取表单元素的值
					获取：val();
					设置：val("值");
					
		 -->
		<h3><span>html()和text()方法设置元素内容</span></h3>
		<div id="html"></div>
		<div id="text"></div>
		<input type="text" name="uname" value="oop" />
		
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			//获取h3标签元素
			var h3 = $("h3");
			//获取元素内容
			//html（）可识别标签
			console.log(h3.html());//<span>html()和text()方法设置元素内容</span>
			//text（）不可识别标签
			console.log(h3.text());//html()和text()方法设置元素内容
			
			//获取div
			$("#html").html("<h3><span>html()和text()方法设置元素内容</span></h3>");
			$("#text").text("<h3><span>html()和text()方法设置元素内容</span></h3>");
			
			
			//设置表单元素
			console.log($("[name = 'uname']").val());//oop
			//修改表单元素的value
			$("[name = 'uname']").val("www");
			
		</script>
	</body>
</html>

```

### 4.4. 创建元素和添加元素

```html

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			div {
			margin: 10px 0px;
			}
			span{
			color: white;
			padding: 8px
			}
			.red{
			background-color: red;
			}
			.blue{
			background-color: blue;
			}
			.green{
			background-color: green;
			}
		</style>
	</head>
	
	<body>
		<!-- 
			创建元素
				在jQuery中创建元素很简单，直接使⽤核⼼函数即可
				4.5. 添加元素
				$('元素内容');
				$('<p>this is a paragraph!!!</p>');
				
			添加元素
				prepend(content)
				在被选元素内部的开头插⼊元素或内容，被追加的 content 参
				数，可以是字符、HTML 元素标记。
				$(content).prependTo(selector) 把 content 元素或内容加⼊ selector 元素开头
				append(content)
				在被选元素内部的结尾插⼊元素或内容，被追加的 content 参
				数，可以是字符、HTML 元素标记。
				$(content).appendTo(selector) 把 content元素或内容插⼊selector 元素内，默认是在尾部
				before() 在元素前插⼊指定的元素或内容:$(selector).before(content)
				after() 在元素后插⼊指定的元素或内容:$(selector).after(content)
			
		 -->
		 
		 <h3>prepend()⽅法前追加内容</h3>
		 <h3>prependTo()⽅法前追加内容</h3>
		 <h3>append()⽅法后追加内容</h3>
		 <h3>appendTo()⽅法后追加内容</h3>
		 <span class="red">男神</span>
		 <span class="blue">偶像</span>
		 <div class="green">
		 <span >⼩鲜⾁</span>
		 </div>
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			//创建元素
			console.log($("<h2>jquery</h2>"))
			
			//内部前追加
			
			var str = "<span>wse</span>";
			$(".green").prepend(str);
			
			var str1 = "<span>www</span>";
			$(str1).prependTo($(".green"));
			
			var str2 = $("<span>阿恩</span>");
			str2.prependTo($(".green"));
			
			//内部后追加
			var str3 = "<span>nb</span>";
			$(".green").append(str3);
			
			var str4 = $("<span>wp</span>");
			str4.appendTo($(".green"));
			
			//before
			$(".red").before("<span class='red'>男神</span>")
			//after
			$(".blue").after("<span class='blue'>周周</span>")
		</script>
	</body>
</html>
```

### 4.5删除元素

| ⽅法     | 说明                                                   |
| -------- | ------------------------------------------------------ |
| remove() | 删除所选元素或指定的⼦元素，包括整个标签和内容⼀起删。 |
| empty()  | 清空所选元素的内容                                     |

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			span{
			color: white;
			padding: 8px;
			margin: 5px;
			float: left;
			}
			.green{
			background-color: green;
			}
			.blue{
			background-color: blue;
			}
		</style>
	</head>
	<body>
		<!-- 
			remove() 删除所选元素或指定的⼦元素，包括整个标签和内容⼀起删。
			empty() 清空所选元素的内容
		 -->
		 
		 <h3>删除元素</h3>
		 <span class="green">jquery<a>删除</a></span>
		 <span class="blue">javase</span>
		 <span class="green">http协议</span>
		 <span class="blue">servlet</span>
		 <script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
		 <script type="text/javascript">
			 
		 	//remove（）删除green
			//$(".green").remove();
			//empty() 清空green中的内容 会清空字标签
			$(".green").empty();		
		 </script>
	</body>
</html>
```

### 4.6. 遍历元素

​	each()
​	$(selector).each(function(index,element)) :遍历元素
​	参数 function 为遍历时的回调函数，
​	index 为遍历元素的序列号，从 0 开始。
​	element是当前的元素，此时是dom元素。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>遍历元素</title>
		<style type="text/css">
			span{
			color: white;
			padding: 8px;
			margin: 5px;
			float: left;
			}
			.green{
			background-color: green;
			}
			.blue{
			background-color: blue;
			}
		</style>
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		
		 
		 <h3>遍历元素 each()</h3>
		 <span class="green">jquery</span>
		 <span class="green">javase</span>
		 <span class="green">http协议</span>
		 <span class="green">servlet</span>
			
	</body>
	<script type="text/javascript">
		var spans = $("span");
		spans.each(function(index,element){
			console.log(index);
			console.log(element);
			
		})
	</script>
</html>
```

## 5、Jquery事件

### 5.1ready加载事件

​		ready()类似于 onLoad()事件
​		ready()可以写多个，按顺序执⾏
​		$(document).ready(function(){})等价于$(function(){})

### 5.2绑定事件

​		为被选元素添加⼀个或多个事件处理程序，并规定事件发⽣时运⾏的函数。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		 <script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<!-- 
			ready()类似于 onLoad()事件
			ready()可以写多个，按顺序执行
			$(document).ready(function(){})等价于$(function(){})
			
			ready与onload的区别
				ready 网页中dom结构加载完毕后执行
				load 网页中dom结构与引入的资源加载完毕后执行
			
			
			
			bind()绑定事件
				$(selector).bind( eventType [, eventData], handler(eventObject));
			
		 -->
		 <button type="button" id="i1">按钮1</button>
		 <button type="button" id="i2">按钮2</button>
		 <button type="button" id="i3">按钮3</button>
		 <button type="button" id="i4">按钮4</button>
		 <script type="text/javascript">
			 
			 //load加载事件
		 	window.onload = function(){
				console.log("load加载事件")
			}
			//ready加载事件
			$(document).ready (function(){
				console.log("ready加载事件")
			}) 
			
			//bind绑定事件
			$("#i1").bind("click",function(){
				console.log("按钮1，点击事件")
			})
			//bind绑定多个事件
			$("#i1").bind("mouseover",function(){
				console.log("按钮1，悬停事件")
			})
			
			//简写
			$("#i2").bind("click",function(){
				console.log("按钮2，点击事件")
			}).bind("mouseover",function(){
				console.log("按钮2，悬停事件")
			})
			
			//简写
			$("#i3").bind({
				"click":function(){
					console.log("按钮3，点击事件")
				},
				"mouseover":function(){
					console.log("按钮4，悬停事件")
				}
			})
			
			
			$("#i4").click(function(){
				console.log("按钮4，点击事件")
			}).mouseover(function(){
				console.log("按钮4,悬停事件")
			})
			
			
		 </script>
	</body>
</html>
```

## 6、Jquery Ajax

### 6.1$.ajax

​		jquery 调⽤ ajax ⽅法：
​		格式：$.ajax({});
​		参数：
​		type：请求⽅式 GET/POST
​				url：请求地址 url
​				async：是否异步，默认是 true 表示异步
​				data：发送到服务器的数据
​				dataType：预期服务器返回的数据类型
​				contentType：设置请求头
​				success：请求成功时调⽤此函数
​				error：请求失败时调⽤此函数

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>Ajax</title>
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	
	<body>
		<!-- 
			
		 -->
		 <script type="text/javascript">
			 //get请求
		 	$.ajax({
				type:'GET',
				url:'js/data.json',
				data:{
					uname:'admin',
					pwd:'1224'
				},
				success : function(msg){
					console.log(msg)
				}
				
			})
			//post请求，需要服务端
			$.ajax({
				type:'POSt',
				url:'js/data.json',
				data:{
					uname:'admin',
					pwd:'1224'
				},
				success : function(msg){
					console.log(msg)
				}
				
			})
			
			$.get('js/data.json',{
					uname:'admin',
					pwd:'1224'
				}, function(msg){
					console.log(msg)
				});
		 </script>
	</body>
</html>
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>Ajax</title>
		<script src="js/jquery-3.5.1.min.js" type="text/javascript" charset="utf-8"></script>
	</head>
	
	<body>
		<!-- 
			
		 -->
		 <script type="text/javascript">
			 //get请求
		 	$.ajax({
				type:'GET',
				url:'js/data.json',
				data:{
					uname:'admin',
					pwd:'1224'
				},
				success : function(msg){
					console.log(msg)
				}
				
			})
			//post请求，需要服务端
			$.ajax({
				type:'POSt',
				url:'js/data.json',
				data:{
					uname:'admin',
					pwd:'1224'
				},
				success : function(msg){
					console.log(msg)
				}
				
			})
			
			$.get('js/data.json',{
					uname:'admin',
					pwd:'1224'
				}, function(msg){
					console.log(msg)
				});
		 </script>
	</body>
</html>
```



