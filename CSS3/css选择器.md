.class  .intro  选择 class="intro" 的所有元素。 1
#id #firstname  选择 id="firstname" 的所有元素。    1
*   *   选择所有元素。 2
element p   选择所有 <p> 元素。    1
element,element div,p   选择所有 <div> 元素和所有 <p> 元素。    1
element element div p   选择 <div> 元素内部的所有 <p> 元素。    1
element>element div>p   选择父元素为 <div> 元素的所有 <p> 元素。  2
element+element div+p   div之后的兄弟p   2
[attribute] [target]    选择带有 target 属性所有元素。 2
[attribute=value]   [target=_blank] 选择 target="_blank" 的所有元素。   2
[attribute~=value]  [title~=flower] 选择 title 属性包含单词 "flower" 的所有元素。 2
[attribute|=value]  [lang|=en]  选择 lang 属性值以 "en" 开头的所有元素。  2
:link   a:link  选择所有未被访问的链接。    1
:visited    a:visited   选择所有已被访问的链接。    1
:active a:active    选择活动链接。 1
:hover  a:hover 选择鼠标指针位于其上的链接。  1
:focus  input:focus 选择获得焦点的 input 元素。   2
:first-letter   p:first-letter  选择每个 <p> 元素的首字母。    1
:first-line p:first-line    选择每个 <p> 元素的首行。 1
:first-child    p:first-child   选择属于父元素的第一个子元素的每个 <p> 元素。   2
:before p:before    在每个 <p> 元素的内容之前插入内容。    2
:after  p:after 在每个 <p> 元素的内容之后插入内容。    2
:lang(language) p:lang(it)  选择带有以 "it" 开头的 lang 属性值的每个 <p> 元素。  2
element1~element2   p~ul    选择前面有 <p> 元素的每个 <ul> 元素。    3
[attribute^=value]  a[src^="https"] 选择其 src 属性值以 "https" 开头的每个 <a> 元素。  3
[attribute$=value]  a[src$=".pdf"]  选择其 src 属性以 ".pdf" 结尾的所有 <a> 元素。    3
[attribute*=value]  a[src*="abc"]   选择其 src 属性中包含 "abc" 子串的每个 <a> 元素。   3
