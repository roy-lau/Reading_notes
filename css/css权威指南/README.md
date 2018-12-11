
# CSS 权威指南

> 层叠样式表(Cascading Style Sheets, CSS) 的功能非常强大，可以影响一个或一组文档的表现。显然，如果不存在某种文档，CSS基本毫无用处，因为这样一来他将没有要表现的内容。当然，“文档”的定义相当宽泛。

##  1、 CSS和文档

### 元素

- 替换元素： 如 `img`

- 非替换元素 : 如 `span`、段落、标题、表单元格、列表和XHTML

- 块级元素 ： 如 `p div`,块级元素生成一个元素框，(默认地)它会填充其父元素的内容区。替换元素可以是块级元素，不过通常都不是。

- 行内元素 ： 如 `a strong em`,行内元素在一个文本行内生成元素框，而不会打断这行文本。

|	#########  | display 				|
|------------|:-----------------------------:|
| 值 				 | `none`、 `inline`、 `block`、 `inline-block`、 `list-item`、 `run-in`、 `table`、 `inline-table`、 `table-row-group`、 `table-header-group`、 `table-footer-group`、 `table-row`、 `table-column-group`、 `table-column`、 `table-cell`、 `table-caption`、 `inherit` |
| 初始值 		| inline 			 |
| 应用于 		| 所有元素 		  |
| 继承性 		| 无					 |

### link标签

```html
<link rel="stylesheet" type="text/css" href="sheet1.css" media="all" />
```

> 加载外部样式表，`link` 必须放在 `head` 元素中，但不能放在其他元素内部(如： title)。 `.css`扩展名可以不加，但是有些老的浏览器无法通过识别 `link` 元素中 `text/css` 类型来加载 css文件。不过这个问题可以通过改变服务器的配置文件来修正。

- 属性
	- rel: 关系(relation),一般为 `stylesheet`。
	- type: 描述了使用 `link` 标记加载的数据类型, 一般为 `text/css`。
	- href: 可以是样式表的 `绝对URL` 也可以是 `相对URL`。
	- median：
		- all： 用于所有表现的媒体
		- aural： 用于语音合成器、屏幕阅读器和文档的其他声音表现。
		- braille： 用 Braille 设备表现文档时使用。
		- embossed： 用 Braille 打印设备打印时使用。
		- handheld： 用于手持设备,如个人数字助理或支持 web 的蜂窝电话。
		- print： 为视力正常的用户打印文档时使用，另外还会在显示文档的“打印预览”时使用。
		- projection： 用于投影媒体，如发表演讲时显示幻灯片的数字投影仪。
		- screen： 在屏幕媒体（如桌面计算机监视器）中表现文档时使用。在这种系统上运行的所有 web 浏览器都是屏幕媒体用户代理。
		- tty： 在固定间距环境（如电传打字机）中显示文档时使用。
		- tv： 在电视上显示文档时使用。

如果样式表支持多个媒体，各个媒体之间用逗号分隔。例如：

```html
<link rel="stylesheet" type="text/css" href="visual-sheet.css" media="screen,projection" />
```

一个文档可能关联多个链接样式表。文档最初显示时只会使用`rel`为`stylesheet`的`link`标记。浏览器会加载如下两个样式表，合并他们的规则，并将其全部应用于文档。

```html
<link rel="stylesheet" type="text/css" href="basic.css" />
<link rel="stylesheet" type="text/css" href="splash.css" />
```

- 候选样式表

> 还可以定义候选样式表（alternate style sheet）。将 `rel` 属性的值置为 `alternate stylesheet` ，就可以定义候选样式表，只有在用户选择这个样式表时才会用于文档表现。**早期功能，现在大量浏览器已不支持**

不同的设备使用不同的元素

```html
<link rel="stylesheet" type="text/css" href="sheet1.css" media="screen" title="Default" />
<link rel="stylesheet" type="text/css" href="print-sheet1.css" media="print" title="Default" />
<link rel="alternate stylesheet" type="text/css" href="bigtext.css" media="screen" title="Big Text" />
<link rel="alternate stylesheet" type="text/css" href="print-bigtext.css" media="print" title="Big Text" />
```

### style元素

```html
<style type="text/css"></style>
```

`style` 一定要使用 `type` 属性;对于 `CSS` 文档,正确的 `type` 属值是 `"text/css"`,这与 `link` 元素类似。
`style` 元素始终要以 `<style type="text/css"></style>`开头，如上例所示。其后可以有一个或多个样式，最后以一个结束 `</style>`标记结尾。还可以为 `style` 元素指定一个 `media` 属性，其可取值与之前的 `media` 属性值相同。

开始和结束 style 标记之间的样式称为文档样式表(`document style sheet`),或嵌套样式表(`embedded style sheet`), 因为这个样式表嵌套在文档中。其中可能包含应用到文档的多个样式，还可以使用`@import` 指令包含多个外部样式表链接。

### @import指令

常见用例：

```html
<style type="text/css">
	@import url(style.css); /* @import comes first */
	@import url(sheet2.css);
	@import url(blueworld.css);
	@import url(zany.css);
	h1 {color: gray;}
</style>
```

根据不同的媒体应用不同的样式：

```html
<style type="text/css">
	@import url(sheet2.css) all;
	@import url(blueworld.css) screen;
	@import url(zany.css) projection print;
</style>
```

`@import` 加载外部样式表:

```css
@import url(http://example.org/library/layout.css);
```

_注意：_ `@import` 指令出现在样式表的开头，`CSS` 要求 `@import` 指令出现在样式表中的其他规则之前。如果一个 `@import` 出现在其他规则（如 `body {color: red;}`）之后，**兼容用户代理会将其忽略**。

_警告：_ `Windows` 平台的 `Internet explorer`不会忽略任何 `@import`指令，甚至出现在其他规则之后的 `@import`也不会忽略。

### `CSS` 注释

```css
/* 单行注释 */

/* 多行
	注释 */
```

### 内联样式

`style` 属性语法：

```html
<p style="color: gray;">这是一段内联样式</p>
```

_此处 “inline” 不能理解为“行内”，而应当是“内联”，有“内部自带”的意思。_

_注意：_ 一个内联 `style` 属性只能放一个声明块，而不能放整个样式表。因此，不能在 `style` 属性中放 `@import`，也不能包含完整的规则。 `style` 属性的值中只能是规则中出现的大括号之间的部分。**style属性通常不推荐使用，XHTML1.1已将将其标注为不建议使用，XML也不太可能使用这个属性。因为他会抵消一些CSS的优点。**

### 小结

利用 CSS，可能会改变用户代理表现元素的方式。可以使用 `display` 属性采用基本方法来显示，也可以将样式表与文档关联，以另一种不同的方式表现。用户不会知道这是通过外部样式表还是嵌套样式表完成的（甚至有可能是利用一个内联样式做到的）。外部样式表真正的意义在于，她允许创作人员将网站的所有表现信息放在一个位置，将所有文档指向这个位置。这不仅使用网络的更新和维护相当容易，还有助于节省带宽，因为文档中去除了所有表现信息。
为了充分利用 CSS 的强大功能，创作人员需要了解如何将一组样式与文档中的元素相关联。要全面地理解 CSS 如何做到这些，创作人员则需要深入地掌握 CSS 以何种方式选择文档中要应用样式的部分。


## 2、选择器

### 基本规则

将所有`h2`标题变为银色
```css
h2 {color: silver}
```

### 规则结构

每个 css 规则都有两个基本部分： **选择器(selector)** 和 **声明块(declaration block)** 。声明块又一个或多个 **声明(declaration)** 组成，每个声明则是一个属性——值对(proerty-value)。每个样式表由一系列规则组成。下图显示了规则的各个部分。

<img src="imgs/css规则结构.png" alt="css规则结构图解" />

如上图所示，选择器定义了将影响文档中的那些部分。上图中选择了 `h1` 元素。如果选择器是 `p` ，怎会选择所有 `p` (段落)元素。

### 元素选择器

将 html 标签元素做为 css 的选择器来使用，称为 **元素选择器**

```css
html{color: black;}
h1 {color: gray:}
h2 {color: silver;}
```

### 声明和关键字

如果一个属性的值可以取多个关键字，在这种情况下，关键字通常由空格分隔。并不是所有的属性都能接受多个关键字，不过确实有许多属性是这样的，例如 `font` 属性。假设腰围段落文本定义中等大小的 `Heletica` 字体，写法如下：

```css
p { font: medium Heletica;}
```

注意 `medium` 和 `Helvetica` 之间的空格，`medium` 和 `Helvetica`  都是关键字（`medium` 指定了字体的大小， `Helvetica` 是字体名）。两个关键字之间的空格使用户代理能够区分这两个关键字，并适当地应用。后面的分号指示声明结束。
用空格分隔的这些词称为关键字，这是因别他们加载一起构成了当前属性的值。

<hr />

__注意 :__  CSS 关键字往往由空格分隔，只用一种情况例外，在 CSS 的 `font` 属性中，只有一整情况可以使用斜线 **/** 来分隔两个关键字。如下例：

```css
h2 {font: large/150% sans-serif;}
```
斜线分隔了用来设置元素的字体大小和行高的两个关键字，只用在这里才允许 `font` 声明中出现斜线。 `font` 允许的所有其他关键字都用空格分隔。
<hr />

### 分组

- 选择器分组

将多个元素设置相同的css样式，最直接的方式可能是这样：

```css
h1 {color: purple;}
h2 {color: purple;}
h3 {color: purple;}
h4 {color: purple;}
h5 {color: purple;}
h6 {color: purple;}
```

但是，使用 **分组选择器** 就简单方便多了，如下：

```css
h1, h2, h3, h4, h5, h6 {color: purple;}
```

- 通配选择器

css2 引入了一种新的选择器，称为 **通配选择器(uninersal selector)** ,显示为一个星号。这个选择器可以与任何元素匹配，就像一个通配符。例如，让一个文档中的每一个元素都为红色，可以写为如下规则：

```css
* {color: red;}
```

- 声明分组

假如您需要为一个元素设置浅绿色背景，18像素的 `Helvetica` 字体，文本颜色为紫色。那您就可以使用 **声明分组** 来更方便的的书写样式了：

```CSS
p {
	font: 18px Helvetica;
	color: purple;
	background: aqua;
}
```

__注意 :__ 声明块的最后一定要使用分号结尾，如果缺少分号就会出现各种意想不到的错误。


- 结合 选择器和声明的分组

```CSS
h1, h2, h3, h4, h5, h6 {
	color: purple;
	background: white;
	padding: 0.5em;
	border: 1px solid black;
	font-family: Charcoal, sans-serif;
	}
```

### 类选择器和ID选择器

> 除了指示文档元素的选择器外，还有另外两种类型的选择器： 类选择器(class selector) 和 ID 选择器(ID selector)，他们允许以一种独立于文档元素的方式来指定元素样式。

- 类选择器：

要应用样式而不考虑具体涉及的元素，最常用的方法就是使用类选择器。不过，在使用类选择器之前，需要秀给具体的文档标记，以便类选择器正常工作，驶入以下 class 属性；

```HTML
<p class="waring">这是一段警告文本</p>
<p>这是一段<span class="waring">警告</span>文本</p>
```

对于HTML文档，可以使用一种很简洁的记法，即类名前有一个点号( ```.``` )。

```CSS
.waring {font-weight: bold; color: red;}
```

- ID 选择器：

ID 选择器与 类选择器类似，ID选择器前面有一个 `#` 号 —— 也成为棋盘符。

```HTML
<p id="text-bold">这是一段加粗的文本</p>
```

```CSS
#text-blod { font-weight: bold; }
```

- 类选择器还是ID选择器 ?
	1. ID选择器具有唯一性，使用过一次，别的地方就不能使用了（实际上浏览器并没有检查ID选择器的唯一性）
	2. 不同于类选择器 ID选择器不能结合使用。因为ID选择器不允许有空格分隔的次词列表。
	3. class 名与 ID名之间的另一个区别是，如果你想确定一个给定元素应用那些样式，ID能包含更多含义。
	4. 类和ID选择器都是可能区分大小写的，这取决于文档语言。HTML和XHTML将类和ID定义为区分大小写，所以ID值的大小写必须和文档中的值相对应。( _一些老旧的浏览器可能会不区分类和ID选择器的大小写_ )

### 属性选择器

> 对于类选择器和ID选择器，实际上只能选择属性的值。CSS2 引入了属性选择器( `attribute selector` ), 可以根据元素的数据及数据值来选择元素。  共有四种类型的属性选择器

- 简单属性选择器：

选择某个属性的元素，而不论属性值是什么。可以使用一个简单的属性选择器。例如，要选择有 `class` 属性的所有 `h1` 元素，使其文本为银色，可以写作：

```CSS
h1[cass]{
	color: silver;
}
```

**对所有带 `alt` 属性的图像应用某种样式：**

```CSS
img[alt] {
	border: 3px solid red;
}
```

**把包含标题( `title` )信息的元素变为粗体显示：**

```CSS
*[title] {
	font-weight: bold;
}
```

**根据多个属性进行选择，只需将属性选择器连在一起即可，如：**

```CSS
a[herf][title] {
	font-weight: bold;
}
```

- 根据具体属性值选择：

除了选择某些属性的元素，还可以进一步缩小范围，只选择特定属性的元素。

```CSS
a[herf="https://www.github.com/roy-lau"] {
	font-weight: bold;
}
```

与属性选择器类似，可以把多个属性-值连在一起选择一个文档。

```CSS
a[herf="https://www.w3c.org/"][title="W3C Home"] {
	font-size: 200%;
}
```

**空格问题**

```HTML
<p class="urgent warning">这是一段警告文本！</p>
```

根据具体属性值来选择这个元素，必须写作：

```CSS
p[class="urgent warning"] {
	font-weight: bold;
}
```

下面这两种方式是错误的：

```CSS
p[class="urgent"] {
	font-weight: bold;
}
p[class="warning"] {
	font-weight: bold;
}
```

- 根据部分属性值选择：

如果属性能接受词列表(词之间空格分隔)，可以根据其中任意一个词进行选择。在HTML中，这方面最经典的例子就是 `class` 属性，他能接受一个或多个词做为其属性值。下面是实例文本：

```HTMl
<p class="urgent warning">这是一段文本。</p>
```

假如想选择 `class` 属性为 `warning` 的元素，可以用一个元素选择器做到：

```CSS
p[class~="warning"] {
	font-weight: bold;
}
```

部分值元素选择器不仅可以用于 `class` 也可以用于别的元素,如：

```CSS
img[title="FIgure"] {
	border: 1px solid gray;
}
```

子串匹配选择值：

|类型 							 | 描述
|-------------------|-------------------------------------
| `[foo^="bar"]`		| 选择 `foo` 属性值 以 `bar` 开头的所有元素
| `[foo$="bar"]`		| 选择 `foo` 属性值 以 `bar` 结尾的所有元素
| `[foo*="bar"]`		| 选择 `foo` 属性值中包含子串 `bar` 的所有元素

用例：

```HTML
<span class="barren rocky"> 银色 粗体 </span>
<span class="cloudy barren"> 斜体 </span>
<span class="life-bearing cloudy"> 斜体 粗体 </span>
```
```CSS
span[class*="cloud"] { font-style: italic; }
span[class^="bar"] { background: silver; }
span[class$="y"] { font-weight: bold; }
```

- 特定属性选择类型:

```CSS
*[lang|="en"] { color: white; }
```

这个规则会匹配等于 `en` 或以 `en` 开头的所有元素。因此，以下元素中前三个元素会被选中，而后两个不会被选中。

```HTML
<h1 lang="en"> Hello </h1>
<p lang="en-us"> Gettings </p>
<div lang="en-au"> G'day </div>
<p lang="fr"> Bonjour </p>
<h4 lang="cy-ea"> Jrooana </h4>
```

一般来说， `[att|="val"]` 可以用于任何属性及值，假设一个 HTML 文档中国有一些列图片，其中每个图片的文件名形如 `figure-1.gif` 和 `figure-2.jpg`。就可以选择一下选择器匹配所有这些图像：

```CSS
img[src|="figure"] {border: 1px solid gray;}
```

### 使用文档结构

> CSS功能很强大，因为他要通过 HTML 的结构来确定适当的样式，并确定如何应用这些样式。还不仅如此，因为这说明使用文档结构是CSS确定和应用样式的唯一途径，确定以何种方式项文档应用样式时，结构还承担着重要的角色。下面先来讨论结构，然后在介绍些功能刚强大的选择器。

- 理解父子关系

要理解选择器和文档的关系，需要先分析文档结构。考虑下面非常简单的HTML文档：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <base href="http://www.meerkat.web/" />
    <title>文档关系</title>
</head>

<body>
    <h1>Meerkat<em>Contral</em></h1>
    <p>Welcome to Meerkat <em>Central</em>, the <strong>best meerkat web site on <a href="inet.html">the <em>entire</em> Internet</a></strong>!</p>
    <ul>
        <li>We offer:
            <ul>
                <li><strong>Detailed information</strong>on how to adopt a meerkat</li>
                <li>Tips for living with a meerkat</li>
                <li><em>Fun</em>thing to do with a meerkat, including:</li>
                <ol>
                    <li>Playing fetch</li>
                    <li>Digging for food</li>
                    <li>Hide and seek</li>
                </ol>
						</ul>
        </li>
        <li>... and so much more!</li>
    </ul>
    <p>Questions? <a href="mailto:suricate@meerkat.web">Contact us!</a></p>
</body>

</html>
```

**css之所以强大，在于元素之间存在父子关系。** HTML文档以一种层次结构为基础（实际上，大多数结构化文档都是如此），可以从文档的“树”视图中了解到这种层次结构。在这个层次结构中，每个元素在整个文档结构中都有自己的一个位置。文档中每个元素要么是某个元素的父元素，要么是某个元素的父元素。而且通常兼而有之（即同时作为元素的父元素，和另一个元素的子元素）。

<img src="imgs/css-dom-tree.png" alt="css文档结构" />

- 后代选择器

理解结构模型后，第一个好处就是定义后代选择器（descendant selector，也成为包含选择器）或者上下文选择器（contextual selector）。定义后代选择器是来创建一些规则，它们仅在某些结构中起作用，而另外一些结构中不起作用。举例来说，假设你希望只对 `h1` 元素继承的那些 `em` 元素应用样式。可以在 `h1` 中找到每个 `em` 元素上放一个 `class` 属性，但这就想使用 font 标记一样费工夫。显然，更高效的做法是声明一些规则，只与 h1 元素包含的 `em` 元素匹配。

为此，可以写作：

```CSS
h1 em { color: gray;}
```
这个规则会把 `h1` 后代的 `em` 元素的文本变成灰色、其他 `em` 文本（如段落或块引用中的 em）则不会被这个规则选中。

后代元素选择器有一个常被忽略的方面，即两个元素之间的层次间隔可以是无限的。例如，如果写作 `ul em` ,这种语法就会选择继承 `ul` 下的所有 `em` 元素，而不论 `em` 元素嵌套有多深。因此， `ul em` 将会选择以下标记中的 `em` 元素:

```HTML
<ul>
	<li>List Item 1
		<ol>
			<li>List Item 1-1</li>
			<li>List Item 1-2</li>
			<li>List Item 1-3
				<ol>
					<li>List Item 1-3-1</li>
					<li>List Item <em>1-3-2</em></li>
					<li>List Item 1-3-3</li>
				</ol>
			</li>
			<li>List Item 1-4</li>
		</ol>
	</li>
</ul>
```

- 选择子元素

某些情况下不想选择任意的后代元素，而是想缩小范围。值选择另一个元素的子元素。例如，你可以选择只作为 `h1`元素的子元素(而不是后代元素)的 `strong` 元素。为此,可以使用子结合符,即大于号 `>`

```CSS
h1 > strong { color: red; }
```
这个规则会把第一个 `h1` 下的 `strong` 变为红色，而第二个出现的 `strong` 元素不受影响。

- 选择相邻的兄弟元素

要去除紧接在一个 `h1` 元素后出现的段落（`p`）上边距，可以写作：

```CSS
h1 + p { margin-top: 0;}
```
这个选择器读作 “选择紧接在一个 `h1` 元素后出现的段落, `h1` 要与 `p` 元素拥有共同的父元素”

为了形象的展示选择器是如何工作的,最容易的办法是再来考虑一个文档树的片段。
<img src="imgs/css-dom-tree-fragment.png" alt="文档树的片段" />
想要正常的工作,CSS要求两个元素按“源顺序”出现。在前面例子中， ol 元素后面有一个 ul 元素。因此可以用 `ol+ul` 选择第二个元素,但这个语法无法选择第一个元素。想要与 `ul+ol` 匹配, 有序类别必须紧跟在无序列表后面。
另外，两个元素之间的文本内容不会影响相邻兄弟结合符起作用。上图与下面代码片段相同：

```HTML
<div>
	<ol>
		<li> List item 1 </li>
		<li> List item 2 </li>
		<li> List item 3 </li>
	</ol>这是一些文本，是'div'的一部分
	<ul>
		<li> a list item </li>
		<li> another list item </li>
		<li> yet another list item </li>
	</ul>
</div>
```
尽管两个列表间多了一行文本,不过还是可以用选择器 `ol+ul` 来匹配第二个列表。这是因为中间文本并不包含在兄弟元素中，而只是父元素 div 的一部分,不过也可以这么写：
```CSS
l + p + ul
```

相邻兄弟选择器还可以结合其他结合符:
```CSS
html > body table + ul {margin-top: 1.5em;}
```
这个选择器解释为“选择一个紧挨在 `table` 后出现的所有兄弟 `ul` 元素,改 `table` 元素包含在一个 `body` 元素中,  `body` 元素本身是 `HTML` 元素的子元素”

_警告：windows平台的ie6之前的浏览器不支持子选择器和相邻元素选择器，ie7 则对二者提供了支持。_

- #### 伪类和伪元素

> 伪类选择器和伪元素选择器可以在文档中不一定具体存在的结构指定样式,或者为某些元素(甚至是元素本身)的状态的幻象类所指定样式,换句话说：会根据另外某种条件而非文档结构，向文档中的某部分添加样式。而且无法通过研究文档的标记准确地推断采用何种方式应用样式。

> 听上去好像在随机应用样式, 不过并非如此。事实上这是根据某种无法提前预测的暂时条件来应用样式。

  - 1、伪类选择器

	CSS 定义了伪类，使已使用的锚点有一个 `visited`, 用法如下：
	```CSS
	a:visited{ color: red; }
	```

	已访问页面的锚都会为红色，不必为任何锚点加 `visited` 属性。 注意规则中的冒号 `:` 。分隔 `a` 和 `visited` 是伪类和伪元素的 “名片”。所有伪类和伪元素关键字前面都有一个冒号。

	* 链接伪类

	| 伪类名		 		| 描述
	|---------------|----------
	| 	`:link`			| 指示做为超链接（既有一个 `herf` 属性）,并指向一个未访问地址的所有锚。_注意:有些浏览器可能会不正确的将 `:link` 解释为任何超链接,包括已访问的和未访问的超链接_
	| 	`:visited`	| 指示做为已访问地址超链接的所有锚

	表中的第一个伪类看起来有些多余。毕竟,如果一个锚点尚未访问过,那么他肯定是为访问的链接。如果这样我们需要的应该是：

	```CSS
	a{color: blue;} /* 所有的a标签，包括没有href链接的*/
	a:visited{color: red;}
	```
	尽管这种个是看上是合理的。但是，第一个规则不仅应用到未访问的链接,还会应用到一下锚点：
	```HTML
	<a name="section4"> 4. The Lives of Meerkats </a>
	```
	上面相对应的文本也会变成蓝色, `a` 元素与规则 `a { color: blue; }` 匹配。所以为了避免将链接样式应用到目标锚，要使用 `:link` 伪类。
	```CSS
	a:link{color: blue;} /* 未访问的链接是蓝色的 */
	a:visited{color: red;} /* 访问的链接是红色的 */
	```
	* 动态伪类
	> css2.1 定义了3个动态伪类，他们可以根据用户的行为改变文档的外观。这种动态伪类以前总用来设置超链接样式，不过他们还有很多其他用途，见下表：

	| 伪类名 			| 描述
	|-------------|---------
	| 	`:focus`		| 指示当前输入焦点的元素，也就是说，可以使用键盘输入或者以某种方式激活的元素。
	| 	`:hover`		|	指示鼠标停留在哪个元素上，例如，鼠标可能停留在一个超链接上,    `:hover` 就会指示这个超链接
	| 	`:active`		| 指示用户被输入激活的元素，例如，鼠标停留在一个超链接上时，如果用户点击鼠标，就会激活这个超链接， `:active` 将指示这个超链接。

	常用伪类实例：
	```CSS
	a:link{color: navy;}
	a:visited:{color: gray;}
	a:hover{color: red;}
	a:active{color: yellow;}
	```
	**注意**： 伪类顺序很重要，这一点最初可能不太明显。通常建议是“`link -> visited -> hover -> active`”,不过现在已经改为“`link -> visited -> focus-> hover -> active`”

	* 选择一个子元素
