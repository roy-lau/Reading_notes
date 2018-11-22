
### CSS 权威指南

> 层叠样式表(Cascading Style Sheets, CSS) 的功能非常强大，可以影响一个或一组文档的表现。显然，如果不存在某种文档，CSS基本毫无用处，因为这样一来他将没有要表现的内容。当然，“文档”的定义相当宽泛。

#### 1、 CSS和文档

**元素：**

- 替换元素： 如 `img`

- 非替换元素 : 如 `span`、段落、标题、表单元格、列表和XHTML

- 块级元素 ： 如 `p div`,块级元素生成一个元素框，(默认地)它会填充其父元素的内容区。替换元素可以是块级元素，不过通常都不是。

- 行内元素 ： 如 `a strong em`,行内元素在一个文本行内生成元素框，而不会打断这行文本。

||display|
||:-----------------------------:|
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