## JavaScript语言精粹

#### 前言
#### 2.1 注释

	建议使用 //
	避免使用 /**/
	原因：
		/*
		   var rm_a = /a*/.match(s);
		*/
#### 2.4 字符串
	
 > JavaScript在被创建的时候，Unicode是16位的字符集，所以JavaScript中所有的字符都是16位的。

#### 2.5 语句
	
 > JavaScript中代码块不会创建一个新的作用域

 * 下面的这些值被当做假(false)
 	- false
 	- null 
 	- undefined
 	- 空字符串''
 	- 数字0，(负数也被当做false)
 	- 数字NaN

 其他所有值都被当做真，包括true，字符串'false'(除空字符串以外的所有字符串)，以及所有的对象。

#### 2.6 表达式
 	
* 运算符优先级 

| 运算符  								| 作用				| 优先级 |
| ------------------------------------- | ----------------- | ------ |
|  `.` `[]` `()`  						| 属性存储及调用 	|   1    |
|  `delete` `new` `typeof` `+` `-` `!`  | 一元运算符 		|   2    |
|  `*` `/` `%`  						| 乘法，除法，取模 	|   3    |
|  `+` `-`  							| 加法/连接，减法 	|   4    |
|  `>=` `<=` `<` `>`  					| 不等于运算符 		|   5    |
|  `===` `!==`  						| 等式运算符 		|   6    |
|  `&&`  								| 逻辑与 			|   7    |
|  `||`		  							| 逻辑或 			|   8    |
|  `? : `   							| 三元 				|   9    |

  `/` 可能会产生一个非整数的结果，即使两个运算数都是整数(计算机精度问题)

#### 3.8 删除对象
	
 * 删除对象属性会让来自原型链中的属性浮现出来

	例：（以后补充）

#### 4.7 给类型增加方法  
<a name="4chapter"></a>

 * 清除字符串空格

```javascript
String.method('trim',function(){
	return this.replace(/^\s+|\s+$/g,'');
	});
```

#### 4.8 递归 

 * 递归（汉诺塔）

```javascript
var hanoi = function(disc, src, aux, dst) {
	if (disc > 0) {
		hanoi(disc - 1, src, dst, aux); //除最大盘外从 src 移到 aux
		document.writeln('move disc ' + disc + ' from ' + src + ' to ' + dst); //最大盘从 src 移到 dst
		hanoi(disc - 1, aux, src, dst); //除最大盘外从 aux 移到 dst
	}
};
hanoi(3, '原地址', '辅助', '目标地址');
```

#### 4.1.5 记忆(fibonacci)
	
  * [ 记忆(斐波那契数列) ](Demo/fibonacci.html)

### 第五章 继承

> 在大多数编程语言中，继承都是一个重要的主题。  
> javaScript是一门弱类型语言，从不需要类型转换。对象的起源是无关紧要的。对于一个对象来说重要的是她能做什么，而不是她从哪里来  
> 基于类的语言中，对象是类的实例，并且类可以从另一个类继承。JavaScript是一门基于原型的语言，这意味着对象可以直接从其他对象继承。  

### 第六章 数组

#### 6.2 长度(length)
```javascript
var arr = [];
arr.length  // 0
arr[1000] = length  // 0
 // 或者
arr[1000] = true    // true
arr.length  // 1001
```
#### 6.3 删除(delete)
```javascript
var arr = ['no','zuo','no','die'];
delete arr[2]  	 // ['no','zuo',undefined,'die']
arr.length // 4
arr.splice(2,1); // ['no','zuo','die']
arr.length // 3
```
#### 6.4 混淆的地方(object is Array)
> 判断数组类型得出来的是对象
```javascript
var arr = [];
typeof arr   // 'object'
```
> 自定义方法判断数组
```javascript
/**
 * @title 判断数组
 * @param {object} 可以传入一个对象
 * @return {true, flase} 返回是否是数组
 */
function is_Array(value){
	return value &&
		typeof value === 'object' &&
		typeof vaule.length === 'number' &&
		typeof vaule.splice === 'function' &&
		!(vaule.propertyIsEnumerable('length'));
}
```

### 第七章 正则表达式
> 大量的标点符号，混乱的思绪，以后回过头来再学

### 第八章 方法
#### Array
<details>
		<summary><b>1、Array.concat(item……)</b> [点击查看]</summary>

> concat 方法返回一个新数组，它包含Array的浅复制(shallow copy) 并将一个或多个参数item附加在其后。如果参数item是一个数组，那么它的每个元素会被分别添加。此外，详情参见Array.push(item……)方法。

```JavaScript
var a = ['a','b','c'];
var b = ['x','y','z'];
var c = a.concat(b,true)  	// c 是 ['a','b','c','x','y','z',true]
```
</details>

<details>
		<summary><b>2、Array.join(separator)</b> [点击查看]</summary>

> join方法把一个Array构造成一个字符串。他将Array中的每个元素构造成一个字符串，并用一个separator(分离器)为分隔符把它们连接在一起。默认的separator(分离器)是 `,` 。为了实现无间隔连接，我们可以用空字符串作为separator.
> 如果你想把大量的片段组装成一个字符串，把这些片段放到一个数组中并用 `join` 方法连接她们通常比用`+`元素运算符连接这些片段要快。

```JavaScript
var a = ['a','b','c'];
a.push('b');
var c = a.join(') 	// c 是 'abcd'
```
* Array.pop()

> `pop`和`push`方法使数组`Array`像堆栈(stack)一样工作。`pop`方法移除`Array`中的最后一个元素并返回该元素。如果该`Array`是空的，他会返回`undefined`
```JavaScript
var a = ['a','b','c','d'];
var c = a.pop() 	// a 是 ['a','b','c'] && c 是 'd'
```
> `pop` 可以像这样实现：
```JavaScript 
Array.method('pop',function(){
	return this.splice(this.length - 1)[0];
	})
```

</details>

<details>
		<summary><b>3、Array.push(item……)</b> [点击查看]</summary>

> `push` 方法将一个或多个参数`item`附件到一个数组的尾部。不像`concat`方法那样，它会修改该数组`Array`,如果参数`item`是一个数组，它会将参数数组作为单个元素整个添加到数组中。它返回这个数组`Array`的新长度值。
```JavaScript
var a = ['a','b','c'];
var b = ['x','y','z'];
var c = a.push(b,true);
// a 是 ['a','b','c',['x','y','z'],true]
// c 是 5;
```
> `psuh` 可以像这样实现：
Array.method('push',function(){
	this.splice.apply(
			this,
			[this.length,0].concat(Array.prototype.slice.apply(arguments))
		);
		return this.length;
});

</details>

<details>
		<summary><b>4、Array.reverse()</b> [点击查看]</summary>
`reverse`方法反转`Array`中的元素的顺序。它返回当前的Array；

```JavaScript
var a = ['a','b','c'];
var b = a.reverse();
// a和b都是 ['c','b','a']
```

</details>

<details>
		<summary><b>5、Array.shift()</b> [点击查看]</summary>

> `shift` 方法移除数组`Array`中的第一个元素并返回该元素。如果这个数组`Array`是空的，它会返回一个`undefined`,`shift`通常比pop慢的多：

```JavaScript
var a = ['a','b','c'];
var c = a.shift(); 		// a 是 ['b','c'] && c 是 'a'
```
>  `shift` 可以这样实现：
```JavaScript
Array.method('shift',function(){
	return this.splice(0,1)[0]
	})
```

</details>

<details>
		<summary><b>6、Array.slice(start,end)</b> [点击查看]</summary>

> `slice`方法对 `Array`中的一段做浅复制。第一个被复制的元素是`Array[start]`。他将一直复制到`Array[end]`为止。`end`参数是可选的，并且默认值是该数组的长度`Array.length`。如果两个参数中的任何一个是负数，`Array.length`将和它们相加来试图使它们成为非负数。如果`start`大于等于`Array.length`,得到的结果将是一个新的空数组。千万别把`slice`和`splice`混淆了。此外请参见后边章节的`String.slice`。
```JavaScript
var a = ['a','b'c],
	b = a.slice(0,1), 	// b 是 ['a']
	c = a.clice(1), 	// c 是 ['b','c']
	b = a.slice(1,20);	// d 是 ['b']
```

</details>

<details>
		<summary><b>7、Array.sort(comparefn)</b> [点击查看]</summary>

> `sort` 方法对`Array`中的内容进行适当的排序。它不能正确地给一组数字排序：
```JavaScript
var n = [4,8,15,16,23,42];
n.sort(); 	// n 是 [15,16,23,4,42,8]
```
> `JavaScript`的默认比较函数假定所有被排序的元素都是字符串。它尚未足够智能到在比较这些元素之前先检测它们的类型，所以当它比较这些数字的时候会将它们转化为字符串，导致得到一个令人吃惊的错误结果。
> 幸运的是，可以使用自己的比较函数来替换默认的比较函数。自己的比较函数应该接受两个参数，并且如果这两个参数相等则返回`0`,如果第一个函数应该排列在前面，则返回一个负数，如果第二个参数应该排列在前面，则返回一个正数。
```JavaScript
n.sort(function(a,b){
	return a -b;
	})
// n 是 [4,8,15,16,23,42]
```
> 上面这个函数将给数字排序，但它不能给字符串排序。如果我们想要给任何简单数组排序，则必须做更多的工作：
```JavaScript
var m = ['aa','bb','a',4,8,15,16,23,42];
m.sort(function(a,b){
		if(a === b){
			return 0;
		}
		if(typeof a === typeof b){
			return a < b ? -1:1;
		}
		return typeof a < typeof b ? -1 : 1;
	});
	// m 是 [4,8,15,16,23,42,'a','aa','bb']
```

> 如果大小写不重要，比较的函数应该在比较运算之前将它们转化为小写。详情参见`String.localeCompare`。
> 如果有一个更智能的比较函数我们也可以给对象数组排序。为了在一般情况下让这个事情更容易，我们将编写一个比较的函数；

```JavaScript
// by 简述接收一个成员名字符串做为参数
// 并返回一个可以用来包含该成员的对象数组进行排序的比较函数
var by = function (name){
	return function(o,p){
		var a,b;
		if(typeof o === 'object' && typeof p === 'object' && o &&p){
			a = o[name];
			b = p[name];
			if(a === b){
				return 0;
			}
			if(typeof a === typeof b){
				return a < b ? -1 : 1;
			}
			return typeof a < typeof b ? -1 : 1;
		}else {
			throw {
				name: 'Error',
				message: 'Expected an object when sorting by' + name;
			};
		}
	};
};
var s = [
	{first:'Joe', last: 'Besser'},
	{first:'Moe', last: 'Howard'},
	{first:'Joe', last: 'DeRita'},
	{first:'Shemp', last: 'Howard'},
	{first:'Larry', last: 'Fine'},
	{first:'Curly', last: 'Howrd'}
];
s.sort(by('first'))
// s 是 [
//	{first:'Curly', last: 'Howrd'}
//	{first:'Joe', last: 'Besser'},
//	{first:'Joe', last: 'DeRita'},
//	{first:'Larry', last: 'Fine'},
//	{first:'Moe', last: 'Howard'},
//	{first:'Shemp', last: 'Howard'},
// ]
```

<details>
		<summary> `sort`语法是不稳定的 <b>[点击查看]</b> ,所以下面的调用	</summary>

_排序的稳定性是指排序后的数组的相等值的相对应位置没有发生改变，而不稳定性排序则会改变相等值的对应位置。详细内容请参见 http://zh.weikepedin.org/wiki/排序算法 。 `JavaScript`的`sort`方法的稳定性根据不同浏览器的实现而不一致。可查见 http://developer.mozilln.org/Cn/Core_JavaScript_1.5_Reference/Global_Objects/Array/Sort 中的介绍。_
</details>

```JavaScript
	s.sort(by('first')).sort(by('last'));
```


> 不能保证产生正确的序列。如果你想基于多个键值进行排序，你需要再次做更多的工作。我们可以修改`by`函数，让其可以接受第二个参数，当主要的键值产生一个匹配的时候，另一个`compare`方法将被调用以决出高下。 

```JavaScript
	// by 函数接受一个成员名字符串和一个可选的次要比较函数做为参数。
	// 并返回一个可以用来对包含该成员的对象数组进行排序的比较函数。
	// 当 `o[name]` 和 `p[name]`相等时，次要比较函数被用来决出高下。
```
```JavaScript
var by = function (name,minor){
	return function(o,p){
		var a,b;
		if(o && p && typeof o === 'object' && typeof p === 'object'){
			a = o[name];
			b = p[name];
			if(a === b){
				return typeof minor === 'function' ? minor(o,p) : 0;
			}
			if(typeof a === typeof b){
				return a < b ? -1 : 1;
			}
			return typeof a < typeof b ? -1 : 1;
		} else {
			throw {
				name: 'Error',
				message: 'Expected an object when sorting by ' + name;
			};
		}
	};
};
s.sort(by('last',by('first')));
// s 是 [
//	{first:'Joe', last: 'Besser'},
//	{first:'Joe', last: 'DeRita'},
//	{first:'Larry', last: '	Fine'},
//	{first:'Curly', last: 'Howrd'}
//	{first:'Moe', last: 'Howard'},
//	{first:'Shemp', last: 'Howard'},
// ]
```

</details>

<details>
		<summary><b>8、Array.splice(start,deleteCount,item……)</b> [点击查看]</summary>

> `splice`方法从`Array`中移除一个或多个元素，并用新的`item`替换它们。参数`start`是从数组`Array`中移除元素的开始位置。参数`deleteCount`是要移除的元素个数。如果有额外的参数，那些`item`都将插入到移除元素的位置上。它返回一个包含被移除元素的数组。
> `splice`最主要的用处是从一个数组中删除元素。千万不要把`splice`和`slice`混淆了；
```JavaScript
var a = ['a','b','c'];
var r = a.splice(1,1,'ache','bug');
// a 是 ['a','ache','bug','c']
// r 是 ['b']
```
> `splice`可以这样实现；
```JavaScript
Array.method('splice',function(start,deleteCount){
		var max = Math.max,
			min = Math.min,
			delta,
			element,
			insertCount = max(arguments.length-1,0),
			k = 0,
			len = this.length,
			new_len,
			result = [],
			shift_count;

		start = start || 0;
		if(start < 0){
			start += len;
		}
		start = max(min(start,len),0);
		deleteCount = max(min(typeof deleteCount === 'number' ? deleteCount : len, len - start),0);
		delta = insertCount - deleteCount;
		new_len = len + delta;
		while(k < deleteCount){
			if(element !== undefined){
				result[k] = element;
			}
			k +=1;
		}
		shift_count = len - start - deleteCount;
		if(delta < 0){
			k = start + insertCount;
			while(shift_count){
				this.[k] = this[k - delta];
				k += 1;
				shift_count -= 1;
			}
			this.length = new_len;
		} else if (delta > 0){
			k = 1;
			while(shift_count){
				this[new_len - k] = this.[len - k];
				k += 1;
				shift_count -= 1;
			}
		}
		for(k = 0; k < insertCount; k += 1;{
			this.[start + k] = arguments[k + 2];
		}
		return result;
	})

```

</details>

<details>
		<summary><b>9、Array.unshift(item……)</b> [点击查看]</summary>

> `unshift`方法像`push`方法一样用于将元素添加懂啊数组中，但它是把`item`插入到`Array`的开始部分而不是尾部。它返回`Array`的新的<summary>长度值[点击查看]</summary>

	<details>
	_IE6之前的浏览器中，`JScript`引擎对`unshift`方法实现有错误，它返回的值永远是`undefined`。`IE7`之后的浏览器修正了这个错误_
	</details>

```JavaScript
var a = ['a','b','c'];
var r = a.unshift('?','@');
// a 是 ['?','@','a','b','c']
// r 是 5
```

> `unshift`可以像这样实现；
```JavaScript
Array.method('unshift', function(){
		this.splice.apply(this.[0,0].concat(Array.prototype.slice.apply(arguments)));
		retrun this.length;
	})
```

</details>

#### Function
<details>
	<summary><b>1、Function.apply(thisArg,argArray)</b> [点击查看]</summary>

> `apply`方法调用函数`function`,传递一个被绑定到`this`上的对象和一个可选的参数数组，`apply`方法被用在`apply`调用模式(applu invocation pattern)[【详见4章】](#4chapter)中

```JavaScript
Function.method('bind', function(that){
// 返回一个函数，调用这个函数就像它是那个对象的方法一样。
var method = this,
    slice = Array.prototype.slice,
    args = slice.apply(arguments,[1]);
return function(){
		return method.apply(that, args.concat(slice.apply(arguments, [0])));
	}
})
var x = function (){
	retrun this.value;
}.bind({value: 666});
alert(x()); 	// 666
```
</details>


#### Number
<details>
	<summary><b>1、Number.toExponential(fractionDigits)</b> [点击查看]</summary>

> `toExponential`方法把这个`number`转换成一个指数形式的字符串。可选参数`fractionDigits`控制其小数点后的数字位数。它的值必须在0值20之间。
```JavaScript
document.writeln(Math.PI.toExponential(0));
document.writeln(match.PI.toExponential(2));
document.writeln(match.PI.toExponential(7));
document.writeln(match.PI.toExponential(16));
document.writeln(match.PI.toExponential());
// 结果
3e + 0
3.14e + 0
3.1415927e + 0
3.1415926535897930e + 0
3.141592653589793e + 0
```

</details>

<details>
	<summary><b>2、Number.toFixed(fractionDigits)</b> [点击查看]</summary>
> `toFixed`方法把这个`number`转换成为一个十进制数形成的字符串。可选参数`fractionDigits`控制其小数点后的数字位数。它的值必须在0和20之间。默认为0；

```JavaScript
document.writeln(Math.PI.toFixed(0));
document.writeln(Math.PI.toFixed(2));
document.writeln(Math.PI.toFixed(7));
document.writeln(Math.PI.toFixed(16));
document.writeln(Math.PI.toFixed());
// 结果
3
3.14
3.1415927
3.1415926535897930
3
```
</details>

<details>
	<summary><b>3、Number.toPrecision(precision)</b> [点击查看]</summary>
> `toPrecision`方法把这个`number`转换成为一个十进制数形成的字符串。可选参数`precision`控制其小数点后的数字位数。它的值必须在0和21之间:

```JavaScript
document.writeln(Math.PI.toPrecision(2));
document.writeln(Math.PI.toPrecision(7));
document.writeln(Math.PI.toPrecision(16));
document.writeln(Math.PI.toPrecision());
// 结果
3.1
3.1415923
3.141592653589793
3.141592653589793
```
</details>

<details>
	<summary><b>4、Number.toString(radix)</b> [点击查看]</summary>
> `toString`方法把这个`number`转换成为一个字符串。可选参数`radix`控制基数。它的值必须在2和36之间。默认为radix是以10为基数的。`radix`参数是最常用的整数，但是可以用任意的数字。
> 在最普通情况下，`number.toString()`可以更简单第写为`String(number)`：

```JavaScript
document.writeln(Math.PI.toString(2));
document.writeln(Math.PI.toString(8));
document.writeln(Math.PI.toString(16));
document.writeln(Math.PI.toString());

// 结果

11.001001000011111101101010100010001000010110100011 
3.1103755242102643
3.243f6a8885a3
3.141592653589793
```
</details>

#### Object

<details>
	<summary><b>object.hasOwnProperty(name)</b> [点击查看]</summary>

> 如果这个`object`包含了一个名为`name`的属性，那么`hasOwnProperty`方法返回`true`。原型链中的同名属性是不会被检查的。这个方法对`name`就是`hasOwnProperty`时不起作用，此时会返回`false`:

```JavaScript
var a = {mermber:true};
var b = Object.beget(a);	// 来自第3章
var t = a.hasOwnPropert('member');	 	// t 是 true
var u = b.hasOwnProperty('member'); 	// u 是 false
var v = b.member; 		// v 是 true
```
</details>

#### RegExp

<details>
	<summary><b>1、regexp.exec(string)</b> [点击查看]</summary>

> `exec`方法是使用正则表达式的最强大(和最慢)的方法。如果它成功地匹配`regexp`和字符串`string`,它会返回一个数组。数组中下标为`0`的元素包含正则表达式`regexp`匹配的字符串。下标为`1`的元素是分组`1`捕获的文本，下标为`2`的元素是分组`2`捕获的文本，以此类推。如果匹配失败，那么它会返回`null`。
> 如果`regexp`带有一个`g`标志(全局标志)，事情标的有点更加复杂了。查找不是从这个字符串的起始位置开始，而是从`regexp.lastIndex`(它的初始化为0)位置开始。如果匹配成功，那么`regexp.lastIndex`将被设置为该匹配后第一个字符串的位置。不成功的匹配会重置`regexp.lastIndex`为0.
> 这就允许通过在一个循环中调用`exec`去查询一个匹配模式在一个字符串中发生几次。有两件事需要注意。如果你提前退出了这个循环，再次进入这个循环前必须把`regexp.lastIndex`重置到`0`。`^`因子也仅匹配`regexp.lastIndex`为`0`的情况。


```JavaScript
// 把一个简单的HTML文本分解为标签和文本。
// (entityify方法请参见string.replace)

// 对每个标签和文本，都产生一个数组包含如下元素
// [0] 整个匹配的标签和文本
// [1] / (斜杠)，如果有的话
// [2] 标签名
// [3] 属性，如果有任何属性的话

var text = '<html><body bgcolor=linen><p>' +
	'This is <b>bold<\/b>!<\/p><\/p><\/body><\/html>';
var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g;
var a,i;
while((a = tages.exec(text))){
	for(i = 0; i < a.length; i +=1){
			document.writenln(('//[' +i+ ']' + a[i]).entityify());
		}
		document.writeln();
	}
// 结果
// [0] <html>
// [1] 
// [3] 

// [0] <body bgcoloe=linen>
// [1]
// [2] body
// [3] bgcolor=linen

// [0] <p>
// [1]
// [2] p
// [3]

// [0] This is
// [1] undefined
// [2] undefined
// [3] undefined

// [0] <b>
// [1] 
// [2] b
// [3]

// [0] bold
// [1] undefined
// [2] undefined
// [3] undefined

// [0] </b>
// [1] /
// [2] p
// [3] 
```
</details>

<details>
	<summary><b>2、regexp.test(string)</b> [点击查看]</summary>

> `test`方法是使用正则表达式的最简单(和最快)的方法。如果该`regexp`匹配`string`，它返回`true`;否则,它返回`false`。不要对这个方法使用`g`标识：


```JavaScript
var b = /&.+;/.test('frank &amp;beans');
// b 是 true
```
> `test` 可以像这样实现：

```JavaScript
RegExp.method('test',function(string){
	return this.exec(string) !== null;
	})
```
</details>

#### String

<details>
	<summary><b>1、string.charAt(pos)</b> [点击查看]</summary>

> `chatAt`方法返回在`string`中`pos`位置处的字符串。如果`pos`小于`0`或大于等于字符串的长度`string.length`,它会返回空字符串。`JavaScript`没有字符串类型(character type)。这个方法返回的结果是一个字符串;

```JavaScript
var name = 'Curly';
var initial = name.charAt(0); 	// initial 是 'c'
```
> `charAt`可以像这样实现:
```JavaScript
String.method('charAt',function(){
		return this.slice(0,1);
	})
```

</details>


<details>
	<summary><b>2、string.charCodeAt(pos)</b> [点击查看]</summary>

> `charCodeAt`方法同`charAt`一样，只不过它返回的不是一个字符串，而是以整数形式表示的在`string`中的`pos`位置处的字符的字符码未。如果`pos`位置处的字符的字符码位。如果`pos`小于`0`或大于等于字符串的长度`string.length`,它返回`NaN`。

```JavaScript
var name = 'Curly';
var initial = name.charCodeAt(0); 	// initial 是 '67'
```
</details>


<details>
	<summary><b>3、string.concat(string……)</b> [点击查看]</summary>

> `concat`方法通过将其他的字符串连接在一起来构建一个新的字符串。它很少被使用，因为`+`运算符更为方便：

```JavaScript
var s = 'C'.concat('a','t'); // s 是 'Cat'
```
</details>


<details>
	<summary><b>4、string.indexOf(searchString,position)</b> [点击查看]</summary>

> `indexOf`方法在`string`内查找另一个字符串`searchString`。如果它被找到，则返回第一个匹配字符的位置，否则返回`-1`。可选参数`position`可设置从`string`的某个指定的位置开始查找：

```JavaScript
var text = 'Mississippi';
var p = text.indexOf('ss'); 	// p 是 2
p = text.indexOf('ss',3); 	// p 是 5
p = text.indexOf('ss',6); 	// p 是 -1
```
</details>


<details>
	<summary><b>5、string.lastIndexOf(searchString,position)</b> [点击查看]</summary>

> `lastIndexOf`方法和`indexOf`方法类似，只不过它是从该字符串的末尾开始查找而不是从开头:

```JavaScript
var text = 'Mississippi';
var p = text.lastIndexOf('ss'); 	// p 是 5
p = text.lastIndexOf('ss',3); 	// p 是 2
p = text.lastIndexOf('ss',6); 	// p 是 5
```
</details>

<details>
	<summary><b>6、string.localeCompare(that)</b> [点击查看]</summary>

> `localeCompare`方法比较两个字符串。如何比较字符串的规则没有详细的说明。如果`string`比价字符串`that`小，那么结果为负数。如果它们是相等的，那么结果为`0`。这类似于`Array.sort`比较函数的约定：

```JavaScript
var m = ['AAA','A','aa','a','Aa','aaa'];
m.sort(function(a,b){
	return a.lovaleCompare(b);
	})
// m (在某些本地环境下) 是 ['a','A','aa','Aa','aaa','AAA']
```
</details>

<details>
	<summary><b>7、string.match(regexp)</b> [点击查看]</summary>

> `match`方法匹配一个字符串和一个正则表达式。它依据`g`标识来决定如何进行匹配。如果没有`g`标识，那么调用`string.match(regexp)`的结果与调用`regexp.exec(string)`的结果相同。然而，如果`regexp`带有`g`标识，那么它返回一个包含除捕获分组以外的所有匹配的数组：

```JavaScript
var text = '<html><body bgcolor=linen><p>' +
		'This is <b>bold<\/b>!<\/p><\/body><\/html>';
var tags = /[^<>]+|<(\/?)([A-Za-z]+)([^<>]*)>/g;
var a,i;
a = text.match(tags);
for(i = 0;i < a.length;i +=1){
	document.writeln(('// [' +i+ ']' + a[i]).entityify());
}

// 结果是

// [0] <html>
// [1] <body bgcolor=linen>
// [2] <p>
// [3] This is
// [4] <b>
// [5] bold
// [6] </b>
// [7] !
// [8] </p>
// [9] </body>
// [10] </html>
```
</details>

<details>
	<summary><b>8、string.replace(searchValue,replaceValue)</b> [点击查看]</summary>

> `replace`方法对`string`进行查找和替换的操作，并返回一个新的字符串。参数`searchValue`可以是一个字符串或一个正则表达式的对象。如果它是一个字符串，那么`searchValue`只会在第一次出现的地方被替换，所以下面的代码结果是`mother-in_law`:

```JavaScript
var result = "mother_in_law".replace('_','-');
```
> 这或许令你失望。
> 如果`searchValue`是一个正则表达式并且带有`g`标志，那么它将替换所有匹配之处。如果它没有带`g`标志，那么它将金体会第一个匹配之处。
> `replaceValue`可以是一个字符串或者一个函数。如果`replaceValue`是一个字符串，字符`$`拥有特别的含义：

```JavaScript
// 捕获括号中的3个数字
var = oldAreaCode = /\((\d{3})\)/g;
var p = '(555)666-1212'.replace(oldAreaCode, '$1-');
// p 是 '555-555-1212'
```
| 美元符号序列  							| 替换对象			 		  |
| --------------------------------------| -------------------------- |
|  $$  									| $					 		 |
|  $&									| 整个匹配的文本	   			|
|  $number								| 分组捕获的文本				|
|  $‘  									| 匹配之前的文本				|
|  $’ 									| 匹配之后的文本				|

> 如果 `replaceValue` 是一个函数，此方法将对每个匹配依次调用它，并且该函数返回的字符串将被用作替换文本。传递给这个函数的第一个参数是整个被匹配的文本。第二个参数是分组`1`捕获的文本，下一个参数是分组`2`捕获的文本，以此类推：

```JavaScrip
String.methon('entityify',function(){
	var character = {
		'<' : '&lt;',
		'>' : '&gt;',
		'&' : '&amp;',
		'"' : '&quot;'
	};
	// 返回 string.entityify方法，它返回调用替换方法的结果。
	// 它的 replaceValue 函数返回在一个对象中查找一个字符串的结果。
	// 这种对象的用法通常优于 switch 语句。
	return function(){
		return this.replace(/[<>&"]/g,function(c){
			return character[c];
		})
	}
}())
```
</details>

<details>
	<summary><b>9、string.seach(regexp)</b> [点击查看]</summary>

> `seach`方法和`indexOf`方法类似，只是它接受一个正则表达是对象作为参数而不是一个字符串。如果找到匹配，它返回第一个匹配的首字符位置，如果没有找到匹配，则返回`-1`。此方法会忽略`g`标志，且没有`position`参数：

```JavaScript
var text = 'and in it he says "Any damn fool could';
var pos = text.search(/["']/) 		// pos 是 18
```
</details>

<details>
	<summary><b>10、string.slice(start,end)</b> [点击查看]</summary>

> `slice`方法复制`string`的一部分来构造一个新的字符串。如果`start`参数是负数，它将与`string.length`相加。`end`参数是可选的，并且它默认值是`string.length`。如果`end`参数是负数，那么它将与`string.length`相加。`end`参数是一个比最末一个字符的位置值还大的数。要想得到从位置`p`开始的`n`个字符，就有`string.slice(p,p+n)`。此外，请参见`string.subString`和`Array.slice`。

```JavaScript
var text = 'and in it he says "Any damn fool could';
var a = text.slice(18);
// a 是 '"Any damn fool could'
var b = text.slice(0,3);
// b 是 'and'
var c = text.slice(-5);
// c 是 'could'
var d = text.slice(19,32);
// d 是 'Any damn fool'
```
</details>

<details>
	<summary><b>11、string.splict(separator,limit)</b> [点击查看]</summary>

> `splict`方法把这个`string`分割成片段来创建一个字符串数组。可选参数`limit`可以限制被分割的片段数量。`separator`参数可以是一个字符串或者一个正则表达式。
> 如果`separator`是一个空字符串，将返回一个单字符串的数组：

```JavaScript
var digits = '0123456789';
var a = digits.split('',5);
// a 是 ['0','1','2','3','45678']
```

> 否则，此方法会在`string`中查找所有的`separator`出现的地方。分割符两边的每个单元文本会被复制到该数组中。此方法会忽略`g`标志：
```JavaScript
var ip = '192.168.1.0';
var b = ip.split('.');
// b 是 ['192','168','1','0']

var c = 'a|b|c'.split('|');
// c 是 ['','a','b','c','']

var text = 'last, first , middle';
var d = text.split(/\s*,\s*/);
// d is [
// 	'last'
// 	'first'
// 	'middle'
//]
```

>  有一些特例须特别注意。来自分组捕获的文本将会被包含在被分割后的数组中；

```JavaScript
var e = text.split(/\s*(,)\s*/);
// e is [
// 'last',
// ',',
// 'first',
// ',',
// 'middle'
//]
```

<details>	
	<summary><b>当 `separator`是一个正则表达式时，有一些`JavaScript`的实现在输出数组中会禁止空字符串：</b>[点击查看]</summary>
	
_据测试，在主流浏览器中，只有IE系统的浏览器会在输出的数组结果中禁止空字符串。_
</details>

```JavaScript
var f = '|a|b|c|'.split(/\|/);
// 在一些系统中，f 是 ['','a','b','c',''],
// 在另外一些系统中，f 是 ['a','b','c']。
```

</details>

<details>
	<summary><b>12、string.subString(start,end)</b> [点击查看]</summary>

> `subString`的方法和`slice`方法一样，只是它不能处理负数参数。没有任何理由去使用`sbuString`方法。请用`slice`替代他。
</details>

<details>
	<summary><b>13、string.toLocaleLowerCase()</b> [点击查看]</summary>

> `toLocaleLowerCase`方法返回一个新的字符串，他使用本地化的规则把这个`string`中的所有字母转换为小写格式。这个方法主要是用在土耳其语上，因为在土耳其语中 `I` 转换为 `I`,而不是 'i'。
</details>

<details>
	<summary><b>14、string.toLocaleUpperCase()</b> [点击查看]</summary>

> `toLocaleUpperCase`方法返回一个新的字符串，他使用本地化的规则把这个`string`中的所有字母转换为大写格式。这个方法主要是用在土耳其语上，因为在土耳其语中 `i` 转换为 `I`,而不是 'I'。
</details>


<details>
	<summary><b>14、string.toLowerCase()</b> [点击查看]</summary>

> `toLowerCase`方法返回一个新的字符串，这个`string`中的所有字母都被转化为小写格式。
</details>

<details>
	<summary><b>15、string.toUpperCase()</b> [点击查看]</summary>

> `toUpperCase`方法返回一个新的字符串，这个`string`中的所有字母都被转化为大写格式。
</details>

<details>
	<summary><b>16、string.fromCharCode(char……)</b> [点击查看]</summary>

> `string.fromCharCode`函数从一串数字中返回一个字符串。

```JavaScript
var a = String.fromCharCode(67,97,116);
// a 是 'Cat'
```
</details>


#### 优美的句子

* “大师牛人，宁有种乎？”
* 如果为了理解她而不得不反复阅读，请别沮丧。你的付出将会有所回报
* 编程这件事情，绝不应该在你一无所知的情况下开始
* 模棱两可的情况会给你带来风险和麻烦事
* 对于丑陋的东西，爱会闭目无视 			————威廉·莎士比亚《维罗那二绅士(The Two Gentlemen of Verona)》
* 所有的过失在未犯以前，都已定下应处的惩罚 		————威廉·莎士比亚《一报还一报(Measure for Measure)》
* 他虽疯，但却有他的一套理论 		————威廉·莎士比亚《丹麦王子、哈姆雷特的悲剧(The Tragedy of Hamlet,Prince of Denmark)》
* 好一串嘟嘟囔囔的头衔！ 		————威廉·莎士比亚《亨利六世上篇 (The First Part of Henry the Sixth)》
* 那会在一言一行中证明其糟糕。 		————威廉·莎士比亚《泰尔亲王佩里克利斯 (Pericles, Prince of Type)》
* 现在要请你告诉我，你究竟为了我哪一点坏处而开始爱上我来呢？ 		————威廉·莎士比亚《无事生非 (Much Ado About Notihing)》
* 难道我的眼睛耳朵都有了毛病？ 		————威廉·莎士比亚《错误的喜剧 (The Comedy of Errors)》
* 你这苦恼的化身，你在用表情向我们说话吗？ 		————威廉·莎士比亚《泰特斯·安德洛尼克斯 (The Tragedy of Titus Andronicus)》
* 再会吧，这宝贵的片刻和短暂的实际限制了我在情义上的真挚表示，也不能容我们畅叙衷曲，这本来是亲友久违重逢所应有的机缘；愿上帝赐给我们美好的将来，好让我们开怀畅谈！在一次告别；勇敢作战吧，祝你胜利！		————威廉·莎士比亚《查理三世 (The Tragedy of Richard the Third)》
