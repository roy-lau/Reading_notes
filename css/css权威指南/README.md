
## CSS 权威指南

> 层叠样式表(Cascading Style Sheets, CSS) 的功能非常强大，可以影响一个或一组文档的表现。显然，如果不存在某种文档，CSS基本毫无用处，因为这样一来他将没有要表现的内容。当然，“文档”的定义相当宽泛。

### 1、 CSS和文档

**元素：**

- 替换元素： 如 `img`

- 非替换元素 : 如 `span`、段落、标题、表单元格、列表和XHTML

- 块级元素 ： 如 `p div`,块级元素生成一个元素框，(默认地)它会填充其父元素的内容区。替换元素可以是块级元素，不过通常都不是。

- 行内元素 ： 如 `a strong em`,行内元素在一个文本行内生成元素框，而不会打断这行文本。

|# 	| display 	|
|----|:-----------------------------:|
| 值 | `none`、 `inline`、 `block`、 `inline-block`、 `list-item`、 `run-in`、 `table`、 `inline-table`、 `table-row-group`、 `table-header-group`、 `table-footer-group`、 `table-row`、 `table-column-group`、 `table-column`、 `table-cell`、 `table-caption`、 `inherit` |
| 初始值 | inline 	|
| 应用于 | 所有元素 	|
| 继承性 | 无		|

**link标签 :**

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

**style元素:**

```html
<style type="text/css"></style>
```

`style` 一定要使用 `type` 属性;对于 `CSS` 文档,正确的 `type` 属值是 `"text/css"`,这与 `link` 元素类似。
`style` 元素始终要以 `<style type="text/css"></style>`开头，如上例所示。其后可以有一个或多个样式，最后以一个结束 `</style>`标记结尾。还可以为 `style` 元素指定一个 `media` 属性，其可取值与之前的 `media` 属性值相同。

开始和结束 style 标记之间的样式称为文档样式表(`document style sheet`),或嵌套样式表(`embedded style sheet`), 因为这个样式表嵌套在文档中。其中可能包含应用到文档的多个样式，还可以使用`@import` 指令包含多个外部样式表链接。

**@import指令**

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

**`CSS` 注释**

```css
/* 单行注释 */

/* 多行
	注释 */
```

**内联样式**

`style` 属性语法：

```html
<p style="color: gray;">这是一段内联样式</p>
```

_此处 “inline” 不能理解为“行内”，而应当是“内联”，有“内部自带”的意思。_

_注意：_ 一个内联 `style` 属性只能放一个声明块，而不能放整个样式表。因此，不能在 `style` 属性中放 `@import`，也不能包含完整的规则。 `style` 属性的值中只能是规则中出现的大括号之间的部分。**style属性通常不推荐使用，XHTML1.1已将将其标注为不建议使用，XML也不太可能使用这个属性。因为他会抵消一些CSS的优点。**

**小结**

利用 CSS，可能会改变用户代理表现元素的方式。可以使用 `display` 属性采用基本方法来显示，也可以将样式表与文档关联，以另一种不同的方式表现。用户不会知道这是通过外部样式表还是嵌套样式表完成的（甚至有可能是利用一个内联样式做到的）。外部样式表真正的意义在于，她允许创作人员将网站的所有表现信息放在一个位置，将所有文档指向这个位置。这不仅使用网络的更新和维护相当容易，还有助于节省带宽，因为文档中去除了所有表现信息。
为了充分利用 CSS 的强大功能，创作人员需要了解如何将一组样式与文档中的元素相关联。要全面地理解 CSS 如何做到这些，创作人员则需要深入地掌握 CSS 以何种方式选择文档中要应用样式的部分。


### 2、选择器

**基本规则：**

将所有`h2`标题变为银色
```css
h2 {color: silver}
```

**规则结构：**

每个 css 规则都有两个基本部分： **选择器(selector)** 和 **声明块(declaration block)** 。声明块又一个或多个 **声明(declaration)** 组成，每个声明则是一个属性——值对(proerty-value)。每个样式表由一系列规则组成。下图显示了规则的各个部分。

<img src="imgs/css规则结构.png" alt="css规则结构图解" />

如上图所示，选择器定义了将影响文档中的那些部分。上图中选择了 `h1` 元素。如果选择器是 `p` ，怎会选择所有 `p` (段落)元素。

**元素选择器：**

将 html 做为 css 的选择器来使用，称为 **元素选择器**

