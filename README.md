# CSS 总结

## 块级元素的特点

- 总是从新行开始
- 高度，行高，外边距和内边距都可以控制
- 宽度默认是容器的100%
- 可以容纳内联元素的其他块元素

## 行内元素的特点

行内元素不占有独立的区域，仅仅靠自身的字体的大小和图像尺寸来支持结构，一般不可以设置宽度、高度、对齐等属性，常用于控制页面中文本的样式。

常见的行内元素有：

- `<a></a>`
- `<strong></strong>`
- `<b></b>`
- `<em></em>`
- `<span></span>`

等等


- 和相邻行内元素在一行上
- 宽高无效，但水平方向的`padding` 和 `margin` 可以设置，垂直方向的无效
- 默认宽度就是它本身内容的宽度
- 行内元素只能容纳文本或其他行内元素（`a` 特殊） 

注意：

1. 只有文字才能组成段落，因此 `<p></p>` 里面不能放块级元素，同理还有这些标签`h1`,`h2`,`h3`,`h4`,`h5`,`h6`，他们都是文字类块级元素，里面不能放其他块级元素。

2. 链接里面不能再放链接

## 行内块元素的特点

在行内元素中有几个特殊的标签`img`，`input`,`td`，可以为他们设置宽高和对齐属性。

- 和相邻行内元素（行内块）在一行上，但是之间有空白间隙
- 默认宽度就是它本身内容的宽度
- 宽度、高度、内外边距都可以设置


## 选择器

![选择器](https://github.com/yjn2015/CSS-content/blob/master/img/select.png)

1. 属性选择器


选择器           | 含义                            | 
--------------- |---------------------------------|
 E[attr]        | 存在attr属性即可                 | 
 E[attr=val]    | 属性值完全等于val                | 
 E[attr*=val]   | 属性值里包含val字符串并且在任意位置| 
 E[attr^=val]   | 属性值里包含val字符并且在开始位置  |
 E[attr$=val]   | 属性值里包含val字符并且在结束位置  |


 2. 伪元素选择器

 选择器          | 含义                            | 
--------------- |---------------------------------|
 E:first-letter | 文本的第一个单词或字              | 
 E:first-line   | 文本第一行                       | 
 E:selected     | 可改变选中的文本                  | 

 注意：

 伪类选择器和伪元素选择器的区别：

 1. `:first-child` 伪类选择器，仅有一个冒号的就是伪类选择器
 2. `::first-letter` 伪元素选择器，有两个冒号的话就是伪元素选择器


 3. `E::before` 和 `E::after`

 `before` 和 `after` 是在盒子`div` 内部的前面插入内容或者是内部后面插入内容


 ## CSS 三大特性

 1. CSS 层叠性

 所谓层叠性就是多种样式的叠加，假如样式名称相同，最后的样式会覆盖掉前面的样式。
 样式冲突，遵循的原则就是就近原则，那个样式近就执行那个样式。

 2. CSS 继承性

 `CSS` 继承性是指书写`CSS` 样式表时，子标签会继承父标签的某些样式，如文本颜色和字号，想要设置一个可继承的属性，只需将它应用于父元素即可。

 3. CSS 优先级


 `specificity` 用一个四位字符串来表示，更像四个级别，值从左到右，左面的最大，一级大于一级，数位之间没有进制，级别之间不可超越。

继承或者*的贡献值         | 0,0,0,0
-------------------------|----------
 每个元素（标签的贡献值）  | 0,0,0,1 
 每个类，伪类贡献值        | 0,0,1,0
 每个ID贡献值为            | 0,1,0,0
 每个行内样式贡献值         | 1,0,0,0
 每个!important            | 无穷大


 优先级的问题：

 !important > 行内样式 > ID > class > 标签


 注意：

 数位之间没有进制，比如说， 0,0,0,5 + 0,0,0,5 = 0,0,0,10 而不是 0,0,1,0,所以不会存在10个`div` 能赶上一个类选择器的情况。

 总结优先级：

 1. 使用了`!important` 声明的规则
 2. 内嵌在 `html` 元素的`style` 属性里面的声明。
 3. 使用了`ID` 选择器的规则。
 4. 使用了类选择器、属性选择器、伪元素和伪类选择器的规则。
 5. 使用了元素选择器的规则
 6. 只包含一个通用选择器的规则
 7. 同一类选择器遵循就近原则 


## 外边距合并塌陷的问题

1. 什么是外边距合并的概念？

外边距合并指的是，当两个垂直外边距相遇时，它们会形成一个外边距。

合并后的外边距的高度等于两个发生合并的外边距的高度中的较大着。

例子：

当一个元素出现在另一个元素上面时，第一个元素的下外边距于第二个元素的上外边距会发生合并。请看下图：

![外边距合并](https://github.com/yjn2015/CSS-content/blob/master/img/margin_collapsing_example_1.gif)


当一个元素包含在另一个元素中时（假设没有内边距或边框把外边距分割开），它们的上和/或下外边距也会发生合并。请看下图：



```
  <!-- html 代码 -->
  <div class="father">
    <div class="son">

    </div>
  </div>

  <!-- css 代码 -->
  <style>
    .father {
      width: 300px;
      height: 300px;
      background-color: skyblue;
      margin-top: 100px;
      border: 1px solid red; /* 解决外边距合并(塌陷) 问题*/

    }

    .son {
      width: 200px;
      height: 200px;
      background-color: green;
      margin-top: 30px;
    }
  </style>
```




