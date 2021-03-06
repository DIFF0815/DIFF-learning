# Markdown简明教程

**说明 **

*本教程 自己手动敲了 一遍学习 教程，教程 来自[Simple-Markdown-Guide](https://gihub.com/Melo618/Simple-Markdown-Guide)。

*本教程使用[Typrora]([Typora — a markdown editor, markdown reader.](https://www.typora.io/))编辑器，一个非常好用的编辑器。

## 基本

* Markdown是一种用来写作的轻量级标记语言。
* 用于标记语法，代替常见的排版格式。
* 兼容HTML代码。
* 特殊字符自动转换，例如`<`和`&`



## 字体

* 使用星号`*`和底号`_`表示`<em>`标签 

  例如：

  ```mark
  *我是斜体*
  _斜体_
  ```

   效果：

  *我是斜体*

 * 使用双星号`**`或`__`表示`<strong>`标签 

   例如：

   ```mark
   **我是强调**
   __我是强调__
   ```

   效果：

   **我是强调**



## 换行

* 单一段落使用空白行



## 标题

* 生成`<h1>`-`<h5>`标签，是通过在文字前面加上同等个数`#`符号来实现。

* 出于美观，也可以使用对称的闭合式标题符合。

  例如：

  ```mark
  ### 这是标题
  ### 这是标题 ###
  ```

  效果：

  ###  这是标题

  

## 列表

* `*`，`-`，`+`这三个符号效果都一样，这三个符号被称为markdown列表符号。而有序列表则使用数字接着一个英文句点 （文字大小并不会影响输出序列）

  例如：

  ```mark
  * 第一行
  * 第二行
  * 第三行
  6. 第四行
  5. 第五行
  4. 第六行
  ```

  效果：

  * 第一行
  * 第二行
  * 第三行
  6. 第四行
  5. 第五行
  4. 第六行

## 引用

* `<`符号表示引用，可以简写于第一行，也可以每一行都添加。

* 区块的引用可以嵌套，只需要在层级上加上同等数量的`<`符号 

* 引用内可以使用其他markdown语法，包括标题、列表、代码区块等。

  例如：

  ```mark
  > 引用
  > > 引用中的引用
  ```

  效果：

  > 引用
  >
  > > 引用中的引用



## 代码区块 

* <code>\`</code>是表示inline代码，4个<code> </code>(空格)来表示缩进代码段，分别对应HTML的`<code>`,和`<pre>`标签。也可以使用<code>\`\`\`</code>来表示围栏式代码块（**GFM**语法，部分编辑器不支持），并指定其他 语言类型，并实现语法高亮。围栏式代码可以大量减少缩进的使用，大规模的代码块使用非常方便。

  例如：

  ```
  `sort()` 函数按升序对给定的数组值排序。
  ```

  普通的缩进式代码块：

  ```
  <?php
      $arr = array('a' => 1, 'b' => 2);
  	var_dump($arr);
  ?>
  ```

  带语法高亮的围栏式代码块：

  ```php
  <?php
      $arr = array('a' => 1, 'b' => 2);
  	var_dump($arr);
  ?>
  ```

  

## 链接

* markdown支持两种形式的链接语法：行内式和参考式两种形式。

  行内式链接：是在方括号 后面接圆括号即可 

  例如：

  ```mark
  [DIFF0815](https://github.com/DIFF0815/)
  ```

  效果：

  [DIFF0815](https://github.com/DIFF0815/)

  

  参考式链接：是在链接文字的后面加上一个另一个方括号，在第二个方括号里面要填入用以辨识链接的标记。

  例如：

  ```
  [DIFF0815][mygithub]
  [mygithub]: https://github.com/DIFF0815/ "diff的github"
  ```

  效果：

  [DIFF0815][mygithub]

  [mygithub]:https://github.com/DIFF0815

  

## 图片

* markdown使用 一种和链接很相似的链接来标记图片，只是多了一个`!`在最前面，同样也允许两种格式：行内式和参考式。

* 目前为止，markdown还没有办法指定图片的宽高，如果你需要的话，可以使用`<img>`标签。

  行内式图片链接：是在方括号后面接圆括号即可。

  例如：

  ```mark
  ![图片1](C:\Users\Administrator\Pictures\Saved Pictures\图片1.jpg)
  ```

  效果：

  ![图片1](C:\Users\Administrator\Pictures\Saved Pictures\图片1.jpg)

  参考式链接：是在链接文字的后面加上一个方括号，在第二个方括号里面填入用以辨识链接的标记。

  例如：

  ```
  ```

  效果：

  ![图片][tupian]

  [tupan]:https://pic1.zhimg.com/80/v2-e97bc2a9d1dda1884f023febcaebe8f0_720w.jpg?source=1940ef5c  "图片"



## 分割线

* 使用三个以上的`*`,`-`来建立一个分割线，行内不能有其他 字符。

  例如：

  ```mark
  * * * 
  ***
  - - -
  ---
  ```

  效果：

  * * *
  ***
  - - -
  ---



##  表格 

* markdown 使用 `|`和`-`来绘制表格，`:`可控制左对齐、右对齐和居中。

  例如：

  ```markd
  | Title | Desc |
  | :---- | :--: |
  | 超市  | 36km |
  | 酒店  | 40km |
  ```

  效果：

  | Title   | Desc        |
  | :------  | :-----------: |
  | 超市     | 36km    |
  | 酒店	 | 40km    |

  

##  特殊符号

* markdown利用 `\`字符来 转义一些在语法中有特殊意义的符号

  

## 其他以后再补充

* 

