# CSS相关

## CSS单位（尺寸）
| 单位|描述 |
|-|-|
|in|英寸|
|cm|厘米|
|mm|毫米|
|em|当前字体倍数|
|ex|当前字体半倍|
|pt|磅|
|pc|12点|
|px|像素|

## CSS定位
* static
元素框正常生成。块级元素生成一个矩形框，作为文档流的一部分，行内元素则会创建一个或多个行框，置于其父元素中。
* relative
元素框偏移某个距离。元素仍保持其未定位前的形状，它原本所占的空间仍保留。
* absolute
元素框从文档流完全删除，并相对于其包含块定位。包含块可能是文档中的另一个元素或者是初始包含块。元素原先在正常文档流中所占的空间会关闭，就好像元素原来不存在一样。元素定位后生成一个块级框，而不论原来它在正常流中生成何种类型的框。
* fixed
元素框的表现类似于将 position 设置为 absolute，不过其包含块是视窗本身。

## CSS多列布局
```CSS
div {
  -moz-column-count:3; 	/* Firefox */
  -webkit-column-count:3; /* Safari 和 Chrome */
  column-count:3;
}
```