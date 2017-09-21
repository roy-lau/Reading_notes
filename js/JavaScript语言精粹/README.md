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
	<summary><b>1、Number.toFixed(fractionDigits)</b> [点击查看]</summary>
> `toFixed`方法把这个`number`转换成为一个十进制数形成的字符串。可选参数`fractionDigits`控制其小数点后的数字位数。它的值必须在0和20之间。默认为0；

```JavaScript
document.writeln(Math.PI.toFixed(0));
document.writeln(match.PI.toFixed(2));
document.writeln(match.PI.toFixed(7));
document.writeln(match.PI.toFixed(16));
document.writeln(match.PI.toFixed());
// 结果
3
3.14
3.1415927
3.1415926535897930
3
```
</details>

<details>
	<summary><b>1、Number.toString(fractionDigits)</b> [点击查看]</summary>
> `toString`方法把这个`number`转换成为一个十进制数形成的字符串。可选参数`fractionDigits`控制其小数点后的数字位数。它的值必须在0和20之间。默认为0；

```JavaScript
document.writeln(Math.PI.toString(0));
document.writeln(match.PI.toString(2));
document.writeln(match.PI.toString(7));
document.writeln(match.PI.toString(16));
document.writeln(match.PI.toString());
// 结果
3
3.14
3.1415927
3.1415926535897930
3
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
