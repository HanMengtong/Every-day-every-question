### 数据类型

js中有六种数据类型，包括五种 **基本数据类型** （Number,String,Boolean,Undefined,Null）,和一种 **复杂数据类型** （Object）。

1.Number类型

	Number类型包含整数和浮点数（浮点数数值必须包含一个小数点，且小数点后面至少有一位数字）两种值。

	NaN:非数字类型。特点：① 涉及到的 任何关于NaN的操作，都会返回NaN   ② NaN不等于自身。

	isNaN() 函数用于检查其参数是否是非数字值。

	```
	isNaN(123)  //false   isNaN("hello")  //true
	```

2.String类型

	字符串有length属性。

	字符串转换：转型函数String(),适用于任何数据类型（null,undefined 转换后为null和undefined）；toString()方法（null,defined没有toString()方法）。

3.Boolean类型

	该类型只有两个值，true和false。

4.Undefined类型

	只有一个值，即undefined值。
	
	使用var声明了变量，但未给变量初始化值，那么这个变量的值就是undefined。

5.Null类型

	null类型被看做空对象指针，前文说到null类型也是空的对象引用。

6.Object类型

	js中对象是一组属性与方法的集合。
	
	这里就要说到引用类型了，引用类型是一种数据结构，用于将数据和功能组织在一起。引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。
	
### typeof 与 instanceof 的区别

	typeof 的返回值是一个字符串，该字符串说明运算数的类型。
	
	instanceof 用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。
	
