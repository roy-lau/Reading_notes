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
		document.writeln("move disc " + disc + " from " + src + " to " + dst); //最大盘从 src 移到 dst
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
typeof arr   // "object"
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

* Array.concat(item……)

> concat 方法返回一个新数组，它包含Array的浅复制(shallow copy) 并将一个或多个参数item附加在其后。如果参数item是一个数组，那么它的每个元素会被分别添加。此外，详情参见Array.push(item……)方法。

```JavaScript
var a = ["a","b","c"];
var b = ["x","y","z"];
var c = a.concat(b,true)  	// c 是 ["a","b","c","x","y","z",true]
```
* Array.join(separator)

> join方法把一个Array构造成一个字符串。他将Array中的每个元素构造成一个字符串，并用一个separator(分离器)为分隔符把它们连接在一起。默认的separator(分离器)是 `,` 。为了实现无间隔连接，我们可以用空字符串作为separator.
> 如果你想把大量的片段组装成一个字符串，把这些片段放到一个数组中并用 `join` 方法连接她们通常比用`+`元素运算符连接这些片段要快。

```JavaScript
var a = ["a","b","c"];
a.push("b");
var c = a.join("") 	// c 是 "abcd"
```
* Array.pop()

> `pop`和`push`方法使数组`Array`像堆栈(stack)一样工作。`pop`方法移除`Array`中的最后一个元素并返回该元素。如果该`Array`是空的，他会返回`undefined`
```JavaScript
var a = ["a","b","c","d"];
var c = a.pop() 	// a 是 ["a","b","c"] && c 是 "d"
```
> `pop` 可以像这样实现：
```JavaScript 
Array.method("pop",function(){
	return this.splice(this.length - 1)[0];
	})
```

* Array.push(item……)

> `push` 方法将一个或多个参数`item`附件到一个数组的尾部。不像`concat`方法那样，它会修改该数组`Array`,如果参数`item`是一个数组，它会将参数数组作为单个元素整个添加到数组中。它返回这个数组`Array`的新长度值。
```JavaScript
var a = ["a","b","c"];
var b = ["x","y","z"];
var c = a.push(b,true);
// a 是 ["a","b","c",["x","y","z"],true]
// c 是 5;
```
> `psuh` 可以像这样实现：
Array.method("push",function(){
	this.splice.apply(
			this,
			[this.length,0].concat(Array.prototype.slice.apply(arguments))
		);
		return this.length;
});

* Array.reverse()
`reverse`方法反转`Array`中的元素的顺序。它返回当前的Array；

```JavaScript
var a = ["a","b","c"];
var b = a.reverse();
// a和b都是 ["c","b","a"]

* Array.shift()

#### 优美的句子

* “大师牛人，宁有种乎？”
* 如果为了理解她而不得不反复阅读，请别沮丧。你的付出将会有所回报
* 编程这件事情，绝不应该在你一无所知的情况下开始
* 模棱两可的情况会给你带来风险和麻烦事
* 对于丑陋的东西，爱会闭目无视 			————威廉·莎士比亚《维罗那二绅士(The Two Gentlemen of Verona)》
* 所有的过失在未犯以前，都已定下应处的惩罚 		————威廉·莎士比亚《一报还一报(Measure for Measure)》
* 他虽疯，但却有他的一套理论 		————威廉·莎士比亚《丹麦王子、哈姆雷特的悲剧(The Tragedy of Hamlet,Prince of Denmark)》
