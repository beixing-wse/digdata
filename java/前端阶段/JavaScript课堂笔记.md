[toc]



# JavaScript课堂笔记

## 1、什么是JavaScript

	JavaScript一种直译式脚本语言，主要用于用来给HTML网页增加动态功能。简称JS.

## 2、JavaScript的基本特点

1. 不需要编译。
2. 主要用来向HTML（标准通用标记语言下的一个应用）页面添加交互行为。
3. 可以直接嵌入HTML页面，但写成单独的js文件有利于结构和行为的分离。
4. 跨平台特性，在绝大多数浏览器的支持下，可以在多种平台下运行（如Windows、Linux、Mac、Android、
   iOS等）。

## 3、JavaScript的引用方式

### 3.1内嵌JS（内联）

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>002-HTML嵌入JS的代码的第二种方式</title>
		<!-- 
			在页头引入JS，指的就是在html页面内编写JavaScript。
			
			<script type="text/javascript">……</script> 格式是固定的，JavaScript代码必须在 <script></script> 标签内编写，并且
			必须设置type属性值为“text/javascript”
		 -->
		 
		 <script type="text/javascript">
		 	window.alert("hello JS")
		 </script>
		 
	</head>
	<body>
		<button type="button">按钮</button>
		
		<button type="button">按钮2</button>
		
	</body>
</html>

```

### 3.2元素事件中引入JS（行内）

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>001-HTML嵌入JS的代码的第一种方式</title>
	</head>
	<body>
		
		<!-- 
			在元素事件中引入JS，就是指在元素的某一个属性中直接编写JavaScript程序或调用JavaScript函数，这个属性指的
			是元素的“事件属性”。
			
			注意：双引号内使用单引号
		 -->
		<input type="button"  value="我是一个按钮" onclick="window.alert('hello,JS')
															window.alert('hello,Jzhangsan')
															window.alert('hello,lisi')
															window.alert('hello,wangwu')
																						"/>
		<!-- window. 可省略 -->
		<input type="button"  value="我是一个按钮2" onclick="alert('hello,JS')
															alert('hello,Jzhangsan')
															alert('hello,lisi')
															alert('hello,wangwu')
																						"/>
	</body>
</html>

```

### 3.3引入外部JS文件(外联)

```javascript
//当页面完全加载完,加载大括号内的代码
window.onload=function(){
	document.getElementById("myspan").onclick=function(){
			alert("sssss");
	}
}

// window.alert("hello jsss!")
// window.alert("hello js!");
```

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>003-HTML嵌入JS的代码的第三种方式</title>
		<!-- 
			引入外部JS文件，说白了就是把JavaScript程序存放在一个后缀名为.js的文件中，然后使用script标签来引用。此
			外，引用外部JS文件的script标签可以放在head标签内，也可以放在body标签中。
		 -->
		<script  src="../js/text.js" type="text/javascript"></script>
		
	</head>
	<body>
		<!-- <script type="text/javascript" src="../js/text.js"> -->
			
		</script>
		<button type="button" id="myspan">按钮</button>
	</body>
</html>

```

## 4、基本语法

### 4.1注释

		跟我们之前学习的HTML和CSS一样，JavaScript代码也有自己的注释方式。在编写JavaScript代码时，我们经常要
在一些关键代码旁做一下注释，这样做的好处很多，比如：方便理解、方便查找或方便项目组里的其它程序员了解
你的代码，而且可以方便以后你对自己代码进行修改。

```javascript
//单行注释内容
/*多行注释内容*/
```

### 4.2标识符

		标识符，就是一个名字。在JavaScript中，变量和函数等都需要定义一个名字，这个名字就可以称为“标识符”。
		标识符规则：
		组成 ->字母、数字、_、$
		开头 -> 其中数字不能开头（即只能以 字母、_、$）
		特殊规定 -> 不能使用js中的关键字

### 4.3关键字

		JavaScript关键字是指在JavaScript语言中有特定含义，成为JavaScript语法中一部分的那些字。JavaScript关键字是
	
		不能作为变量名和函数名使用的，也就是说变量的名称或者函数的名称不能跟系统的关键字重名。使用JavaScript
		关键字作为变量名或函数名，会使JavaScript在载入过程中出现编译错误。

### 4.4数据

		数据是程序的运行过程中，必不可少的一部分。用来描述和记录信息，可以是数值的形式，也可以是逻辑的形式，
		还可以是文本的形式。而且数据本身是不会发生改变的。比如 3， 100， true, "abc"

## 5、变量 var

### 5.1变量定义

		变量，就是指在程序运行过程中，其值是可以改变的。变量的命名，只需满足标识符的规则并且见名知意。变量的
		声明与赋值，在JavaScript中，使用变量之前需要先声明变量。

```javascript
//所有的JavaScript变量都由关键字var声明。
 var 变量名; 
 var 变量名=值;
```

		在声明变量的同时，也可以对变量进行赋值。

### 5.2变量的赋值

		变量的赋值，即将数据存入变量中，通过“=” 赋值号实现

```javascript
    var age ;
    age = 18;
```

		若只声明而没有赋值，则该变量的值为undefined。
		JavaScript 允许省略 var，直接对未声明的变量赋值。但此时变量将变为全局变量（先了解作用域）

### 5.3变量的声明

		声明，即告诉系统，有一个变量存在。若变量未声明就使用，JavaScript会报错，告诉你变量未定义。

### 5.4重复声明

		若使用var重新声明一个已经存在的变量，是无效的。
		但是如果重复声明并赋值了，则会覆盖掉之前的变量。

### 5.5变量提升

		“所有的JavaScript变量都由关键字var声明。” var 变量名; var 变量名=值; var age ; age = 18; var name;
		console.log(name)
		max;//Uncaught ReferenceError: max is not defined，表示捕获引用错误： var min = 0; var min;
		console.log(min); var mid = 5; var mid = 10;
		console.log(min);
## 5、变量 var

### 5.1变量定义

		变量，就是指在程序运行过程中，其值是可以改变的。变量的命名，只需满足标识符的规则并且见名知意。变量的声明与赋值，在JavaScript中，使用变量之前需要先声明变量。

```javascript
//所有的JavaScript变量都由关键字var声明。
 var 变量名; 
 var 变量名=值;
```

		在声明变量的同时，也可以对变量进行赋值。

### 5.2变量的赋值

		变量的赋值，即将数据存入变量中，通过“=” 赋值号实现

```javascript
    var age ;
    age = 18;
```

		若只声明而没有赋值，则该变量的值为undefined。
		JavaScript 允许省略 var，直接对未声明的变量赋值。但此时变量将变为全局变量（先了解作用域）

### 5.3变量的声明

		声明，即告诉系统，有一个变量存在。若变量未声明就使用，JavaScript会报错，告诉你变量未定义。

### 5.4重复声明

		若使用var重新声明一个已经存在的变量，是无效的。
		但是如果重复声明并赋值了，则会覆盖掉之前的变量。

### 5.5变量提升

		JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升。

```javascript
console.log(age);
var age = 18;		//结果显示underfined，表示变量以声明但未赋值。
			
//相当于
var age;
console.log(age);
age = 18;
```



## 6、数据类型

		每一种计算机语言都有自己所支持的数据类型。JavaScript跟传统编程语言不同，它采用的是弱数据方式，也就是说一个变量不必首先做声明，而是在使用或赋值时再确定其数据类型。虽然变量没有类型，但数据本身是存在类型的。
		JavaScript数据类型有2大分类：一是“基本数据类型”，二是“引用/复合数据类型”。
	
		Number、String 、Boolean、Null和Undefined。基本数据类型是按值访问的，因为可以直接操作保存在变量中的实际值。

### 6.1Undefined类型

		Undefifined类型只有一个值，即特殊的undefifined。在使用var声明变量但未对其加以初始化时，这个变量的值就是undefifined，例如：

```javas
var a
console.log(a)	//undefifined
```



### 6.2Null类型

```javas
var car = null; 
console.log(typeof car); 	// "object"
```



### 6.3Bollean类型

		该类型只有两个字面值：true和false。虽然Boolean类型的字面值只有两个，但JavaScript中所有类型的值都有这两个Boolean值等价的值。要将一个值转换为其对应的Boolean值，可以调用类型转换函数Boolean()，例如：

```javascript
var message = 'Hello World';
var messageAsBoolean = Boolean(message);
```

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>boolean数据转换</title>
		<script type="text/javascript">
			/* 
				boolean类型
			 */
			var a = true;
			console.log(Boolean(a));	//true
			var b = false;
			console.log(Boolean(b));	//false
			
			console.log("==============================")
			
			/* 
				String类型
				"" 空字符串 返回false		 任何非空字符串 返回true
			 */
			var c = "";
			console.log(Boolean(c));	// false
			var d = "hello，word！";
			console.log(Boolean(d));	// true
			
			console.log("==============================")
			
			/* 
				Number类型
				任何非零数字值，包括无穷大，返回true
				0和NaN,返回false 
			*/
			var e =12344;
			console.log(Boolean(e));	//true
			var f =0;
			console.log(Boolean(f));	//false
			var g = NaN;
			console.log(Boolean(g));	//false
			
			console.log("=======================")
			
			/* 
				Undefined类型
			 */
			var h = undefined;
			console.log(Boolean(h));	//false
			
			var i ;
			console.log(i);			//underfined
			
			var car = null; 
			console.log(typeof car); 	// object
			
			/* 
				运行这个示例，就会显示一个警告框，
				因为字符串message被自动转换成了对应的Boolean值（true）。由于存在
				这种自动执行的Boolean转换，因此确切地知道在流控制语句中使用的是什么变量至关重要。
			 */
			/* 
				var message = 'Hello World'; 
				if(message) { 
					alert("Value is true");
					 } 
			*/
		</script>
	</head>
	<body>
	</body>
</html>

```



### 6.4Number类型

		这种类型用来表示整数和浮点数值，还有一种特殊的数值，即NaN（非数值 Not a Number）。这个数值用于表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误了）。例如，在其他编程语言中，任何数值除以0都会导致错误，从而停止代码执行。但在JavaScript中，任何数值除以0会返回NaN因此不会影响其他代码的执行。
	
		NaN本身有两个非同寻常的特点。首先，任何涉及NaN的操作（例如NaN/10）都会返回NaN，这个特点在多步计算中有可能导致问题。其次，NaN与任何值都不相等，包括NaN本身。例如，下面的代码会返回false。

```javascript
alert(NaN == NaN); //false
```



		JavaScript中有一个isNaN()函数，这个函数接受一个参数，该参数可以使任何类型，而函数会帮我们确定这个参数是否“不是数值”。isNaN()在接收一个值之后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，例如字符串”10“或Boolean值。而任何不能被转换为数值的值都会导致这个函数返回true。

```javascript
alert(isNaN(NaN)); //true
alert(isNaN(10)); //false(10是一个数值) 
alert(isNaN("10")); //false(可能被转换为数值10) 
alert(isNaN("blue")); //true(不能被转换为数值)
alert(isNaN(true)); //false(可能被转换为数值1)
```

		有3个函数可以把非数值转换为数值：Number()、parseInt()和parseFloat()。第一个函数，即转型函数Number()可以用于任何数据类型，而另外两个函数则专门用于把字符串转换成数值。这3个函数对于同样的输入会返回不同的结果。

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>number类型数据转换</title>
		<script type="text/javascript">
			/* 
				NaN（非数值 Not a Number）
			 */
			/* 
				Number()函数的转换规则
			 */
			// 如果是Boolean值，true和false将分别被替换为1和0
			var num1 = Number(true);
			console.log(num1);		//	1
			var num2 = Number(false);
			console.log(num2);		//	0
			
			console.log("=============================");
			
			// 如果是数字值，只是简单的传入和返回
			var num3 = Number(1);
			console.log(num3);		//	1
			
			console.log("=============================");
			
			// ● 如果是null值，返回0
			var num4 = Number(null);
			console.log(num4);		//	0
			
			console.log("=============================");
			
			//● 如果是undefined，返回NaN
			var num5 = Number(undefined);
			console.log(num5);
			
			console.log("=============================");
			
			/* 
				如果是字符串，遵循下列规则：
					如果字符串中只包含数字，则将其转换为十进制数值，
					即”1“会变成1，”123“会变成123，而”011“会变成11（前导的0被忽略）
					
					如果字符串中包含有效的浮点格式，如”1.1“，则将其转换为对应的浮点数（同样，也会忽略前导0）
					
					如果字符串中包含有效的十六进制格式，例如”0xf“，则将其转换为相同大小的十进制整数值 
					
					如果字符串是空的，则将其转换为0 
					
					如果字符串中包含除了上述格式之外的字符，则将其转换为NaN
			 */
			var num6 = Number("Hello World"); 
			console.log(num6)	;			//NaN
			var num7 = Number("");
			console.log(num7);				//0
			var num8 = Number("000011"); 
			console.log(num8);				//11
			var num9= Number(true);	
			console.log(num9)				//1
			
			console.log("=================");
			
			/* 
				由于Number()函数在转换字符串时比较复杂而且不够合理,	
				因此在处理整数的时候更常用的是parseInt()函数。
			 */
			/* 
				parseInt()函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个
				非空格字符。如果第一个字符串不是数字字符或者负号，parseInt()会返回NaN；也就是说，用parseInt()转换空字
				符串会返回NaN。如果第一个字符是数字字符，praseInt()会继续解析第二个字符，知道解析完所有后续字符或者
				遇到了一个非数字字符。
				例如，"1234blue"会被转换为1234，”22.5“会被转换为22，因为小数点并不是有效的数字
				字符
				
				如果字符串中的第一个字符是数字字符，parseInt()也能够识别出各种整数格式（即十进制、八进制、十六进
				制）
			 */
			
			console.log(parseInt(" 123"));	//123
			console.log(parseInt(""));		//NaN
			console.log(parseInt("123abcd"));		//123
			
			/* 
				如果字符串中的第一个字符是数字字符，parseInt()也能够识别出各种整数格式（即十进制、八进制、十六进
				制）。
			 */
			
			console.log(parseInt("0xA"));		//10		16进制
			console.log(parseInt("071",8));		//57		8进制	
			console.log(parseInt("10",2));		//2			2进制 
			console.log(parseInt("10",10));		//10		10进制
			console.log(parseInt("AF",16));		//175		16进制
			
			console.log("============");
			/* 
				与parseInt()函数类似，parseFloat()也是从第一个字符（位置0）开始解析每个字符。而且也是一直解析到字符串
				末尾，或者解析到遇见一个无效的浮点数字字符为止。也就是说，字符串中的第一个小数点是有效的，而第二个小
				数点就是无效的了，因此它后面的字符串将被忽略。例如，”22.34.5“将会被转换成22.34。
				
				parseFloat()和parseInt()的第二个区别在于它始终都会忽略前导的零。由于parseFloat()值解析十进制值，因此它
				没有用第二个参数指定基数的用法
			 */
			
			console.log(parseFloat("22.34.5"));		//22.34
			console.log(parseFloat("1234abc"));		//1234
			console.log(parseFloat("010101001"));	//10101001
			console.log(parseFloat("0XA"));			//0
			console.log(parseFloat("0999.0"));		//999
			console.log(parseFloat("0999.9"));		//999.9
		</script>
	</head>
	<body>
	</body>
</html>

```



### 6.5String类型

	任何字符串的长度都可以通过访问其length属性取得.

```javascript
alert(str1.length); //输出5
```

	要把一个值转换为一个字符串有两种方式。第一种是使用几乎每个值都有的toString()方法。

```javascript
var age = 11; 
var ageAsString = age.toString(); //字符串"11"
```



### 6.6Object类型

## 7、运算符

		JavaScript的运算符按运算符类型可以分为以下5种：
	
		1）算术运算符
	
				+
	
				-
	
				*
	
				/	
	
				%
	
				++
	
				--
	
		2）逻辑运算符
	
				&&				与
	
				||				或
	
				！				非
	
		3）比较运算符
	
				>
	
				<
	
				==
	
				!=
	
				>=
	
				<=
	
		4）赋值运算符
	
				=
	
				+=
	
				-=
	
				*=
	
				/=
	
				%=
	
		5）条件运算符(三元运算符)
	
			条件	？表达式1 ：表达式2
## 8、数组

​		数组是按次序排列的⼀组数据，每个值的位置都有编号（从0开始），整个数组⽤⽅括号表示。

### 8.1数组的定义

​		JS 中定义数组的三种⽅式如下（也可先声明再赋值）：

```
    var arr = [值1,值2,值3]; // 隐式创建
    var arr = new Array(值1,值2,值3); // 直接实例化
    var arr = new Array(size); // 创建数组并指定⻓度
```

### 8.2数组遍历

#### 8.2.1普通for循环遍历

```javascript
for(var i=0; i<=数组.length-1; i++){
}
如：
for(var idx=0;idx<arr.length;idx++){
	console.log(arr[idx]);
}
```



#### 8.2.2for...in

```
for(var 下标(名称任意) in 数组名){
	数组名[下标]是获取元素
} // 下标(名称任意)
如：
for(var idx in arr){
	console.log(arr[idx]);
}
```



#### 8.2.3forEach

```
数组名.forEach(function(element,index){
	// element(名称任意)：元素，index(名称任意)：下标
})
如：
arr.forEach(function(elem,idx){
	console.log(idx + "-->" + elem);
});
```

### 8.3数组方法

```
push 添加元素到最后
unshift 添加元素到最前
pop 删除最后⼀项
shift 删除第⼀项
reverse 数组翻转
join 数组转成字符串
indexOf 数组元素索引
slice 截取（切⽚）数组，原数组不发⽣变化
splice 剪接数组，原数组变化，可以实现前后删除效果
concat 数组合并
```



## 9、函数

​		函数，即⽅法。就是⼀段预先设置的功能代码块，可以反复调⽤，根据输⼊参数的不同，返回不同的值。函数也是对象。

## 10、JS事件

### 10.1什么是事件

​		事件 (Event) 是 JavaScript 应⽤跳动的⼼脏 ，进⾏交互，使⽹⻚动起来。当我们与浏览器中 Web ⻚⾯进⾏某些类型的交互时，事件就发⽣了。事件可能是⽤户在某些内容上的点击、⿏标经过某个特定元素或按下键盘上的某些按键。事件还可能是 Web 浏览器中发⽣的事情，⽐如说某个 Web ⻚⾯加载完成，或者是⽤户滚动窗⼝或改变窗⼝⼤⼩。
​		通过使⽤ JavaScript ，你可以监听特定事件的发⽣，并规定让某些事件发⽣以对这些事件做出响应。

### 10.2事件的作用

- 验证⽤户输⼊的数据。
- 增加⻚⾯的动感效果。
- 增强⽤户的体验度

### 10.3事件的类型

​		JavaScript可以处理的事件类型为：⿏标事件、键盘事件、HTML事件。

​		常用事件

		onload：当⻚⾯或图像加载完后⽴即触发
		onblur：元素失去焦点
		onfocus：元素获得焦点
	    onclick：⿏标点击某个对象
	    onchange：⽤户改变域的内容
	    onmouseover：⿏标移动到某个元素上
	    onmouseout：⿏标从某个元素上离开
	    onkeyup：某个键盘的键被松开
	    onkeydown：某个键盘的键被按下

### 10.4事件处理程序

​		事件就是⽤户或浏览器⾃身执⾏的某种动作。例如 click、load 和 mouseover 都是事件的名字，⽽响应某个事件的函数就叫做事件处理程序（或事件侦听器）。事件处理程序的名以“on”开头，因此 click 事件的事件处理程序就是 onclick，为事件指定处理程序的⽅式有好⼏种。

#### 10.4.1HTML 事件处理程序

​		某个元素⽀持的每种事件，都可以⽤⼀个与相应事件处理程序同名的HTML特性来指定。这个特性的值应该是能够执⾏的JavaScript代码：

```html
<input type="button" value="Press me" onclick="alert('thanks');" />
```

​		这样做有⼀些缺点，例如耦合度过⾼，还可能存在时差问题（当⽤户点击按钮时，处理函数还未加载到，此时处理函数是单独写的⼀段js代码），⽽且在不同的浏览器上可能会有不同的效果。

#### 10.4.2DOM0 级事件处理程序

​		通过JavaScript指定事件处理程序的传统⽅式，就是将⼀个函数赋值给⼀个事件处理程序属性。这种⽅式被所有现代浏览器所⽀持。这种⽅式⾸先必须取得⼀个要操作的对象的引⽤，每个元素都有⾃⼰的事件处理程序属性，这些属性通常全都⼩写，例如onclick，然后将这种属性的值设为⼀个函数，就可以指定事件处理程序了。

```html
<body>
	<button id="myBtn">按钮</button>
	<script type="text/javascript">
        var btn = document.getElementById('myBtn');
        btn.onclick = function(){
        	console.log('you click a button');
        }
	</script>
</body>
```

​		以这种⽅式添加的事件处理程序会在事件流的冒泡阶段被处理。⽽且，只能为同⼀个元素的同⼀个事件设定⼀个处理程序（覆盖），也可以通过删除DOM0级⽅法指定的事件处理程序，只要将属性值设为null即可：

```html
btn.onclick = null;
```

#### 10.4.3DOM2 级事件处理程序

​		“DOM2级事件”定义了两个⽅法，⽤于处理指定和删除事件处理程序的addEventListener() 和removeEventListener()。所有DOM节点都包含这两个⽅法，并且他们都接受3个参数：要处理的事件名、作为事件处理程序的函数和⼀个布尔值。最后这个布尔值参数如果是true，则表示在捕获阶段调⽤事件处理程序；如果是false则表示在冒泡阶段调⽤事件处理程序。

```html
<body>
    <button id="myBtn">按钮</button>
    <script type="text/javascript">
        var btn = document.getElementById('myBtn')
        btn.addEventListener('click',function(){
        	alert('you add a eventListener by DOM2')
        },false)
        btn.addEventListener('click',function(){
        	alert('you add a eventListener by DOM2 again')
        },false)
        function thread(){
        	alert('you add a eventListener by DOM2 第三次')
        }
        btn.addEventListener('click',thread,false)
        btn.removeEventListener('click',thread,false)
    </script>
</body>
```

​		这种⽅式可以为同⼀个元素的同⼀个事件添加多个处理函数。还可删除事件处理函数，注意，在删除的时候，不能删除匿名处理函数。

## 11、BOM

​		BOM的核⼼对象是window，它表示浏览器的⼀个实例。window对象有双重⻆⾊，它既是通过JavaScript访问浏览器窗⼝的⼀个接⼝，⼜是ECMAScript规定的Global对象。这意味着在⽹⻚中定义的任何⼀个对象、变量和函数，都以window作为其Global对象，因此有权访问parseInt()等⽅法。如果⻚⾯中包含框架，则每个框架都拥有⾃⼰的window对象，并且保存在frames集合中。在frames集合中，可以通过数值索引（从0开始，从左⾄右，从上到下）或者框架的名称来访问相应的window对象。

### 11.1Window对象方法

```html
（1）消息框:alert， 常⽤。
alert() ⽅法⽤于显示带有⼀条指定消息和⼀个 OK 按钮的警告框。
（2）输⼊框:prompt，返回提示框中的值。
prompt() ⽅法⽤于显示可提示⽤户进⾏输⼊的对话框。
参数（可选）：
第⼀个参数：要在对话框中显示的纯⽂本。
第⼆个参数：默认的输⼊⽂本。
（3）确认框:confirm，返回 true/false.
confirm() ⽅法⽤于显示⼀个带有指定消息和 OK 及取消按钮的对话框。


<style type="text/css">
    #aa{
        border: 1px solid red;
        height: 100px;
    }
</style>
<body>
    <div id="aa">
    	This is a div
    </div>
    <button onclick="testAlert();">警告</button>
    <button onclick="testComfirm();">修改</button>
    <button onclick="testPrompt();">输⼊</button>
    <script type="text/javascript">
    // 1.警告框
    function testAlert(){
   		alert('警告框！！！');
    }	
    /*
        2.输⼊框
        返回值：输⼊的内容
    * */
    function testPrompt(){
    var item = prompt('请输⼊年龄'); // item得到输⼊的值
    // console.log(item)
    // alert(prompt('请输⼊年龄',18)); // 将输⼊的值输出
    }
    /*
    3.确认框
    返回值：boolean（true|false）
    * */
    function testComfirm(){
    var result = confirm('真的要改吗？');
    if(result){
    var ele = document.getElementById("aa");
        ele.style.color="red";
        ele.innerHTML="<span>fdsfsd</span>";
    }else{
    	alert("没事别瞎点。。。");
   	 	}
    }
    </script>
</body>
```

### 11.2打开窗口

​		window.open()⽅法既可以导航到⼀个特定的URL也可以⽤来打开⼀个新的窗⼝

```html
<script type="text/javascript">
function openBaidu(){
    window.open('http://www.baidu.com','_self'); // _self、_blank等
    // window.open(); //空⽩窗⼝
}
</script>
<input type="button" name="open" value="百度" onclick='openBaidu();' />
```

### 11.3关闭窗口

​		window.close()：关闭窗⼝。

```html
<input type="button" value="关闭窗⼝" onclick="window.close();" />
```

### 11.4时间函数

#### 11.4.1setTimeout()

​		setTimeout() : 在指定的毫秒数后调⽤函数或计算表达式。返回⼀个唯⼀的标识；也可以通过返回的标识clearTimeout(id)： 来清除指定函数的执⾏。

```html
var id = setTimeout(function,times);
```

```html
<script type="text/javascript">
// 延迟3 秒后出现 alert
function hello() {
	alert("对不起, 要你久候");
}
setTimeout("hello()", 3000);
// 时间显示器
var timeout;
	function init(){
	// 拿到当前时间
var date = new Date();
var time = date.toLocaleString();
// 拿到相应对象
var h1 = document.getElementById('h1');
// 根据需求添加样式
if(0==date.getSeconds()){ // 当时间的秒数变成0时，显示红⾊字体
	h1.innerHTML = '<span style="color:red">' + time + '</span>';
} else {
	h1.innerHTML = time;
}
/*
* 定时操作，只执⾏⼀次
第⼀个参数：执⾏的⽅法；第⼆个参数：定时，单位是毫秒
* */
setTimeout(init,1000); // 等多少时间来执⾏
}
// window.setTimeout(init,1000);// 只执⾏⼀次
// 停⽌操作
function stopShow () {
	clearTimeout(timeout);
}
</script>
<body onload="init();">
    <h1 id="h1"></h1>
    <button onclick="stopShow()">时间停⽌</button>
</body>
```

#### 11.4.2 setInteval()

​		setInterval():可按照指定的周期（以毫秒计）来调⽤函数或计算表达式，也可根据返回的标识⽤来结束。该⽅法会不停地调⽤函数，直到 clearInterval() 被调⽤或窗⼝被关闭。

```javascript
var id = setInterval(function,times);
clearInterval(id);
function test(){
console.log(".....");
}
// window是⼀个全局对象，通过全局对象调⽤setInterval()函数
window.setInterval(test,1000);
```

### 11.5history对象

​		history 对象是历史对象。包含⽤户（在浏览器窗⼝中）访问过的 URL。history 对象是 window 对象的⼀部分，可通过 window.history 属性对其进⾏访问。
​		history对象的属性：length，返回浏览器历史列表中的 URL 数量。
​		history对象的⽅法：
​		back()：加载 history 列表中的前⼀个 URL。
​		forward()：加载历史列表中的下⼀个 URL。当⻚⾯第⼀次访问时，还没有下⼀个url。
​		go(number|URL): URL 参数使⽤的是要访问的 URL。⽽ number 参数使⽤的是要访问的 URL 在 History的 URL 列表中的相对位置。go(-1)，到上⼀个⻚⾯

```html
<body>
	<a href="013-history-a.html">013-history-a.html</a>
	<h1>我是第⼀个⻚⾯</h1>
	<input type="button" value="前进" onclick="window.history.forward();" />
    <script>
    	console.log(window.history);
    </script>
</body>
```

```html
<body>
    <a href="013-history-b.html">013-history-b.html</a>
    <h1>我是A⻚⾯</h1>
    <input type="button" value="后退" onclick="window.history.back();"/>
</body>
```

```html
<body>
    <h1>我是B⻚⾯</h1>
    <input type="button" value="第⼀个⻚⾯"onclick="window.history.go(-2);"/>
    <input type="button" value="后退" onclick="window.history.back();"/>
</body>
```

### 11.6location对象

​		location 对象是window对象之⼀，提供了与当前窗⼝中加载的⽂档有关的信息，还提供了⼀些导航功能。也可通过 window.location 属性来访问。
​		location 对象的属性 href：设置或返回完整的 URL
​		location 对象的⽅法
​		reload()：重新加载当前⽂档。
​		replace()：⽤新的⽂档替换当前⽂档。

```html
<script type="text/javascript">
    function openBaidu(){
        // 没有历史记录,⽤新的⽂档替换当前⽂档
        // window.location.replace("http://www.baidu.com");
        // console.log(window.location.href); // 获取完整的url
        window.location.href = "http://www.baidu.com";
    }
</script>
<body>
    <input type="text" value="" />
    <input type="button" value="刷新" onclick="window.location.reload();" />
    <input type="button" value="百度" onclick="openBaidu();" />
</body>
```

## 12、DOM对象

​		DOM：Document Object Model ⽂档对象模型
​		要实现⻚⾯的动态交互效果，bom 操作远远不够，需要操作 html 才是核⼼。如何操作 html，就是DOM。简单的说，dom 提供了⽤程序动态控制 html 接⼝。DOM即⽂档对象模型描绘了⼀个层次化的节点树，运⾏开发⼈员添加、移除和修改⻚⾯的某⼀部分。dom 处于javascript 的核⼼地位上。
​		每个载⼊浏览器的 HTML ⽂档都会成为 Document 对象。Document 对象使我们可以从脚本中对 HTML⻚⾯中的所有元素进⾏访问。Document 对象是 Window 对象的⼀部分，可通过 window.document 属性对其进⾏访问。

### 12.1节点

​		加载 HTML ⻚⾯时，Web 浏览器⽣成⼀个树型结构，⽤来表示⻚⾯内部结构。DOM 将这种树型结构理解为由节点组成，组成⼀个节点树。对于⻚⾯中的元素，可以解析成以下⼏种类型的节点：

| 节点类型 | HTML内容         | 例如                  |
| -------- | ---------------- | --------------------- |
| ⽂档节点 | ⽂档本身         | 整个⽂档 document     |
| 元素节点 | 所有的HTML元素   |                       |
| 属性节点 | HTML元素内的属性 | id、href、name、class |
| ⽂本节点 | 元素内的⽂本     | hello                 |
| 注释节点 | HTML中的注释     |                       |


html --> ⽂档节点
div --> 元素节点
title --> 属性节点
测试 Div --> ⽂本节点

### 12.2操作元素的节点

​		当HTML⽂档在被解析为⼀颗DOM树以后，⾥⾯的每⼀个节点都可以看做是⼀个⼀个的对象，我们称为DOM对象，对于这些对象，我们可以进⾏各式各样的操作，查找到某⼀个或者⼀类节点对象，可以创建某种节点对象，可以在某个位置添加节点对象，甚⾄可以动态地删除节点对象，这些操作可以使我们的⻚⾯看起来有动态的效果，后期结合事件使⽤，就能让我们的⻚⾯在特定时机、特定的事件下执⾏特定的变换。

### 12.2.1获取节点


​		在进⾏增、删、改的操作时，都需要指定到⼀个位置，或者找到⼀个⽬标，此时我们就可以通过Document对象提供的⽅法，查找、定位某个对象（也就是我们说的节点）。

注意：操作 dom 必须等节点初始化完毕后，才能执⾏。

处理⽅式两种:
（1）把 script 调⽤标签移到html末尾即可；
（2）使⽤onload事件来处理JS，等待html 加载完毕再加载 onload 事件⾥的 JS。
获取⽅式如下：

| ⽅法                     | 描述                                            |
| ------------------------ | ----------------------------------------------- |
| getElementById()         | 根据id获取dom对象，如果id重复，那么以第⼀个为准 |
| getElementsByTagName()   | 根据标签名获取dom对象数组                       |
| getElementsByClassName() | 根据样式名获取dom对象数组                       |
| getElementsByName()      | 根据name属性值获取dom对象数组，常⽤于多选获取值 |

```html
<body>
    <p id="p1" class="para">这是⼀个段落<span>⽂本</span></p>
    <p id="p1" class="para">这⼜是⼀个段落</p>
    <input type="text" name="txt" />
    <input type="checkbox" name="hobby" value="游泳" />游泳
    <input type="checkbox" name="hobby" value="篮球" />篮球
    <input type="checkbox" name="hobby" value="⾜球" />⾜球
    <hr />
    <a href="javascript:void(0)" onclick="testById()">按照id获取</a>
    <a href="javascript:void(0)" onclick="testByName()">按照name获取</a>
    <a href="javascript:void(0)" onclick="testByTagName()">按照标签名获取</a>
    <a href="javascript:void(0);" onclick="testByClass();">按照class获取</a>
</body>
```

```html
<script type="text/javascript">
// 按照id获取元素
function testById() {
// 返回单个对象
var p = document.getElementById("p1");
console.log(p);
    // 表示获取元素开始标签和结束标签之间的html结构
    console.log(p.innerHTML);
    console.log(p.innerText); // 表示获取标签之间的普通⽂本
}
// 按照name获取元素
function testByName() {
    // 对象数组
    var ho = document.getElementsByName("hobby");
    console.log(ho);
    for(var i = 0; i <= ho.length - 1; i++) {
        console.log(ho[i].value);
    }
}
// 按照标签名获取元素
function testByTagName() {
    // 对象数组
    var inputArr = document.getElementsByTagName("input");
    for(var i = 0; i < inputArr.length; i++) {
        if(inputArr[i].type == "text") {
        	console.log("text类型");
    	} else if(inputArr[i].type == "checkbox") {
        	if(inputArr[i].checked) {
       	 		console.log(inputArr[i].value);
			}
		}
	}
}
// 按照class属性获取元素
function testByClass() {
    // 对象数组
    var ps = document.getElementsByClassName("para");
    console.log(ps[0].innerHTML);
    ps[0].innerHTML += "这是⼀段新的⽂本";
}
</script>
```

### 12.2.2创建节点和插入节点

#### 12.2.2.1创建节点

| ⽅法             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| createElement()  | 创建⼀个新的节点，需要传⼊节点的标签名称，返回创建的元素对象 |
| createTextNode() | 创建⼀个⽂本节点，可以传⼊⽂本内容                           |
| innerHTML        | 也能达到创建节点的效果，直接添加到指定位置了                 |

#### 12.2.2.2插入节点

| ⽅法           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| write()        | 将任意的字符串插⼊到⽂档中                                   |
| appendChild()  | 向元素中添加新的⼦节点，作为最后⼀个⼦节点                   |
| insertBefore() | 向指定的已有的节点之前插⼊新的节点newItem：要插⼊的节点exsitingItem：参考节点 需要参考⽗节点 |

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<!-- 
			createElement() 创建⼀个新的节点，需要传⼊节点的标签名称，返回创建的元素对象
			createTextNode() 创建⼀个⽂本节点，可以传⼊⽂本内容
			innerHTML 也能达到创建节点的效果，直接添加到指定位置了
			write() 将任意的字符串插⼊到⽂档中
			appendChild() 向元素中添加新的⼦节点，作为最后⼀个⼦节点
			insertBefore()
			向指定的已有的节点之前插⼊新的节点newItem：要插⼊的节点exsitingItem：参
			考节点 需要参考⽗节点
		 -->
		<button onclick="addPara();">添加段落</button>
		<button onclick="addImg();">添加图片</button>
		<button onclick="addTxt();">添加文本框</button>
		<button onclick="addOptions()">添加选项</button>
		<select name="music">
			<option value="-1">你心内的一首歌</option>
			<option value="0">南山南</option>
			<option value="1">喜欢你</option>
		</select>
		<hr />
		<div id = "container"></div>
		
		<script type="text/javascript">
			//获取div
			var div = document.getElementById("container");
			//console.log(div);
			//添加段落
			function addPara(){
				//方式1
				// //创建节点
				var p = document.createElement("p");
				// //console.log(p);
				// //创建文本节点
				// var text = document.createTextNode("段落标签")
				// p.appendChild(text);
				// div.appendChild(p);
				// //console.log(p);
				
				//方式2 
				// var p = document.createElement("p");
				// p.innerHTML = "需要文本";
				// div.appendChild(p);
				
				//方式2
				var str = "<p>段落标签</p>"
				div.innerHTML += str;
				
			}
			
			//添加图片
			function addImg(){
				//方式1
				// //创建图片标签
				 var img = document.createElement("img");
				// //设置src属性
				// img.src = "宝宝.png";
				// img.width = 500;
				// //获取容器
				// var container = document.getElementById("container")
				//将img节点追加到container中。
				// container.appendChild(img);
				
				
				//方式2 
				// setAttribute() 方法添加指定的属性，并为其赋指定的值。
				// 设置img的src属性
				// img.setAttribute("src","宝宝.png");
				// img.setAttribute("width","500");
				//获取容器
				//var container = document.getElementById("container")
				//将img节点追加到container中。
				container.appendChild(img);
				
				//方式3 innerhtml
				var str = "<img src = '宝宝.png' width = 500px></img>";
				div.innerHTML += str;
				
			}
			
			//添加文本框
			function addTxt(){
				//创建文本框
				var txt = document.createElement("input");
				//方式1
				// txt.type = "text";
				// txt.value = "添加成功";
				//div.appendChild(txt);
				
				//方式2 
				txt.setAttribute("type","txt");
				txt.setAttribute("value","添加失败");
				div.appendChild(txt);				
			}
			
			//添加下拉框
			function addOptions(){
				//弹窗输入歌名
				var str = window.prompt("输入歌名");
				//获取select节点
				var sel =document.getElementsByName("music")[0];
				//方式1
				var option = document.createElement("option");
				// option.value = 2;
				// option.text = str;
				option.setAttribute("value","2");
				var geming = document.createTextNode(str);
				option.appendChild(geming);
				sel.appendChild(option);
				
				//方式2
				//sel.options.add(option);
				
				//方式3
				//sel.innerHTML += "<option value = '2' >1978</option>"
				
			}
			
			
			
		</script>
	</body>
</html>
[]
```



### 12.3删除节点

```html
<script type="text/javascript">
    function delNode(){
        var programmer =document.getElementById("programmer");
        // 从⽗元素中删除节点，获取要删除对象的⽗元素，然后从⽗元素中删除该对象
        programmer.parentNode.removeChild(programmer);
    }
</script>
<body>
    <span id="programmer">程序猿</span>
    <a href="javascript:void(0)" onclick="delNode();">删除</a>
</body>
```

## 13、表单

### 13.1获取表单

1、document.表单名称
2、document.getElementById(表单 id);
3、document.forms[表单名称]
4、document.forms[索引]; //从 0 开始

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<!-- 
				1.document.表单名称
				2、document.getElementById(表单 id);
				3、document.forms[表单名称]
				4、document.forms[索引]; //从 0 开始
				例如：
				5.2. 获取表单元素
				5.2.1. 获取input元素
				如 text password hidden textarea等，前两种常⽤。
				5.2.2. 获取单选按钮
		 -->
		
		<form id='myform' name="myform" action="" method="post"></form>
		<form id='myform2' name="myform2" action="" method="post"></form>
		
		<script>
			//四种方式
			// var form =document.getElementById("myform");
			var form =document.myform;
			// form =document.forms["myform"];
			// form =document.forms[0];
			console.log(form);
		</script>
	</body>
</html>
```



### 13.2获取表单元素

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<!-- 
			1)、通过 id 获取：document.getElementById(元素 id);
			2)、通过 form.名称形式获取: myform.元素名称; name属性值
			3)、通过 name 获取 :document.getElementsByName(name属性值)[索引] // 从0开始
			4)、通过 tagName 数组 :document.getElementsByTagName('input')[索引] // 从0开始
		 -->
		 <form id='myform' name="myform" action="" method="get">
			 姓名:<input type="text" id="uname" name="uname" value="zs"/><br />
			 密码:<input type="password" id="upwd" name="upwd" value="1234"/><br />
			 <input type="hidden" id="uno" name="uno" value="隐藏域" />
			 个人说明:<textarea name="intro"></textarea>
			 <button type="button" onclick="getTxt();" >获取元素内容</button>
		 </form>
		 <br>
		 <br>
		 <form action="" name="myform">
			 性别<input type="radio" name="rad" value="我是带把的" /> 男
			 <input type="radio" name="rad" value="我是林黛玉" /> 女
			 <button type="button" onclick="get();" >获取性别</button>
			 <div id="div">
			 	
			 </div>
		 </form>
		 
		 <form action="" method="post">
		 	<input type="checkbox" name="hobby" id="" value="sing" />唱
		 	<input type="checkbox" name="hobby" id="" value="dance" />跳
		 	<input type="checkbox" name="hobby" id="" value="rap" />rap
			<button type="button" onclick="getHobby();" >获取爱好</button>
			<div id="div1">
				
			</div>
		 </form>
		 
		 <script type="text/javascript">
			 
			 //获取input元素
		 	function getTxt(){
				//通过id获取
				var uno = document.getElementById("uno");
				console.log(uno.value);
				//通过 myform.元素名称（name）
				var uname = document.getElementById("uname");
				//console.log(uname.value);
				//通过标签名获取
				var upwd = document.getElementsByTagName("input")[1]
				//console.log(upwd.value);
				//通过name获取
				var uname1 = document.getElementsByName("uname")[0];
				//console.log(uname1.value);
				var intro = document.getElementsByName("intro")[0];
				//console.log(intro.value);
				//console.log(uname.value );
				console.log(uname.value +"，"+ upwd.value +"，"+ intro.value);
			}
			
			//获取单选按钮
			function get(){
				//通过name属性获取按钮节点
				var radios =document.getElementsByName("rad");
				//console.log(radios);
				//循环遍历
				for(var i = 0 ;i <radios.length;i++){
					//被选中的返回true，未选中的返回false
					console.log(radios[i].checked + '----'+ radios[i].value);
					var div =  document.getElementById("div");
					div.innerHTML = radios[i].checked + '----'+ radios[i].value;
				}
			}
			
			//获取爱好
			function getHobby(){
				//通过name获取多选框
				var checkBox = document.getElementsByName("hobby");
				var div =  document.getElementById("div1");
				var result  = ''  ;  
				//循环遍历
				for(var i = 0 ;i <checkBox.length;i++){
					//被选中的返回true，未选中的返回false
					if(checkBox[i].checked){
						result   += checkBox[i].value+',';
					}
				}
				div.innerHTML  =result.substr(0,result.length-1);
			}
		 </script>
	</body>
</html>

```

### 13.3提价表单

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<!-- 
			(1)使用普通button按钮+onclick事件+事件中编写代码:
			 获取表单.submit();
			（2）使用submit按钮 + onclick="return 函数()" +函数编写代码:
			最后必须返回：return true|false;
			（3）使用submit按钮/图片提交按钮 + 表单onsubmit="return 函数();" +函数编写代码:
			最后必须返回：return true|false;
		 -->
		<form id='myform1' name="myform2" action="http://www.baidu.com" method="post" onsubmit="return onsub()">
			<input name="test" id="uname"/><span id="msg"></span><br />
			<!--通过js事件：sub()提交表单-->
			<input type="button" onclick="sub();" value="提交表单1" />
			<input type="submit" onclick="return sub2();" value="提交表单2" />
			<input type="submit" value="onsubmit" /><br />
			<input type="image" src="img/u=71331624,2965806045&fm=23&gp=0.jpg"
			width="60px" height="40px" />
		</form>
		<script type="text/javascript">
			//方式1
			function sub(){
				//var uname = document.getElementById("uname");
				// input的type=button，调用submit()方法提交
				document.myform2.submit();
				
			}
			
			//方式2  进行校验，返回值为true才能提交
			function sub2(){
				var uname = document.getElementById("uname");
				var val = uname.value;
				if(val.length>0){
					return true;
				}
				document.getElementById("msg").innerHTML = "不能空着啊！！！";
				document.getElementById("msg").style.color="red";
				return false; // 不提交
			}
			
			//方式3
			// onsubmit事件提交
			function onsub () {
				var uname = document.getElementById("uname");
				var val = uname.value;
				if(val.length>0){
				return true; // 提交
				}
				document.getElementById("msg").innerHTML = "咋不写呢！~";
				document.getElementById("msg").style.color="red";
				return false; // 不提交
			}
		</script>
	</body>
</html>
```

### 13.4表单验证

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>
		<form id='myform'   name="myform">
			姓名:<input type="text" id="uname" name="uname" /><br />
			密码:<input type="password" id="upwd" name="upwd" /><br />
			年龄:<input type="radio" name="uage" value="0" checked="checked"/>小屁孩
				<input type="radio" name="uage" value="1"/>你懂得 <br />
			爱好:<input type="checkbox" name="ufav" value="篮球"/>篮球
				<input type="checkbox" name="ufav" value="爬床"/>爬床
				<input type="checkbox" name="ufav" value="代码"/>代码<br />
			来自:<select id="ufrom" name="ufrom">
					<option value="-1" selected="selected">请选择</option>
					<option value="0">北京</option>
					<option value="1">上海</option>
			</select><br />
			
			<div id="validate" style="color: red;"></div>
			
			<button type="button" onclick="return checkForm();">提交</button>
			<button type="reset" onclick="resetForm();">重置</button>
		</form>
		
		<script type="text/javascript">
			
			
			//通过id属性获取dom对象的函数
			function $(id){
					return document.getElementById(id);
			}
			//获取div	
			var div = $("validate");	
			//重置表单的方法
			function resetForm(){
				
				div.innerHTML = "";
			}
			
			function checkForm(){
				var flag  = true;
			  
				/* 
					1、验证用户名
						1)不能为空
						2)长度为 6-12 位
				*/
			   //获取用户名值
				var name  = $('uname').value;
				//进行判断
				if(" "  ===name || name.length ==0){
					div.innerHTML = "用户名不能为空<br>";
					flag = false;
				}else if(name.length<6 || name.length>12){
					div.innerHTML = "密码长度在6-12为之间<br>";
					flag = false;
				}
				/* 
			·		2、验证密码
						1)不能为空 *
						2)长度为 6-12 位 
						3)不能包含用户名
				 */
				//获取密码值
				var pwd  = $('upwd').value;
				//进行判断
				if(" "  ===pwd || pwd.length ==0){
					div.innerHTML = "密码不能为空<br>";
					flag = false;
				}else if(pwd.length<6 || pwd.length>12){
					div.innerHTML = "密码长度在6-12为之间<br>";
					flag = false;
				}else if(pwd.length>0&& pwd.indexOf(name)>=0){
					div.innerHTML = "密码 不能包含用户名<br>";
					flag = false;
				}
				 
				/* 
					3、年龄: 必须选择 你懂得
				 */
				//按name获取年龄单选按钮 
				var ageGroup = document.getElementsByName("uage");
				//声明年龄
				var age ;
				//进行判断
				for (var i = 0; i < ageGroup.length; i++) {
					if(ageGroup[i].checked){
						age = ageGroup[i].value;
					}
				}
				if(age==0){
					flag = false;
					div.innerHTML = "小屁孩<br>";
				}
				/* 
					爱好
				 */
				 var ufav = document.getElementsByName("ufav");
				 var favstr = "";
				 for (i = 0;i < ufav.length; i++){
					 if(ufav[i].checked){
					 favstr += ufav[i].value + ",";
					}
				 }
				 favstr = favstr.substr(0,favstr.length-1);
				 if(favstr.length < 1){
					flag = false;
				 }
				 /* 
					来自
				 */
				 var ufrom = $('ufrom');
				 var idx = ufrom.selectedIndex ;
				 var val = ufrom.options[idx].value;
				 var valTxt = ufrom.options[idx].text;
				 if(-1 == val){
					 flag = false;
					 div.innerHTML += "*你来⾃⽕星吗?</br>";
				 }
				 //  满足以上条件 弹出内容
				 if(flag){
					 var str = "";
					 str += "您的姓名是:" + name + "\n";
					 str += "您的密码是:" + pwd + "\n";
					 str += "您的年龄是:" + " 你懂得" + "\n";
					 str += "您的爱好是:" + favstr + "\n";
					 str += "您来自于:" + valTxt + "\n";
					 alert(str);
					 // 设置表单提交的地址
					 myform.action="http://www.baidu.com";
					 // 提交表单
					 myform.submit();
					 return false;
				 } else {
					return false;
				}
			}
			
			
		</script>
	</body>
</html>
```

