### 数据类型

js中有六种数据类型，包括五种 **基本数据类型** （Number,String,Boolean,Undefined,Null）,和一种 **复杂数据类型** （Object）。

1.Number类型

	Number类型包含整数和浮点数（浮点数数值必须包含一个小数点，且小数点后面至少有一位数字）两种值。

	NaN:非数字类型。特点：① 涉及到的 任何关于NaN的操作，都会返回NaN   ② NaN不等于自身。

	isNaN() 函数用于检查其参数是否是非数字值。
	
	isNaN(123)  //false   isNaN("hello")  //true

2.String类型

	字符串有length属性。

	字符串转换：转型函数String(),适用于任何数据类型（null,undefined 转换后为null和undefined）；
		
			  toString()方法（null,defined没有toString()方法）。

3.Boolean类型

	该类型只有两个值，true和false。

4.Undefined类型

	只有一个值，即undefined值。
	
	使用var声明了变量，但未给变量初始化值，那么这个变量的值就是undefined。

5.Null类型

	null类型被看做空对象指针，前文说到null类型也是空的对象引用。

6.Object类型

	js中对象是一组属性与方法的集合。
	
	这里就要说到引用类型了，引用类型是一种数据结构，用于将数据和功能组织在一起。
	
	引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。
	
### typeof 与 instanceof 的区别

	typeof 的返回值是一个字符串，该字符串说明运算数的类型。
	
	instanceof 用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。
	
### Ajax 运行机制

	在页面不刷新的情况下，向浏览器发送请求，达到页面和后台的异步交互。
	
	1. 创建 XMLHttpRequest 对象 ( Ajax核心对象 )
	
```
	var xml;
	if (window.XMLHttpRequest)
	{
		//  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
		xml=new XMLHttpRequest();
	}
	else
	{
		// IE6, IE5 浏览器执行代码
		xml=new ActiveXObject("Microsoft.XMLHTTP");
	}
```
		
	2. 向服务器发送请求

	* GET请求
	
```
	xml.open("GET",url,true);
	xml.send();
```
	
	* POST请求
	
```
	xml.open("POST",url,true);
	xml.setRequestHeader("Content-type","application/x-www-form-urlencoded");
	xml.send("fname="+Henry+"&lname="+Ford);
```
	
	3. 服务器响应

```
	xml.onreadystatechange = function(){
		if (xml.readyState === 4 && xml.status === 200){
			//xml.responseText 获得的数据
		}
	}
```

### xml.readyState 状态值

	0: 请求未初始化
	
	1: 服务器连接已建立
	
	2: 请求已接收
	
	3: 请求处理中
	
	4: 请求已完成，且响应已就绪
	
### xml.status 状态码

	1**： 请求收到，继续处理
	
	2**： 操作成功收到，分析、接受
	
	3**： 完成此请求必须进一步处理
	
	4**： 请求包含一个错误语法或不能完成
	
	5**： 服务器执行一个完全有效请求失败
	
### jsonp 原理

JSONP 全称是 JSON with Padding ，是基于 JSON 格式的为解决跨域请求资源而产生的解决方案。

他实现的基本原理是利用了 HTML 里 <script></script> 元素标签，远程调用 JSON 文件来实现数据传递。

### 两列布局

css

```
.div{
	display: flex;
	max-width: 500px;
	height: 300px;
	border: 1px solid #666;
}
.div div{
	height: 100%;
}
.adiv{
	flex: 0 1 100px;
	background: #42B983;
}
.bdiv{
	flex: 0 1 100%;
	background: #2586F3;
}
```

html

```
<div class="div">
  <div class="adiv"></div>
  <div class="bdiv"></div>
</div>
```

### 实现水平垂直居中的方法

1. 已知宽高

```
.div{
	position: absolute;
	top: 50%;
	left: 50%;
	margin: -(height/2)px 0 0 -(width/2)px;
}
```

2. 未知宽高

```
.div{
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50% -50%);
}
```

3. 未知宽高

```
父级
.parent{
	display: flex;
	justify-content: center;
	align-items: center;
}
```

### bind、apply、call的区别

相似点： 都可以改变 this 的指向

不同点： bind 返回的是函数，后续需要进行调用

        apply、call 对函数进行直接调用
		
		call 后面传参与函数中的方法一一对应
		
		apply 的第二参数是个数组，数组中的元素与方法一一对应
		
### var、let、const 的区别

1. var、let 声明变量，const 声明常量

2. var 声明变量存在变量提升 

3. let、const 声明形成块作用域

4. 同一作用域下 let、const 不能重复声明，而 var 可以

### 深拷贝

1. 利用递归去复制所有层级属性

```
function deepClone(obj){
    let objClone = Array.isArray(obj)?[]:{};
    if(obj && typeof obj==="object"){
        for(key in obj){
            if(obj.hasOwnProperty(key)){
                //判断ojb子元素是否为对象，如果是，递归复制
                if(obj[key]&&typeof obj[key] ==="object"){
                    objClone[key] = deepClone(obj[key]);
                }else{
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}    
```

2. JSON对象的parse和stringify

```
function deepClone(obj){
    let _obj = JSON.stringify(obj),
        objClone = JSON.parse(_obj);
    return objClone
```

3. JQ的extend

$.extend( [deep ], target, object1 [, objectN ] )

deep表示是否深拷贝，为true为深拷贝，为false，则为浅拷贝

target Object类型 目标对象，其他对象的成员属性将被附加到该对象上。

object1  objectN可选。 Object类型 第一个以及第N个被合并的对象。 

### rem原理

根据 html 的 font-size 大小而改变。

相当于根元素<html></html>的字体大小的单位。

### split()

用于把一个字符串分割成字符串数组。

```
this.newsData.forEach((e,index) => {
    e.newsTxt = e.newsTxt.split("",40).join("")+"..."   //以空字符串 ("") 作为分割条件，那么 stringObject 中的每个字符之间都会被分割。
    e.newsHMS = e.newsTime.split(" ")  // => ["2014-05-08", "18:00:00"]
});
```

### slice()

从已有的数组中返回选定的元素。返回一个新的数组，包含从 start 到 end （不包括该元素）的 array 中的元素。

array.slice(start,end)

start : 从何处开始选取( 必选 )。

end : 从何处结束选取( 可选 )，不包括该元素。

```
this.news = this.newsData.slice(0,4);   //选取前4个数据
```

### 水仙花数

```
let arr = [];
for (let i = 100; i < 999; i++) {
   let numArr = i.toString().split("");  //分割
   let n1 = Math.pow(numArr[0],3)  //第一位的立方
   let n2 = Math.pow(numArr[1],3)  //第二位的立方
   let n3 = Math.pow(numArr[2],3)  //第三位的立方
   if (i == n1 + n2 + n3) {  //符合条件的添加到新的数组中
       arr.push(i)
   }
}
console.log(arr)
```
