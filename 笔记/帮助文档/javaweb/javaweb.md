#  	HTML

## 概念:

### 标签概念:

语义标签: 主要是该表签名表示的意义不同, 文本样式主要是还是通过css定义. 不过是方便程序员罢了

### 块和行内:

块元素:主要是为了宏观的给页面进行布局

行内:主要是用来包裹文字对文字进行装修.

​	<p 中不能放任何块元素


### 浏览器修正:

浏览器修正并不会修正源码, 而是将源码加载到内存之后,从内存里面修正.

浏览器中elements一栏中可以显示内存中的元素.

## 特殊字符

```html
 &nbsp;  空格字符
    &gt;    小于号
    &lt;    大于号
    &copy;  版权符号
```

## 标签

### <meta

单个出现,mata用于指定网页之中的一些元数据.  

**关键字**

keywords:表示网站的关键字.    表现形式:name="keywords"

content:指定数据内容 表现形式:content="关键字"

charset:指定网页的字符集 表现形式:charset="字符集"

description:表示搜索引擎中对网页的描述.

http-epuiv:表示网页在几秒后开始跳转至另一个网页

refresh:跟在http-epuiv里面

### **下面这些是语义化标签**

### <h1~6

成对出现,标题标签

### <hgroup

成对出现,用来为标题分组,可以将一组相关的标签同时放入hgroup中

### <em

成对出现,行内元素,用于表示语音语义的加重

### <strong

成对出现,行内元素, 表示强调,(字体加粗)

### <blockquote

成对出现,块元素,独占一行  常用来表示长引用,一般用来引用一段话.

### <q

成对出现,行内元素,常用来表示短引用,用来给一句话加上双引号.

### <sub    <sup

将一行 一分为二, sub显示在下面的一半,sup反之.  成对出现

### <header  <main <footer 

页面内容的 头部,主体,尾部.   

### <nav

表示网页中的导航.

### <aside

通常侧边栏

### <article

表示一个独立的文章

### <section

表示一个独立的区块,上面的都不合适时,用这玩意儿.

### <div

**块元素**,div没有语意, 用来表示一个区块, 没别的意思.  其实上面的所有玩意儿都可以用div.

### <span

**行内元素**,装在div里   用于选中文字

### **列表**

#### <ul

无序列表 <ul

#### <ol

​    有序列表 <ol

#### <dl

​    定义列表 <dl

给列表下定义<dt      

给下的定义进行解释<dd

#### <li

​    列表里面的列表项 套在列表里面

​      <li

### **<a  超链接**  重点!

是一个行内元素.不能自动换行.   可以嵌套任何元素(不包含自己).        

​	 **href**属性  填写他要跳转的网址

```html
<a href="网址">超链接</a>
```

​	**target**属性: 定义连接的打开方式

### <**img** **图片标签**

替换元素, 从外部引入资源的标签 占位大小与引入资源大小有关

属性:

​		**src="" ,**  双引号内填写,引入资源路径.

​		**alt="",** 对图片进行描述, 图片没显示出来时,就会显示. 并不是所有的浏览器都会这么做.  **搜索引擎会根据alt中的内容,来识别图片.** 			

​		width=""  设置宽度    		宽度和高度中如果只修改了一个

​		height=""设置高度   		 另一个则会等比例缩放(不建议改														大小)

**图片的格式**

​		(**精美照片)jpeg(jpg)**:支持的颜色比较丰富,不支持透明效果,													不支持动图

​		**(动态图)gif** : 支持的颜色比较少,支持简单透明,支持动图

​		**(网页常用)png:** 支持颜色丰富,复杂透明,不支持动图                             

​		webp:专门用于网页, 集合所有优点,内存又小.

​		base64: 将图片  用base64进行编码,  在浏览器中复制时,复制内容也会是编码内容.





### <iframe 内联框架

在网页中开辟一个小窗口 显示其它内容

属性:

​		src : 显示内容路径,

​		width:高度

​		height:宽度

​		**frameborder**:  框架边框大小,一般为0,不写此属性,大小默认为1

### <audio  <video音视频文件

默认不允许用户控制播放

还可以在里面写一个 <source  在这里面 用src写路径

帮助不支持播放标签的浏览器给用户一个提示.



属性: controls  允许用户控制 少见的没有值的属性

​		autoplay	自动播放音频, 同上

​		loop  自动播放

​		src :设置文件路径

​		



















































## 表单

### 表单安全性

我把这理解为对表单文本框内值的约束规则

- placeholder    提示信息    
- required          非空判断
- pattern            正则表达式



### 简述

```html
<!--
action:表单提交的位置,可以使网站,也可以是一个请求处理地址
method: post,get 提交方式
-->
<form>     <!--表单标签-->
	<input type="text" name="名字"> <!--文本域输入框-->
    <input type="password" name="名字"> <!--密码输入框-->
    <input type="radio" name="名字"> <!--单选按钮-->
    <input type="checkbox"><!--多选按钮-->
    <input type="submit" value="Submit"><!--提交按钮-->
</form>
```

### 标签

```html
<form>
    当我们点击'啊啊啊'文字时 鼠标会自动跳转到对应id的文本框内.
    <lable for="id值">啊啊啊</lable> ,
</form>
```



```html
<input type="文本格式" name="名字" maxlength="最大字符数" size="输入框长度" value="默认值">
<!--type属性的值
button    按钮
checkbox	多选框
color      颜色
date
datetime
datetime-local
email	邮箱验证
file	上传文件
hidden
image	图片按钮
month
number		数字验证
password    密码
radio		单选框
range		滑块(音量?)
reset
search		搜索框(有个x清楚文本内容)
submit     提交
tel
text    文本
time
url		网址验证
week
-->

单选框
<input type="radio" value="boy" name="sex" chacked/>男 
<input type="radio" value="girl" name="sex"/>男女
<!--只有name值一样的单选标签,才会有"单选"的特性 							chacked默认选中	 复选框中也有-->

图片按钮,  图片按扭也可以提交表单
<input type="image" src="路径">
普通按钮
<input type="botton" name="" value="默认值">
文件域 上传文件
<input type="file" name="files" accept="">
<!--有了这个就可以将本机文件上传到网页了  accept限制上传的文件格式-->


```

![image-20210531224510276](F:\图像\typora图像保存位置\image-20210531224510276.png)





```html
<textarea rows="10" cols="30">
我是一个文本框。
</textarea>

<!--文本框标签 
属性			作用
autofocus		加载页面自动获得文本框焦点	
cols			规定文本框的宽度 
rows			规定文本框一次显示的行数
placeholder 	 描述你期望用户填写的内容, 值是text类型,只有当文本框中没有内容时才会显示
-->
```





```html
<select name="菜品">  
    <option value="烤肉饭">烤肉饭</option>
</select>
<!--
<select> 下拉框,
name: 名字
<option> 下拉框选项
value:值
selected   默认选中
-->
```











## 属性(少许关键字).

### keywords:

在name里面,表示网站的关键字.    表现形式:name="keywords"

### content:

指定关键字内容 表现形式:content="关键字"

### charset:

指定网页的字符集 表现形式:charset="字符集"

### description:

在name里面,表示搜索引擎中对网页的描述.

### http-epuiv:

表示网页在几秒后开始跳转至另一个网页  refresh:

### href<a标签

表示超链接  用在<a 标签

关键字:"#" 用于回到页面顶部  

​			"#??" 用于去指定id标签所在的位置

​			"javascript:;" 占位符虽然有超链接可以点但是无响应

### target<a标签

指定超链接打开的位置  不写关键字时 默认_self

包含关键字:"_self 表示当前页面", 国外较多用

​					"_blank在一个新的页面中打开"国内较多用

### id:

区分大小写, 身份证号有唯一性, 每个标签都可添加



### width=""  设置宽度    	

### height=""设置高度 

### tetle:

标题属性, 给标签加一个备注信息. 



























































































## 练习素材

### 文本素材

"家乡美丽的地方很多：有一望无际的茶园，有峰峦叠嶂的高山……但我最喜欢的还是美丽的江滨公园。

   初入公园，第一个映入眼帘的的当然是我最喜爱的中央喷泉。喷泉的四周立着四根又高又大的灯柱，宛如四位士兵不分日夜的保护着它们。夜已降临，优美的音乐如约而至，泉水忽高忽低，时而像一群可爱的海豚跳跃;时而如琴键奏出春天的赞歌;时而似千奇百怪的烟火喷上蓝天;时而……踏着欢快的节奏，灯柱像变魔术似的，不停地变幻出绚丽多彩的灯光，照耀在喷泉上，让公园变得更加五彩缤纷。

   公园的东边，几棵高大威风的樟树昂首耸立，那光溜溜的树梢就像秃头的老爷爷。树上已悄悄然地冒出了几片娇嫩的小绿芽儿，像一个个调皮的娃娃向我们招手，迎接春的到来，为公园增添了不少生机。玉兰树上一位位花仙子争奇斗艳，有的站在枝头唱歌，有的穿上花瓣衣裳变得更加美丽，有的小脑袋埋藏在小绿帽里还没探出来，却顽皮的想要把帽子扔掉。这么多花仙子，各有各的美丽，千姿百态。看呀看呀，我忽然觉得，自己就是一位小花仙子，穿着粉红的裙子，和伙伴们翩翩起舞。花坛中，娇嫩的茶花、艳丽的牡丹、热情的迎春花……正在争论谁更美丽，赢得春姑娘的赞赏。

   公园的西面，人工河缓缓流淌，河水清澈见底。有许多小蝌蚪向四面八方去“旅行”。岸边的柳树如小女孩似的，扎着小辫子，在唱优美的童谣。粉红的桃花被春姑娘称为“花中公主”，害羞的的脸儿红成小太阳，趁着春光，显得更加美丽动人。鸟儿从蔚蓝的天空中落到它的休息站，它用嘴啄了啄，就急忙往别处飞去，只有树枝还在那不停的摇晃。小草也不甘示弱，用自己的绿毛线，为大地编制了一条绿茸茸的地毯。孩子们在地毯上踢足球、捉迷藏、玩游戏、打滚，不亦乐乎，时不时传来欢快的笑声。

   公园的尽头，一条又宽又长的堤坝依水而建。靠栏远眺，松荫溪的水清清的、凉凉的，站在岸边，你会感觉清清爽爽，让人身心放松，流连忘返。对岸的独山、村落像被摄影师“咔擦”地映在水里。好一派江南水乡的优美风光。

   江滨公园，你是我们家乡最美的一道风景线。"

























# CSS

## 定义方式

1.内联样式,行内样式

​	-在标签内部通过style属性来设置元素样式

```html
<div style="font-size: 20px;color: aqua;">
```

2.内部样式表

将样式编写到head标签中 的 **style** **标签**里

```css
<style>
        div{color: #aaffbb;font-size: 60px;}
    </style>
```

3.外部样式表

引入css文件

```html
 <link rel="stylesheet" href="./css样式.css">
```



## 基本语法:

选择器 声明块



选择器 用来选择html中的标签   

声明块 里面定义选中标签的样式.

​          声明块中 填写名值对    名是样式名, 值是赋给样式名的值,   名值对以  ;  结尾

## 继承

![image-20201223221229350](F:\图像\typora图像保存位置\image-20201223221229350.png)







































## 选择器:

### 选择器的优先级:

内联样式:	1,0,0,0

id选择器:	0,1,0,0

类和伪类选择器: 	0,0,1,0

元素选择器:	0,0,0,1

通配选择器:	0,0,0,0

继承的样式:    null



比较优先级时,对 所有类选择器的优先级进行相加,最后优先级越高,越优先显示,    **同类选择器的优先级,不会突破自身级别极限**

如果优先级相同,则优先使用靠下的样式.

 

如果在某一个样式的后面添加     !important  关键字, 则会获取做高的优先级



### 元素选择器

元素名 +代码块

```css
div{color: #aaffbb;font-size: 60px;}
```



### id选择器

根据标签 的id属性进行选择  

id具有唯一性, 即使语法不报错也不建议使用,不利于扩展

```css
<div id="red">aaaaaaaaaaaaa</div>
#red{   //   #+id名
    color: blue;
    font-size: 150px;
}
```

### 类选择器

根据标签的 class属性  来选中一组(一类)元素.

类名可以取多个 名与名之间 用 空格 隔开

```html
  <div class="lanse">asdsadf</div>
    <div class="lanse">asdsasdadf</div>
    <div class="huangse lanse">asdsasdfasfadf</div>
```

```css
.lanse{     //  .+class名
    color: blue;
}
.huangse{
    color: yellow;
}
```



### 统配选择器

全选中

```
*{
  样式
}
```

### 交集选择器

用法很简单 看代码吧 懒得描述了

总之就是全部符合 才可以,  是一个复合选择器

甚至可以复合多个类名

```html
div class="lanse" id="red">asdsasdfasfadf</div>
```

```css
div.lanse#red{
    color: rgb(21, 182, 61);
    font-size: 99px;
}
```

### 并集选择器

选择器与选择器之间  加  ,   号    大概语法参考上面

![image-20201223171006809](F:\图像\typora图像保存位置\image-20201223171006809.png)

###  子元素选择器:

父元素>子元素

### 后代元素选择器

祖先元素 后代元素

### 同辈选择器

同辈元素 

前一个元素+后一个元素

(只有一个元素生效哦)

为后一个元素改变样式



前元素 ~后元素 

选择前元素到后元素之间的**同辈后元素**



### 属性选择器:

![image-20201223185703622](F:\图像\typora图像保存位置\image-20201223185703622.png)

### 伪类选择器

![image-20201223192730825](F:\图像\typora图像保存位置\image-20201223192730825.png)

![image-20201223192757673](F:\图像\typora图像保存位置\image-20201223192757673.png)

## 样式

### style   

 在标签内部设置元素样式,

### 单位大小

![image-20201223231126973](F:\图像\typora图像保存位置\image-20201223231126973.png)

### color:

设置颜色  

格式:  #??????  or  颜色名

颜色单位:

![image-20201223232024599](F:\图像\typora图像保存位置\image-20201223232024599.png)

![image-20201223232807148](F:\图像\typora图像保存位置\image-20201223232807148.png)

HSL值我感觉可能美术生懂这玩意儿

### font-size:

设置字体大小  ??px  

### <a 伪类

a:link 用来设置访问过得超链接(正常的链接)

a:visited 用来设置没访问过的超链接  只能修改颜色,保护隐私(黄网)

a:hover 鼠标移入后的显示样式

a:active 鼠标点击的样式

### 伪元素

元素名::first-letter    首字下沉

元素名::first-line     表示第一行  

元素名::selection  表示选中的内容

元素名::before 元素开始的位置

元素名::after  元素的最后

​    注: before和after 必须结合 content属性 来使用

### background-color   

背景颜色

### **!important**

给样式设置最高的优先级

### overflow 

overflow-x:横向处理

overflow-y:竖向处理

父元素处理子元素溢出的属性

  值: 

​		visible: 默认值 子元素会从父元素中溢出,在父元素外部的位置显示

​		hidden:溢出内容将会被裁减不会显示

​		scroll: 生成两个滚动条,通过滚动条来查看完整内容.

​		auto:根据需要生成滚动条



### display:

元素种类的转换: inline 将元素设置成行内元素

​							block 将元素设置为块元素

​							inline-block: 将元素设置为行内块元素,可以设置宽高又不独占一行, 

​							table:将元素设置成一个表格

​							none:元素不在页面显示(可以通过手段显示)

### visibility

设置元素的显示状态

visible:默认值 ,正常显示

hidden:元素在页面中隐藏, 不显示. 但是依然占据位置.



### box-sizing:

设置盒子大小的计算方式.

border-box:让宽度和高度 代表可见框的大小, 用宽度和高度把大小给固						  定死了.



### 轮廓和圆角

**border**: 大小,颜色,显示状态  .    设置边框,此边框影响盒子大小

**outline**:   和border一样, 只不过该属性设置的轮廓线不会影响可见框的大小

**box-shadow**: 设置阴影, 不影响页面布局 默认与元素同大小. 

​			设置的值为:(+右-左)偏移量(单位:像素)  (+下-上)偏移量 

​								阴影的模糊半径          颜色

**border-radius**: 设置圆角,   可以根据方向(上左,上右,下左,下右)进行单设置

​							值为圆角半径: 值(x轴)  值(y轴)

​													 将元素设置为圆形50%

​			

### 浮动

**float:**行内元素 进行浮动后 会变成块元素  文字不会出现在元素的下方

![image-20201225183544090](F:\图像\typora图像保存位置\image-20201225183544090.png)

![image-20201225183415442](F:\图像\typora图像保存位置\image-20201225183415442.png)

### BFC属性

开启方法: float:left; 设置元素的浮动

​				display: inline-block;  将元素设置成行内块元素

​	(推荐)  将元素的overflow设置为一个非visible的值	

​		overflow: hidden;  开启其BFC

![image-20201225222902232](F:\图像\typora图像保存位置\image-20201225222902232.png)

### **clear** (通过伪类解决高度塌陷)

让元素免受其他元素浮动带来的影响.

![image-20201226152143295](F:\图像\typora图像保存位置\image-20201226152143295.png)

下面是思想

```css
<style>
        .box1{
            border: 10px #aaaaaa solid;
            /* overflow: hidden; */
        }
        .box2{
            height: 100px;
            width: 100px;
            background-color: #aaffbb;
            float: left;
        }
        .box3{
            clear:left;
        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="box2"></div>
        <div class="box3"></div>
    </div>
    
</body>

/*但是下面的方法更优*/

    <style>
        .box1{
            border: 10px #aaaaaa solid;
            /* overflow: hidden; */
        }
        .box2{
            height: 100px;
            width: 100px;
            background-color: #aaffbb;
            float: left;
        }
        /*通过CSS来解决高度塌陷,伪类*/
        .box1::after{
            clear:both;
            display: block;/* 转化成块元素*/
        }
    </style>
</head>
<body>
    <div class="box1">
        <div class="box2"></div>
    </div>
    
</body>
```



### 消除高度塌陷和外边距重叠的最佳方案

```css
.clearfix::before, /*表头 + 表屁股*/
.clearfix::afrter{
content:'';
display: table;
clear:both;
}
```



## ==盒子模型==(**重点**)

**盒子模型的可见大小 由 内容区 内边距 边框 大小的总和决定**

行内元素的盒模型:

​	![image-20201224175333407](F:\图像\typora图像保存位置\image-20201224175333407.png)

### 垂直外边距的重叠

垂直方向的外边距会发生重叠现象.

兄弟元素:

​		取两者之间的最大值

​		如果一正一负:则取两者的和

​		都是负数则取绝对值更大的

父子元素

​		子元素的上外边距会传递给父元素

​		影响页面布局 ,有下面两种处理方案

​		![image-20201224172812044](F:\图像\typora图像保存位置\image-20201224172812044.png)

​			





每一个盒子模型都由以下几部分组成:

### 	内容区(content)

```css
 /*
        内容区 content
        width 设置高度
        height 设置宽度
        background-color  设置背景颜色
    */
```

### 	内边距(padding)

```css
top(上) right(右) bottom(下) left(左) 设置对应方向的大小
padding-xx: ;
padding: ;(简写模式) 
可以设置四个值
                        两个值时: 上下 左右
                        三个值时: 上 左右 下
                        四个值时: 上 右 下 左
padding是对内容区的延伸, 颜色跟随内容区的设定
		所以可以在div标签里 嵌套一个div标签  然后在内部的div标准中 定义内容区的具体大小和颜色
			就是下面这种 .
<div class="box1">
        <div class="content"></div>
    </div>

.box1 {
    /*
        内容区 content
        width 设置高度
        height 设置宽度
        background-color  设置背景颜色
    */
    width: 300px;
    height: 300px;
    background-color: #aaffaa;
    
    padding-top: 100px;
}
.content {
    width: 300px;
    height: 300px;
    background-color: #010f01;
}

```

### 	边框(border)

```css
/*
        边框 border  
        border-color: #aafaff; 设置外边框颜色
                        也可以像下面那样搞四个值  
                        每个边框边的界限 是个斜线.以确保每个边框的大小相同
        border-width: 10px;     设置外边框大小  
                        可以设置四个值
                        两个值时: 上下 左右
                        三个值时: 上 左右 下
                        四个值时: 上 右 下 左
                        还可以通过 top(上) right(右) bottom(下) left(左)  来设置对应方向的边框大小
                        格式为 border-xx-width:??px;

        border-style: solid;    设置外边框的 样式, 
                        solid 实线
                        dotted 点状虚线
                        dashed 虚线
                        double 双线
                        none  没有 无 
        下面为 边框的简写形式,   三个值没有顺序要求
        border-top(上) right(右) bottom(下) left(左)  来设置对应方向的 三个值.
        border: #aaffaa 10px solid
    */
```

### 	外边框(margin)

![image-20201224120846043](F:\图像\typora图像保存位置\image-20201224120846043.png)

































































































# JS

## 注意事项

```js
'use strict'  严格检查模式
```



### 规范

![image-20210530141754418](F:\图像\typora图像保存位置\image-20210530141754418.png)







## 浏览器控制台编写js代码

控制台名字   console

打印变量  console.log()

![image-20210528151454778](F:\图像\typora图像保存位置\image-20210528151454778.png)



## 基本数据类型:

JavaScript 中有五种可包含值的数据类型：

- 字符串（string）

- 数字（number）

  ​	整数

  ​	浮点数

  ​	负数

  ​	NaN      not a number     表示不可表示的数

  ​	infinity			表示无限大的数

- 布尔（boolean）

- 对象（object）

  **js对象中所有的建 其实都是字符串.**

- 函数（function）

  ​	如果没有return 函数会返回 undefined 







有三种对象类型：

- 对象（Object）

  ​	对象需要用 {		} 扩起来

  ​	括号内每个属性用   ‘,’  隔开 

- 日期（Date）

- 数组（Array）

  数组用	[	]	扩起来

同时有两种不能包含值的数据类型：

- null            空值
- undefined  未定义的值,所有js变量未赋值时全是这个值.
- NaN          非数字,非数值.

查看某个变量的数据类型: 

​	typeof()函数 : 传入一个参数, 参数为变量.返回它的数据类型. 



## 逻辑and关系运算

​		关系运算

==========     表示等于    自作字面上的比较,比如说  

```js
var i = 12;
var m = "12";
(i==m);  //true
(i===m); //false
所以在js中  尽量用===
```





## js中的面向对象

```js
class 类名{
    //构造器
    constructor(name){
        this.name=name;
    }
    //方法 直接定义,没有什么返回值这一说
    getname(){
        console.log('我的名字是'name);
    }
    
    
}
```





## 语法规则

### 定义多行字符串

```js
var name = `
	这里面可以编写 多行字符串
`
```

### 模板字符串

```js
var name = "炸毛"
var string = `我爱你, ${name} `
```



### 一些方法 

```js
//数组
.length   // 获取长度
slice() //截取数组的一部分  返回一个新的数组
array.indexOF();   //通过元素获取下标
.push() //向数组末端添加数据,并扩充长度
.pop() //弹出一个数据
unshift(),shift() //头部
sort() //排序
reverse()//翻转
concat([])  //添加元素 返回一个新数组,  不修改原数组
join()   //以特定字符链接数组元素


//字符串
.toUpperCase() //大写
.toLowerCase() //小写
.substring()	//截取字符串
```



### 对对象的操作

```javascript
//定义对象
man{
    var name="炸毛",
    var age = 19
}
//使用一个对象中不存在的属性, 会提示 undefined(不存在) 不会报错
man.aa 
undefined

//动态的删减属性
delete man.name 
man.name
undefined

//动态的增加属性  直接赋值就添加了
man.aa="这是aa"

//判断属性值是否存在这个对象  继承来的也算在内
'age' in man
true

//判断一个属性是否是这个对象自身拥有的 hasOwnProperty()
//返回值也是 true或 false  

```

### 遍历数组

for(var 下标 in 数组){

代码块

}

![image-20210529115402281](F:\图像\typora图像保存位置\image-20210529115402281.png)



## Map Set

map

```js
Map对象的属性

size：返回Map对象中所包含的键值对个数
Map对象的方法

set(key, val): 向Map中添加新元素
get(key): 通过键值查找特定的数值并返回
has(key): 判断Map对象中是否有Key所对应的值，有返回true,否则返回false
delete(key): 通过键值从Map中移除对应的数据
clear(): 将这个Map中的所有元素删除


//遍历map
const map = new Map([['a', 1], ['b',  2]])

for (let key of map.keys()) {
  console.log(key)
}
// "a"
// "b"

for (let value of map.values()) {
  console.log(value)
}
// 1
// 2

for (let item of map.entries()) {
  console.log(item)
}
// ["a", 1]
// ["b", 2]

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value)
}
// "a" 1
// "b" 2

// for...of...遍历map等同于使用map.entries()

for (let [key, value] of map) {
  console.log(key, value)
}
// "a" 1
// "b" 2

```

set

```js
Set 中的值是不可以重复的 是一个一维数组,


Set中的特殊值

Set 对象存储的值总是唯一的，所以需要判断两个值是否恒等。有几个特殊值需要特殊对待：

+0 与 -0 在存储判断唯一性的时候是恒等的，所以不重复
undefined 与 undefined 是恒等的，所以不重复
NaN 与 NaN 是不恒等的，但是在 Set 中认为NaN与NaN相等，所有只能存在一个，不重复。
/*-------------------基本方法------------------------------*/
add(value)：添加某个值，返回 Set 结构本身(可以链式调用)。
delete(value)：删除某个值，删除成功返回true，否则返回false。
has(value)：返回一个布尔值，表示该值是否为Set的成员。
clear()：清除所有成员，没有返回值。

//合并set
/*注意这个[...]   是必须的  否则 他会把 set1当做一个元素存储进去
如果把两个元素值相同的set存储在一个 set里  并不会被去重*/
var set = new Set([...set1,...set2]);  //并集

//求交集   利用filter方法来求交集  差集很简单 在 被执行对象前加 '!' 就行

let set1 = new Set([1,1,1,9,2,5,3,6,4,2]);
let set2 = new Set([7,8,10,11,1,2,3,4]);
let set3 = new Set([...set1].filter(x =>set2.has(x))); //交集
let set3 = new Set([...set1].filter(x =>set2.!has(x)));//差集
console.log(set3);


```







## 函数

定义方式

```js
//第一种定义方式
function 函数名(){
    
    return ;
}

//第二种定义方式 
var 函数名 = function(){
    return;
}
```

## 变量作用域

var,let,const的区别

学习参考的是下面文章

https://chinese.freecodecamp.org/news/javascript-var-let-and-const/

```js
/*----------------var---------------*/
var  全局作用域 ;
	//变量提升是 JavaScript 的一种机制:在执行代码之前，变量和函数声明会移至其作用域的顶部。 这意味着如果我们这样做:

console.log(greeter);
var greeter = 'say hello';
//生面的代码会被解释为:

var greeter;
console.log(greeter); // greeter is undefined
greeter = 'say hello';
//因此，将var声明的变量会被提升到其作用域的顶部，并使用 undefined 值对其进行初始化.
	
/*----------let----------*/

let  块级作用域
//用let定义的变量只会在 当前块内定义, 

//let定义的变量可以被重新赋值 但是不能被重新定义

let a1 = 5;
a1=3;    //可以

let a1 = 5;
let a1 = 3;//error
//这一点与var 不同 
var a1= 3;
var a1= 6;//可以



/*--------------const--------------*/
const greeting = {
    message: 'say Hi',
    times: 4,
};    //定义

const greeting = {
    words: 'Hello',
    number: 'five',
}; // error:  Assignment to constant variable.

greeting.message = 'say Hello instead'; //可以


```









- 用var声明在函数内部的变量为局部变量

- 直接定义在函数内部的变量也是**全局变量**

- 定义在函数外部的变量是全局变量即使使用var定义也是全局变量

- 父函数**声明**的变量,在子函数中同样可以使用, 但是仅限在父函数的范围内

- 用`var`声明的变量会被提升到其作用域的顶部，并使用 undefined 值对其进行初始化。 **详解看上面代码块**

- 用`let`声明的变量会被提升到其作用域的顶部，不会对值进行初始化。

- ### const 声明的变量在块级作用域内

- ### const 不能被修改并且不能被重新声明

- const定义的对象不能被修改,但是对象内属性的值可以被修改,详解看代码块

- const声明的变量,**必须在声明时对其初始化**



```js
  var a1 =1;   //全局变量a1
  console.log(a1);
  console.log("aaa");

  function hanshu(){
      var a1;       //局部变量a1  为负值
      console.log(a1);
      var a2=a1+1;
      console.log(a2);
      console.log('aaaaaa');
      function hanshu(){
          console.log('a1='+a1);  //使用的是父函数的a1
           a1=3;        //父函数a1赋值
          console.log(a1);
          var a2=a1+1;
          console.log(a2);

      }
      hanshu();
      console.log('a1='+a1); // 局部变量a1 =3
      console.log('a2='+a2);
  }
  hanshu();

  console.log('aaaaaaaaaaaa');
  console.log(a1);  //仍然是全局变量
```









## 一些关键字

```js
typeof x;  //获取变量的类型

arguments;   //相当于参数列表   是一个数组
 
rest;   //定义在参数列表里面 以...的形式.   会将多余的参数组合进一个数组




```



## 像java一样定义一个类

![image-20210530150626681](F:\图像\typora图像保存位置\image-20210530150626681.png)

实际上,上面那种并不实用

```js
var zhamao={
    name:'炸毛', //属性 ->姓名
    bitrh:2001,	//属性-> 出生年饭
    age: function getAge(){
    	var now = new Date().getFullyear(); //获取现在的年份
        return now-this.bitrh; //返回现在的年级
    }   //定义一个getAge方法 ,用age属性接受该方法的返回值.
}
```



## JSON转化对象

- 用来传输由属性值或者序列性的值组成的数据对象

- JSON中属性以键值对的形式存在,其中键(key)以字符串的形式表述.

	```json
	{'name':'炸毛','age':19,'home':'河南省开封市'}
	```

- 字符串的表示可以用双引号或单引号表示,但浏览器中默认是  [  ” ”  ] ; 







将一个对象 转化为 JSON格式

```JS
var JSONUser = JSON.stringify(对象);  //将一个对象转换成JSON格式 ,需要定义一个变量来接收

var man = JSON.parse("JSON对象");  //讲JSON字符串转换成一个对象.   

//但是像上面那个代码块那样,如果把一个属性定义为,某个方法的返回值,  那么在转换时,并不会被转换成相对应的键值对.
```











## BOM

BOM 就是 [浏览器对象模型](https://zh.wikipedia.org/wiki/浏览器对象模型)（BrowserObjectModel）

**Navigator** ,封装了浏览器的信息

```js
//常用的
navigator.appName    //返回浏览器的名称
navigator.appVersion  //返回浏览器的平台和版本信息
navigator.userAgent	//饭会友客服机发送服务器的 user-agent头部的值
navigator.platform	//返回浏览器的操作平台
```



**location非常重要**

```js
host                       //返回一个URL (也就是网页网址)
protocol				//返回协议
href					//返回完整的URL
/*---------------方法----------------*/
assign()   //加载一个新的页面, 里面需要一个 URL参数
reload()     	//重新载入当前页面    ??刷新?     如果把参数设置为ture 那么刷新时 就会从服务器去重新获取页面文件,而不是从缓存中.
replace()		//用新的页面 替换当前页面

```













## DOM

### 概念

通过这个对象模型，JavaScript 获得创建动态 HTML 的所有力量：



- JavaScript 能改变页面中的所有 HTML 元素
- JavaScript 能改变页面中的所有 HTML 属性
- JavaScript 能改变页面中的所有 CSS 样式
- JavaScript 能删除已有的 HTML 元素和属性
- JavaScript 能添加新的 HTML 元素和属性
- JavaScript 能对页面中所有已有的 HTML 事件作出反应
- JavaScript 能在页面中创建新的 HTML 事件



### DOM获取节点

![image-20210530213401601](F:\图像\typora图像保存位置\image-20210530213401601.png)



### DOM更新节点

```js
节点.innerText=''; //修改节点内的文本值
节点.innerHTML=''; //修改节点的html标签元素
节点.style.样式='';//修改样式
```





### DOM删除节点

删除一个元素后,后面的元素下标会前移.

![image-20210530221359936](F:\图像\typora图像保存位置\image-20210530221359936.png)



### DOM插入节点

```js
<p id="js">JavaScript</p>
<div id="list">
    <p id="java">Java</p>
    <p id="python">Python</p>
    <p id="scheme">Scheme</p>
</div>
//
var
    js = document.getElementById('js'),
    list = document.getElementById('list');
list.appendChild(js);//将list插入到js节点的子节点的最后面,
```

从0开始

```js
var
    list = document.getElementById('list'),
    ref = document.getElementById('python'),
    haskell = document.createElement('p');//创建一个标签节点
haskell.id = 'haskell';
haskell.innerText = 'Haskell';
list.insertBefore(haskell, ref);//将第一个参数节点,添加到第二个参数节点上面.
```











## 操作表单



```js
如果我们要操作单选框等等的节点时,我们要如果操作他们所返回的值呢?
var radio = doucment.getElmentByID("")  ;
radio.value="";    
------------xxxxxxxx----------
var radio = doucment.getElmentByID("");
radio.checked=true/false;  
----------√√√√√√√√√√-
```





# JQ框架

## 语法

```js
$(选择器).事件(
	function(){
        编写代码
    }
);
```



































# TomCat

启动关闭,  启动 bin文件夹下的 startup.bat(启动)  shutdown.bat(关闭)

注: 启动失败 是因为没有配置 java的环境变量   tomcat启动需要jre环境



## 修改配置文件

在conf文件夹下面的server.xml文件中可以修改 访问的**本机名** 与**端口号**

<Host标签>修改 主机名

![image-20210601212229051](F:\图像\typora图像保存位置\image-20210601212229051.png)

注:当本机名修改为 域名时  会出现无法访问的情况. 因为windows 系统文件配置给阻止了. 需要去 C:windows\system32\drivers\etc\hosts文件中修改本机名

## web应用目录结构

![image-20210317223150309](F:\图像\typora图像保存位置\image-20210317223150309.png)



## 网站是怎么进行访问的	

在浏览器输入一个网址,  会先去本机 hosts 文件下找网址的映射ip, 如果没有,就去 DNS服务器上找, DNS服务器存放着全世界的网站域名.







# Maven

## 配置环境变量

新建系统变量名:  M2_HOME		路径  XXXXXX\apache-maven-3.6.3

​						 :  MAVEN_HOME  路径  XXXXXX\apache-maven-3.6.3

​							path   新建路径 %MAVEN_HOME%\bin

​														%M2_HOME%\bin

cmd 测试命令: mvn  -varsion





## 配置阿里云镜像和本地仓库

将配置好的xml文件 复制到 C:用户/.m2/  路径下    此为idea默认读取配置文件的路径 无法更改

```xml
<!--
     maven阿里云镜像
-->
  <mirror>
    <id>aliyunmaven</id>
    <mirrorOf>central</mirrorOf>
    <name>aliyun maven</name>
    <url>https://maven.aliyun.com/repository/public </url>
    </mirror>
<!-- 配置本地仓库 -->

<localRepository>D:\Studio\Maven\apache-maven-3.8.1\maven-repository</localRepository>

<!--中间夹的是路径-->
<!--在<profiles>标签下添加一个<profile>标签，修改maven默认的JDK版本。-->
<profile>
　　<id>jdk11</id>
　　<activation>
　　　　<activeByDefault>true</activeByDefault>
　　　　<jdk>11</jdk>
　　</activation>
　　<properties>
　　　　<maven.compiler.source>11</maven.compiler.source>
　　　　<maven.compiler.target>11</maven.compiler.target>
　　　　<maven.compiler.compilerVersion>11</maven.compiler.compilerVersion>
　　</properties>
</profile>

```



## Setting.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--
Licensed to the Apache Software Foundation (ASF) under one
or more contributor license agreements.  See the NOTICE file
distributed with this work for additional information
regarding copyright ownership.  The ASF licenses this file
to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
-->

<!--
 | This is the configuration file for Maven. It can be specified at two levels:
 |
 |  1. User Level. This settings.xml file provides configuration for a single user,
 |                 and is normally provided in ${user.home}/.m2/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -s /path/to/user/settings.xml
 |
 |  2. Global Level. This settings.xml file provides configuration for all Maven
 |                 users on a machine (assuming they're all using the same Maven
 |                 installation). It's normally provided in
 |                 ${maven.conf}/settings.xml.
 |
 |                 NOTE: This location can be overridden with the CLI option:
 |
 |                 -gs /path/to/global/settings.xml
 |
 | The sections in this sample file are intended to give you a running start at
 | getting the most out of your Maven installation. Where appropriate, the default
 | values (values used when the setting is not specified) are provided.
 |
 |-->
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 
   http://maven.apache.org/xsd/settings-1.0.0.xsd">


<localRepository>D:\SDK\maven-3.8.2\repository</localRepository>

  <!-- localRepository
   | The path to the local repository maven will use to store artifacts.
   |
   | Default: ${user.home}/.m2/repository
  <localRepository>/path/to/local/repo</localRepository>
  -->

  <!-- interactiveMode
   | This will determine whether maven prompts you when it needs input. If set to false,
   | maven will use a sensible default value, perhaps based on some other setting, for
   | the parameter in question.
   |
   | Default: true
  <interactiveMode>true</interactiveMode>
  -->

  <!-- offline
   | Determines whether maven should attempt to connect to the network when executing a build.
   | This will have an effect on artifact downloads, artifact deployment, and others.
   |
   | Default: false
  <offline>false</offline>
  -->

  <!-- pluginGroups
   | This is a list of additional group identifiers that will be searched when resolving plugins by their prefix, i.e.
   | when invoking a command line like "mvn prefix:goal". Maven will automatically add the group identifiers
   | "org.apache.maven.plugins" and "org.codehaus.mojo" if these are not already contained in the list.
   |-->
  <pluginGroups>
    <!-- pluginGroup
     | Specifies a further group identifier to use for plugin lookup.
    <pluginGroup>com.your.plugins</pluginGroup>
    -->
  </pluginGroups>

  <!-- proxies
   | This is a list of proxies which can be used on this machine to connect to the network.
   | Unless otherwise specified (by system property or command-line switch), the first proxy
   | specification in this list marked as active will be used.
   |-->
  <proxies>
    <!-- proxy
     | Specification for one proxy, to be used in connecting to the network.
     |
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    -->
  </proxies>

  <!-- servers
   | This is a list of authentication profiles, keyed by the server-id used within the system.
   | Authentication profiles can be used whenever maven must make a connection to a remote server.
   |-->
  <servers>
    <!-- server
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     |
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are
     |       used together.
     |
    <server>
      <id>deploymentRepo</id>
      <username>repouser</username>
      <password>repopwd</password>
    </server>
    -->

    <!-- Another sample, using keys to authenticate.
    <server>
      <id>siteServer</id>
      <privateKey>/path/to/private/key</privateKey>
      <passphrase>optional; leave empty if not used.</passphrase>
    </server>
    -->
  </servers>

  <!-- mirrors
   | This is a list of mirrors to be used in downloading artifacts from remote repositories.
   |
   | It works like this: a POM may declare a repository to use in resolving certain artifacts.
   | However, this repository may have problems with heavy traffic at times, so people have mirrored
   | it to several places.
   |
   | That repository definition will have a unique id, so we can create a mirror reference for that
   | repository, to be used as an alternate download site. The mirror site will be the preferred
   | server for that repository.
   |-->
  <mirrors>
    <!-- mirror
     | Specifies a repository mirror site to use instead of a given repository. The repository that
     | this mirror serves has an ID that matches the mirrorOf element of this mirror. IDs are used
     | for inheritance and direct lookup purposes, and must be unique across the set of mirrors.
     |
    <mirror>
      <id>mirrorId</id>
      <mirrorOf>repositoryId</mirrorOf>
      <name>Human Readable Name for this Mirror.</name>
      <url>http://my.repository.com/repo/path</url>
    </mirror>
     -->
    
   
    <mirror>
    <id>aliyunmaven</id>
    <mirrorOf>central</mirrorOf>
    <name>aliyun maven</name>
    <url>https://maven.aliyun.com/repository/public </url>
    </mirror>
  
  </mirrors>

  <!-- profiles
   | This is a list of profiles which can be activated in a variety of ways, and which can modify
   | the build process. Profiles provided in the settings.xml are intended to provide local machine-
   | specific paths and repository locations which allow the build to work in the local environment.
   |
   | For example, if you have an integration testing plugin - like cactus - that needs to know where
   | your Tomcat instance is installed, you can provide a variable here such that the variable is
   | dereferenced during the build process to configure the cactus plugin.
   |
   | As noted above, profiles can be activated in a variety of ways. One way - the activeProfiles
   | section of this document (settings.xml) - will be discussed later. Another way essentially
   | relies on the detection of a system property, either matching a particular value for the property,
   | or merely testing its existence. Profiles can also be activated by JDK version prefix, where a
   | value of '1.4' might activate a profile when the build is executed on a JDK version of '1.4.2_07'.
   | Finally, the list of active profiles can be specified directly from the command line.
   |
   | NOTE: For profiles defined in the settings.xml, you are restricted to specifying only artifact
   |       repositories, plugin repositories, and free-form properties to be used as configuration
   |       variables for plugins in the POM.
   |
   |-->
  <profiles>
    <!-- profile
     | Specifies a set of introductions to the build process, to be activated using one or more of the
     | mechanisms described above. For inheritance purposes, and to activate profiles via <activatedProfiles/>
     | or the command line, profiles have to have an ID that is unique.
     |
     | An encouraged best practice for profile identification is to use a consistent naming convention
     | for profiles, such as 'env-dev', 'env-test', 'env-production', 'user-jdcasey', 'user-brett', etc.
     | This will make it more intuitive to understand what the set of introduced profiles is attempting
     | to accomplish, particularly when you only have a list of profile id's for debug.
     |
     | This profile example uses the JDK version to trigger activation, and provides a JDK-specific repo.
    <profile>
      <id>jdk-1.4</id>

      <activation>
        <jdk>1.4</jdk>
      </activation>

      <repositories>
        <repository>
          <id>jdk14</id>
          <name>Repository for JDK 1.4 builds</name>
          <url>http://www.myhost.com/maven/jdk14</url>
          <layout>default</layout>
          <snapshotPolicy>always</snapshotPolicy>
        </repository>
      </repositories>
    </profile>
    -->

    <!--
     | Here is another profile, activated by the system property 'target-env' with a value of 'dev',
     | which provides a specific path to the Tomcat instance. To use this, your plugin configuration
     | might hypothetically look like:
     |
     | ...
     | <plugin>
     |   <groupId>org.myco.myplugins</groupId>
     |   <artifactId>myplugin</artifactId>
     |
     |   <configuration>
     |     <tomcatLocation>${tomcatPath}</tomcatLocation>
     |   </configuration>
     | </plugin>
     | ...
     |
     | NOTE: If you just wanted to inject this configuration whenever someone set 'target-env' to
     |       anything, you could just leave off the <value/> inside the activation-property.
     |
    <profile>
      <id>env-dev</id>

      <activation>
        <property>
          <name>target-env</name>
          <value>dev</value>
        </property>
      </activation>

      <properties>
        <tomcatPath>/path/to/tomcat/instance</tomcatPath>
      </properties>
    </profile>
    -->
  </profiles>

  <!-- activeProfiles
   | List of profiles that are active for all builds.
   |
  <activeProfiles>
    <activeProfile>alwaysActiveProfile</activeProfile>
    <activeProfile>anotherAlwaysActiveProfile</activeProfile>
  </activeProfiles>
  -->
</settings>
```





## pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.zhamao</groupId>
    <artifactId>mybatis</artifactId>
    <version>1.0-SNAPSHOT</version>


<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.6</version>
    </dependency>

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>

</dependencies>

    <!--读取该路径下 指定文件名-->
    <!--我们用这样的形式来约束maven 让他读取资源目录下的 该后缀文件. -->
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

    </resources>
    <!--maven约束JDK版本  此处为 jdk11-->
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.7.0</version>
            <configuration>
                <release>11</release>
            </configuration>
        </plugin>
    </plugins>
</build>



</project>
```

















# javaweb

## 小技巧

### 字符编码解码问题

![image-20210605141430294](F:\图像\typora图像保存位置\image-20210605141430294.png)

## web.xml

最新的webxml配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                  http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">

</web-app >
```



## maven父子项目

- 父项目中会有,子模块标签,填写子模块信息.

	```xml
	    <modules>
	        <module>servlet01</module> //子项目名
	    </modules>
	
	```

	

- 子模块的,pom.xml文件中会有一个 parent 标签,填写父项目信息

	```xml
	  <parent>
	    <artifactId>maven</artifactId> //父项目名
	    <groupId>com.zhamao</groupId>	//项目组名
	    <version>1.0-SNAPSHOT</version>	//版本信息
	  </parent>
	```

	

## servlet继承

我们编写一个类 ,继承 HttpServlet 实现类来编写代码.   点进源码后我们会发现其实是这样的一条继承链.

```java
servlet(接口) --> GenericServlet(类) -->HttpServlet(类) --> 自己的实现类
```



## servlet映射

我们所编写的servlet是一个java类, 浏览器访问 web服务器, 所以我们需要将 servlet映射到web服务中,      映射完成后 会根据用户查找的url信息,找到匹配的 servlet映射名,根据映射名找到与之匹配的servlet实例,   而这个servlet实例所存在的位置,我们也会在配置文件中表明清楚.

```xml
 <!--配置Servlet
    name是servlet名
    class是对应的java代码路径
    -->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.zhamao.servlet.MyServlet</servlet-class>
    </servlet>
    <!--servlet映射,第一个标签与 servlet标签中的 -name标签 对应
    url标签  是 浏览器网址栏的路径  一个servlet可以有多个映射
    -->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
<!--默认路径 优先级高于index.jsp-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
<!--尾部任意字符都可以访问 ,但是不能这么写/asdsad*-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/sads/*</url-pattern>
    </servlet-mapping>
<!--*号后面如果加了后缀 前面就不能有任何路径-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>*.zhamao</url-pattern>
    </servlet-mapping>
```



## servlet实例

我的第一个实例

```java
package com.zhamao.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class MyServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("我要进去咯~小夫.");
        resp.setContentType("text/html;charset=utf-8"); //设置表头和字符编码  设置内容类型
        PrintWriter writer = resp.getWriter();
        writer.println("你好哦哦哦哦啊啊");
    }
}

```





## servletcontext和config

原文链接：https://blog.csdn.net/gavin_john/article/details/51399425

### 小技巧

我们可以通过 

```java
getServletConfig().getServletContext().getInitParameter("");
//可以通过这样的方式来调用 context
//之前我们学过的请求转发是通过request对象的：
request.getRequestDispatcher("/url").forward(request, response);

//这里要说明的是，ServletContext也可以实现请求转发：
this.getServletContext().getRequestDispatcher("/url").forward(request, response);
//这两个转发效果是一样的。
```



### 简介

servletcontext 是一个 可以被所有servlet实例调用的 公共空间,   它在web服务器启动时就开始存在, 直到服务器关闭 才会死亡.

### servletContext应用

（1）多个Servlet通过ServletContext对象实现数据共享

------

这个很好理解，类似于Session，我们也可以通过ServletContext对象来共享数据，但要注意的是，Session只能在一个客户端共享数据，它独占一个客户端。而ServletContext中的数据是可以供所有客户端共享的。



### servletcontext不是线程安全的

```
当a用户调用servelt设置 context属性时，  可能中间插过来了一个b用户设置的值，  然后a用户再次获取属性值时， 就会获取到 b用户获取到的值。    
所以我们在servlet中 不能即设置 属性 又取出属性， 这可能会出现线程
```











### context和config的不同

他们都是用来初始化参数的，但不同的是， config只属于某个servlet 而context是属于整个web应用的。  

他们都在xml中配置初始化信息，不过 context有属于自己的标签   而config必须要在servlet标签内去配置  名字中也比 context的配置标签 多了 **==init==** 

两者通过相同的方法 来获取初始化参数值   

```java
//context
getServletContext().getInitParameter("");
//config
getServletConfig().getInitParameter("");
```







### 通过xml给context初始化键值对

```xml
    <context-param>
        <param-name>name</param-name>
        <param-value>炸毛</param-value>
    </context-param>
```







### 读取配置文件获取信息

```java
public class servletDemo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //将配置文件读取到输入流中
        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");//这里是配置文件路径
        String contenttype = this.getServletContext().getInitParameter("ContentType");
        resp.setContentType(contenttype);

        Properties properties = new Properties();
        properties.load(is);
        String ursename = properties.getProperty("ursename");
        String password = properties.getProperty("password");
        resp.getWriter().print("ursename="+ursename);
        resp.getWriter().print("password="+password);
        resp.getWriter().print("<br></br>");
        resp.getWriter().print("上面就是你的用户信息哦~~~");


    }
}

```



## 

## Listener监听

### contextListener

#### 技术，通过context来初始化实例对象

第一步 配置xml   **我们需要在配置文件中 表明在哪个位置 有一个监听者**

```xml
<web-app>
  <display-name>Archetype Created Web Application</display-name>
//	context初始化参数
  <context-param>
    <param-name>username</param-name>
    <param-value>zhamao</param-value>
  </context-param>
  <context-param>
    <param-name>password</param-name>
    <param-value>123456</param-value>
  </context-param>
  //	listener位置  注意！ 一定要放在 context标签下  否则报错 但如果用注解来配置就不会报错  
  <listener>
    <listener-class>com.five.listener.contextListener</listener-class>
  </listener>
</web-app>

```

第二步 实现监听者

```java
@WebListener("contextListener")
public class contextListener implements ServletContextListener {
    @Override
    public void contextInitialized(ServletContextEvent sce) {
        ServletContext servletContext = sce.getServletContext();
        String username = servletContext.getInitParameter("username");
        String password = servletContext.getInitParameter("password");
        dbUser dbUser = new dbUser(username,password);
        servletContext.setAttribute("dbuser",dbUser);

    }
}
下面是 要实例化的类 以及测试用的servlet
    public class dbUser {
    private String username;
    private String password;
}
---------------------------------------------------------------------------
    @WebServlet(urlPatterns = "/ListenerTest")
public class servlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.setContentType("text/html;charset=utf-8");
        PrintWriter writer = resp.getWriter();
        dbUser dbUser = (dbUser) getServletContext().getAttribute("dbuser");
        writer.println("<div>");
        writer.println("用户名："+dbUser.getUsername()+"<br>");
        writer.println("密码："+dbUser.getPassword()+"<br>");
        writer.println("</div>");
    }
}
```









## response     request

### response下载文件

```java
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取文件路径
        String file = "G:\\Downloads\\Web\\新建文本文档.txt";
        //2.下载的文件名是啥, 用一下技巧可以更便捷的获取文件名哦~  注意这就叫技术哦   \\表示为 '/'   +1就可以跳过'/'直接获取最后的字符串 也就是文件名
        String filename = file.substring(file.lastIndexOf("\\")+1);
        //3.设置浏览器头文件信息,以支持我们的下载功能                               转换字符串编码  将传入的字符串转换成另一种编码
        resp.setHeader("Content-Disposition","attachment;filename="+ URLEncoder.encode(filename,"UTF-8"));
        //4.获取文件下载流
        FileInputStream in = new FileInputStream(file);
        //5.设置缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
        //6.获取输出流对象
        ServletOutputStream out = resp.getOutputStream();
        //7.将文件输入流的数据 用 servlet输出流输出
        while((len=in.read(buffer))>0)
        {
            out.write(buffer,0,len);
        }
        in.close();
        out.close();
        
        //4,5,6,7 是很标准的一套缓冲区传输文件流的写法 注意记 不要在把 i/o里落下的东西往后拖了

    }
```

### response图片验证码

```java
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //告诉浏览器 我们每隔三秒刷新一次
        resp.setHeader("refresh","5");
        //在浏览器中 创建一个图片内存
        BufferedImage image = new BufferedImage(150,30,BufferedImage.TYPE_INT_RGB);
        //得到图片
        Graphics2D g = image.createGraphics(); //获得画笔
        g.setColor(Color.white);
        g.fillRect(0,0,150,30);

        g.setColor(Color.black);             //设置背景颜色
        g.setFont(new Font(null,Font.BOLD,24)); //设置字体 传进去一个字体 ,有字体的name,字体的样式,字体大小
        g.drawString(getpassword(),0,30);

        //下面就是对resp对象的操作了
        resp.setContentType("image/jpeg");//告诉浏览器 以图片的方式打开
        resp.setDateHeader("expires",-1); //告诉浏览器不要将图片保存到缓存空间
        resp.setHeader("Cache-control","no-cache");
        resp.setHeader("Pragma","no-cache");

        //把图片 写给浏览器
        ImageIO.write(image,"jpeg",resp.getOutputStream()); //图片文件 , 文件格式 , 一个输出流


    }
//获取验证码的函数
    private String getpassword(){
        Random num = new Random();
        String number = num.nextInt(99999999)+"";
        //如果随机数的长度小于8位数,那么会给sb补上0  直到有七位数大小   8-number.length() 表示少了几位
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < 8-number.length(); i++) {
            sb.append("0");
        }
        //这里将sb的字符串输出,在拼接上产生的随机数字符串,  就是一个八位字符串了     因为少了几位,在for循环里 就会给sb添加几位
        //不过我认为仍然不完美, 如果产生的随意数比八位大 那么程序就崩了,   如果比八位小, 那么随机数还会是那些数,缺少的位数补上的全是0,而不是随机数
        number = sb.toString()+number;
        return number;
    }
```

### response重定向

![image-20210604135837118](F:\图像\typora图像保存位置\image-20210604135837118.png)

```java
public class demo3 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        // sendRedirect 的内部实现原理
         resp.setHeader("Location","/s/getimage");
         resp.setStatus(HttpServletResponse.SC_MOVED_TEMPORARILY);
			//HttpServletResponse.SC_MOVED_TEMPORARILY=302
        //状态码 200 表示没问题
        //302表示 重定向 
        //400+ 表示 错误
        //500+ 表示 被墙了  网关

//        resp.sendRedirect("/s/getimage");
    }
}

```





### request处理请求

表头固定格式

==**<form action="${pageContext.request.contextPath}/login" method="post" >**==    

表单提交信息

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<body>
<h1>登录!</h1>
<div> <%--固定格式获取当前项目路径--%>
    <form action="${pageContext.request.contextPath}/login" method="post" >
        <input type="text" name="username"><br>
        <input type="password" name="password">
        <br>
        <input type="checkbox" name="hobbies" value="女人">洛丽塔
        <input type="checkbox" name="hobbies" value="穿女装的男孩">穿女装的男孩
        <input type="checkbox" name="hobbies" value="小裙子">小裙子
        <input type="checkbox" name="hobbies" value="女装">女装
        <br>
        <input type="submit">
    </form>

</div>
</body>
</html>

```

servlet处理信息, 处理成功则转到某页面, 失败转到某页面 下面例子默认成功

```java
//servlet实例
@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobbies = req.getParameterValues("hobbies");
    System.out.println("---------------------------");
    System.out.println(username);
    System.out.println(password);
    System.out.println(Arrays.toString(hobbies)); //如果直接hobbies.toString(),会输出第一个元素的地址  ,所以才要这么写
    System.out.println("---------------------------");

    req.getRequestDispatcher("/success.jsp").forward(req,resp);


}

---------------重定向到 成功页面.jsp------------
    <%--
  Created by IntelliJ IDEA.
  User: 炸毛
  Date: 2021/6/4
  Time: 13:15
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登陆成功</title>
</head>
<body>
<h1>欢迎来到可爱窝~</h1>
</body>
</html>

```

![image-20210604135848718](F:\图像\typora图像保存位置\image-20210604135848718.png)

### 转发请求

```java
req.getRequestDispatcher("/1").forward(req,resp);//实现转发
System.out.println(req.getAttribute("javax.servlet.forward,query_string")); //得到servlet转发过来的属性
System.out.println(req.getQueryString());//得到url栏中的属性
```





## Cookie

### 实现登录信息记录入cookie

```jsp
<%--填写登录信息页面--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<body>
<h1>登录!</h1>
<div> <%--固定格式获取当前项目路径 ,将表单数据发送给处理页面--%>
    <form action="${pageContext.request.contextPath}/cookiedemo2" method="get" >
        <input type="text" name="username"><br>
        <input type="password" name="password">
        <br>
        <input type="checkbox" name="hobbies" value="女人">洛丽塔
        <input type="checkbox" name="hobbies" value="穿女装的男孩">穿女装的男孩
        <input type="checkbox" name="hobbies" value="小裙子">小裙子
        <input type="checkbox" name="hobbies" value="女装">女装
        <br>
        <input type="submit">
    </form>

</div>
</body>
</html>

```

```java
//cookiedemo2  这个servlet负责处理表单信息 并制作成cookie 发送给显示页面
import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class CookieDemo2 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=UTF-8");

        //获取表达信息 ,添加到Cookie
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobbies = req.getParameterValues("hobbies");
        resp.addCookie(new Cookie("username",username));
        resp.addCookie(new Cookie("password",password));
        for (int i = 0; i < hobbies.length; i++) {
            resp.addCookie(new Cookie("hobbies"+i,hobbies[i]));
        }
        //重定向到输出页面
        req.getRequestDispatcher("/cookiedemo1").forward(req,resp);

    }
}
//cookiedemo1
import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class CookieDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=UTF-8");
        //注意这个 流的名字一定要叫  out
        PrintWriter out = resp.getWriter();
        Cookie[] cookies = req.getCookies();
        if(cookies!=null)
        {
            Cookie cookie;
            for (int i = 0; i < cookies.length; i++) {
                cookie=cookies[i];
                out.write(cookie.getName()+":"+cookie.getValue());
                out.print("<br>");

            }

        }else {
            out.write("你还未注册,请注册");
            resp.sendRedirect("/index.jsp");
        }


    }
}
```



## session

### 与cookie的不同

session存放在服务器中,  这里面的数据 是servlet共享的,  一个servlet中存储的数据,另一个可以取出来.

session可以存放对象数据, 一个cookie却只能存放一个键值对.

session创建了之后 只有用户关掉浏览器才会消失,

通过**session.invalidate();** 方法可以结束session的生命

也可以通过xml来设置 session的生命周期 

### 小demo

通过两个servlet 来验证 session是共享数据的

```java
//sevlet1   用来显示用户数据
package com.zhamao.sessien;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.io.PrintWriter;

public class sessiondemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");

        HttpSession session = req.getSession();


        PrintWriter out = resp.getWriter();
        if(session.isNew()){
            out.write("新session的id:"+session.getId());
        }else {
            out.write("session的id:"+session.getId());
        }
        out.print("<br>");
        User user = (User) session.getAttribute("user1");
        out.write(user.toString());
    }
}
//servlet2   用将用户数据存放servlet中
package com.zhamao.sessien;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;
import java.io.PrintWriter;

public class sessiondemo2 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");

        //获取表达信息 ,添加到Cookie
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobbies = req.getParameterValues("hobbies");

        HttpSession session = req.getSession();
        session.setAttribute("user1",new User(username,password,hobbies));

    }
}

```

这是用户类

```java
package com.zhamao.sessien;

import java.util.Arrays;

public class User {
    private String username;
    private String password;
    private String[] hobbies;

    public User(String username, String password, String[] hobbies) {
        this.username = username;
        this.password = password;
        this.hobbies = hobbies;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", hobbies=" + Arrays.toString(hobbies) +
                '}';
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String[] getHobbies() {
        return hobbies;
    }

    public void setHobbies(String[] hobbies) {
        this.hobbies = hobbies;
    }
}

```

### xml配置

```xml
    <session-config>
        <!--设置session刷新时长 以分钟为单位-->
        <session-timeout>15</session-timeout>
    </session-config>    

<servlet>
        <servlet-name>sessiondemo1</servlet-name>
        <servlet-class>com.zhamao.sessien.sessiondemo1</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>sessiondemo1</servlet-name>
        <url-pattern>/s1</url-pattern>
    </servlet-mapping>
    <servlet>
        <servlet-name>sessiondemo2</servlet-name>
        <servlet-class>com.zhamao.sessien.sessiondemo2</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>sessiondemo2</servlet-name>
        <url-pattern>/s2</url-pattern>
    </servlet-mapping>
```



### 提出问题

那么问题来了,  既然session的数据资源是共享的 ,那么怎么才能保证用户数据的安全呢???==session内部究竟是怎么区分你我他的呢???== 

因为当一个客户(浏览器)访问session时,   session会给他一个id 

![image-20210605192254028](F:\图像\typora图像保存位置\image-20210605192254028.png)

这个id1是在用户关闭浏览器后 或者 session刷新后  才会变更的,    session就是通过这个id能做到辨别用户的.

通过这个例子就很好理解

![image-20210605192402140](F:\图像\typora图像保存位置\image-20210605192402140.png)

可以看到两边的id不一样,所以 edge(用户1) 访问不到 谷歌(用户2)中的数据.

## JSP

### JSP依赖

```xml
    <!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl-api -->
    <dependency>
      <groupId>javax.servlet.jsp.jstl</groupId>
      <artifactId>jstl-api</artifactId>
      <version>1.2</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.apache.taglibs/taglibs-standard-impl -->
    <dependency>
      <groupId>org.apache.taglibs</groupId>
      <artifactId>taglibs-standard-impl</artifactId>
      <version>1.2.5</version>
    </dependency>
```



### 原理

![image-20210606124952787](F:\图像\typora图像保存位置\image-20210606124952787.png)

### 语法

![image-20210606135950156](F:\图像\typora图像保存位置\image-20210606135950156.png)



![image-20210606135914105](F:\图像\typora图像保存位置\image-20210606135914105.png)



![image-20210606140029919](F:\图像\typora图像保存位置\image-20210606140029919.png)

#### 全局变量

上面这些代码都会被写在一个 jspservler 的方法中,  那么我们如何去定义全局函数 全局变量呢

**<%!      %>** 没错 用这个标签就可以了 

#### 合并页面

```jsp
<jsp:include page="/common/footer.jsp"/>
```



![image-20210606151200942](F:\图像\typora图像保存位置\image-20210606151200942.png)



### 9大内置对象

- PageContext	存东西
- Request           存东西
- Response
- Session           存东西
- Application [ServletContext]   存东西
- config  [ServletConfig]
- out               输出流
- page           当前页面
- exception     





### EL表达式

#### 禁止在jsp中使用java代码 

我们可以在web.xml中这样配置 来达到禁止 java代码 的效果

```xml
  <jsp-config>
    <jsp-property-group>
      <url-pattern>*.jsp</url-pattern>
      <scriptting-invalid>
        true
      </scriptting-invalid>
    </jsp-property-group>
  </jsp-config>
```



#### jsp标准动作

这个标准动作 不属于Java脚本。

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <--这个<jsp:xxxxxx> 就是一个动作-->
<jsp:useBean id="propen" class="com.eight.javabean.propen" scope="request">
    <jsp:setProperty name="propen" property="name" value="张三"></jsp:setProperty>
    <jsp:setProperty name="propen" property="age" value="18"></jsp:setProperty>
</jsp:useBean>

<% propen p = (com.eight.javabean.propen) request.getAttribute("propen");%>
用户信息：<%= p.toString()%>  或者 <jsp:getproperty name="propen" property="name"></jsp:getproperty>
</body>
</html>
```

##### javabean

这个玩意儿呢， 就是jsp中的一个功能。    我们可以让这个 bean 变成任何一个类，自定义的也行。 这个功能要用下面几个标准动作来操作

```jsp
<jsp:useBean id="propen" class="com.eight.javabean.propen" scope="request">
    id= 实例化类的名字，也是这个实例 作为属性 的属性名   例： xxx。getAttrobute("propen"); 
    type && calss  =  type  ??= new class   .   这里的type可以是一个抽象类，也可以是一个具体类 。 class必须是具体类。并且这个具体类必须要有一个    无参无参无参！！构造函数。
    scope=  这个属性 将要存放到哪个位置。  req？ session？ context？？ page？？ 都可以
    
    <jsp:setProperty name="propen" property="name" value="张三"></jsp:setProperty>
    这个就会调用 name类的set “property”方法   值为 value内的值   等价于 propen.setname("张三");
    <jsp:setProperty name="propen" property="age" value="18" param=“xxxxx”></jsp:setProperty>
    这里是补充   因为我的 propen类的age 设置的是int类型   但是 这里面的 18 是个string  但是运行后并没有报错。
    说明容器会自动把 你的值， 转化成 类成员 对应的类型
    param等同于value  只不过 这个值 来源于   表单提交上来的参数。 
    <jsp:getproperty name="propen" property="name"></jsp:getproperty>
    等价于propen.getname();
</jsp:useBean>
```



**补充小技巧**

```jsp
 <jsp:getproperty name="propen" property="<%=  %>"></jsp:getproperty> 对没错 是可以这样子来调用jsp表达式的
```

```jsp
如果参数名 与 javabean中定义的类 的成员名一样   ，那么就不需要在 set 动作中 使用param字段，  不过你必须要保证  参数名 与成员变量名是一致的。
```

```jsp
如果我们想要这样写<jsp:setProperty name="propen" property="name" >   注意 这里取的是请求参数，上个小技巧中提到的那个。 
    			<jsp:setProperty name="propen" property="age" >
那么我们可以这样写                                property=“*”  ,     效果是一模一样
```















































## MVC架构

![image-20210610133318505](F:\图像\typora图像保存位置\image-20210610133318505.png)







## filter过滤器

### 在XML中配置filter

```xml
<filter>
    <filter-name>filter01</filter-name> 与servlet相似 filter名
    <filter-class>com.zhamao.filter.filter01</filter-class> 文件地址
  </filter>

  <filter-mapping>
    <filter-name>filter01</filter-name> filter名
    <url-pattern>/servlet01</url-pattern> 响应地址
      //响应地址意为:  当我们进入这个地址的servlet时 该过滤器才会启动
  </filter-mapping>
```

### filter概念

servlet 要对我们的数据进行处理,  那么如何保证 servlet要处理的数据 一定是合法 安全 规范的呢?   这就需要用到 我们的 filter   .  它的作用也很简单   就是在数据进入 servlet之前 接收输入  并对该数据进行过滤处理, 最后将合法安全的数据 交给servlet.   

当然了  你可以把filter理解为 一个 专门为了 过滤数据的servlet   ,只不过他不叫servlet 而是叫做  filter   并且 也不能在浏览器地址栏中 直接访问使用    必须访问特定的servlet时才会被调用.

filter在服务器启动时初始化 ,在服务器关闭时销毁.   





### 多个filter的调用顺序

一段信息 在进入 servlet之间  要经过 所有的filter 才行,   如果一个servlet 适配了多个filter 那么 会按照其在xml中的先后顺序  来依次进入.  如果其中 有某一个 filter没有调用 过滤器链方法  那么信息就会传递失败.



如果 使用注解 来注册 filter 那么我们就无法决定 filter的先后顺序.  所以我们要根据实际情况来使用合理的方法.



### filter的应用场景

![image-20210723223059232](F:\图像\typora图像保存位置\image-20210723223059232.png)



### 实例

```java
//servlet
@WebServlet("/servlet01")
public class servlet01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //这时 servlet接收到的req和resp 已经是经过过滤器处理过的数据   ,所以req.getParameter("user"),req.getParameter("textvox")已经不存在了.
        //2021年7月23日22:39:49 改正上面错误  不存在了只是我他吗 字母打错了   还存在    我们调用这个 get方法 只是从请求中 获取这个信息 获取到的是一个 新的String 而不是 请求里面的信息本体
        //至于如何对 请求中的本题进行修改 需要学习 另一个类 叫啥我忘了  哦哦 叫HttpServletRequestWrapper

        //不过相对应的 我们可以用 Attribute(); 来代替 Parameter    当然了 只是一种手段 PARAMETER中的值依然没有被改变
        resp.getWriter().write(req.getParameter("user")+":"+req.getAttribute("textbox"));

    }
}


//filter
@WebFilter("/servlet01")
public class filter01 implements Filter {


    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("filter01已初始化.");
    }
    //接收路径为 servlet01 的响应数据 并进行过滤
    @Override
    public void doFilter(ServletRequest Req, ServletResponse Resp, FilterChain Chain) throws IOException, ServletException {
        Req.setCharacterEncoding("utf-8");
        Resp.setCharacterEncoding("utf-8");
        Resp.setContentType("text/html;UFT-8");
        String str = null;
        str = new String(Req.getParameter("user")+":"+Req.getParameter("textbox"));
        str = "已发送.";
        Req.setAttribute("textbox",str);

        //将处理过的请求和响应传给 servlet01
        Chain.doFilter(Req,Resp);
    }

    @Override
    public void destroy() {
        System.out.println("filter01已销毁");
    }
}


```













## AJAX

简介:  AJAX就是异步传输     就是  在同一个页面中 我们的请求在等待回应的同时 可以继续做其他操作.



ajax不是一门语言 而是一种 编程思想 一种技术.  这种技术 通过 jQuery来实现





### 注意事项

当我们用 post提交时  一定要附带参数  否则将会提交失败 并 报500错误.



如果我们要使用 ajax这门技术 时   就不能 用  <form>表单来提交数据了.   因为使用表单提交数据会自动刷新页面. 这违背了 ajax的核心思想.







































# MyBatis

## pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.zhamao</groupId>
    <artifactId>mybatis</artifactId>
    <version>1.0-SNAPSHOT</version>


<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.47</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
    <dependency>
        <groupId>org.mybatis</groupId>
        <artifactId>mybatis</artifactId>
        <version>3.5.6</version>
    </dependency>

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.22</version>
    <scope>provided</scope>
</dependency>


</dependencies>

    <!--读取该路径下 指定文件名-->
    <!--我们用这样的形式来约束maven 让他读取资源目录下的 该后缀文件. -->
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.xml</include>
                <include>**/*.properties</include>
            </includes>
        </resource>

    </resources>
    <!--maven约束JDK版本  此处为 jdk11-->
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.7.0</version>
            <configuration>
                <release>11</release>
            </configuration>
        </plugin>
    </plugins>
</build>



</project>
```



## 练习数据

```sql
CREATE DATABASE yggl
use yggl
CREATE TABLE `departments` (
`DepartmentID`  char(3) NOT NULL COMMENT '部门编号' ,
`DepartmentName`  char(20) NOT NULL COMMENT '部门名' ,
`Note`  text NULL DEFAULT NULL COMMENT '备注' ,
PRIMARY KEY (`DepartmentID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO departments VALUES ('1', '财务部', null),
('2', '人力资源部', null),
('3', '经理办公室', null),
('4', '研发部', null),
('5', '市场部', null);



CREATE TABLE `employees` (
`EmployeeID`  char(6) NOT NULL ,
`Name`  char(10) NOT NULL ,
`Education`  char(4) NOT NULL ,
`Birthday`  date NOT NULL ,
`Sex`  char(2) NOT NULL ,
`WorkYear`  tinyint(1) NULL DEFAULT NULL ,
`Address`  varchar(20) NULL DEFAULT NULL ,
`PhoneNumber`  char(12) NULL DEFAULT NULL ,
`DepartmentID`  char(3) NOT NULL ,
PRIMARY KEY (`EmployeeID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO employees 
VALUES ('000001', '王林', '大专', '1966-01-23', '1', '8', '中山路32-1-508', '83355668', '2'),
('010008', '伍容华', '本科', '1976-03-28', '1', '3', '北京东路100-2', '83321321', '1'),
('020010', '王向容', '硕士', '1982-12-09', '1', '2', '四牌楼10-0-108', '83792361', '1'),
('020018', '李丽', '大专', '1960-07-30', '0', '6', '中山东路102-2', '83413301', '1'),
('102201', '刘明', '本科', '1972-10-18', '1', '3', '虎距路100-2', '83606608', '5'), 
('102208', '朱俊', '硕士', '1965-09-28', '1', '2', '牌楼巷5-3-106', '84708817', '5'),
('108991', '钟敏', '硕士', '1979-08-10', '0', '4', '中山路10-3-105', '83346722', '3'),
('111006', '张石兵', '本科', '1974-10-01', '1', '1', '解放路34-1-203', '84563418', '5'), 
('210678', '林涛', '大专', '1977-04-02', '1', '2', '中山北路24-35', '83467336', '3'),
('302566', '李玉珉', '本科', '1968-09-20', '1', '3', '热和路209-3', '58765991', '4'),
('308759', '叶凡', '本科', '1978-11-18', '1', '2', '北京西路3-7-52', '83308901', '4'), 
('504209', '陈林琳', '大专', '1969-09-03', '0', '5', '汉中路120-4-12', '84468158', '4');



CREATE TABLE `salary` (
`EmployeeID`  char(6) NOT NULL COMMENT '员工编号' ,
`InCome`  float NOT NULL COMMENT '收入' ,
`OutCome`  float NOT NULL COMMENT '支出' ,
PRIMARY KEY (`EmployeeID`)
)ENGINE=INNODB DEFAULT CHARSET=utf8;


INSERT INTO salary 
VALUES ('000001', '2100.8', '123.09'),
('010008', '1582.62', '88.03'),
('020010', '2860', '198'),
('020018', '2347.68', '180'),
('102201', '2569.88', '185.65'),
('102208', '1980', '100'),
('108991', '3259.98', '281.52'),
('111006', '1987.01', '79.58'),
('210678', '2240', '121'),
('302566', '2980.7', '210.2'),
('308759', '2531.98', '199.08'),
('504209', '2066.15', '108');

```



## 结构

### 结构图

![image-20211211232952495](F:/图像/typora图像保存位置/image-20211211232952495.png)

### 结构思想

与javaweb中的结构相似, 但是在mybatis中  用 mapper 取代了dao层.   从返回结果来看二者功能一致,不过是过程不同.  总而言之,mybatis确实避免了大量的重复的 jdbc代码 使的jdbc的使用更加便捷 实用.  

同样的我们用 接口来定义方法,  **不过我们不需要再写实现接口的实现类** 这一切将由 MyBatis来进行.  我们只需要 配置好 mapper.xml.   将对应的 类路径给对,  方法名给对 sql 语句写对就行了. 





## 配置文件

### mybatis-config.xml(含解析)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!-- 根标签 -->
<configuration>
    !-- 读取properties文件  在下面的事务管理器中 可以获取文件中的键值对 下面只是其中一种写法 peroperties标签内 还有更多的功能 如果只是读取文件的话 做到这一部就可以了 -->
<!--    <properties resource="db.properties"/>-->
<!--其内部的标签可以当做一个键值对来看待 name属性 对标  事务管理器中的 value属性-->
    <properties resource="db.properties">
        <property name="aaa" value="123456"/>
    </properties>

<!--
    <typeAlias>
    类型别名可为 Java 类型设置一个缩写名字。 它仅用于 XML 配置，意在降低冗余的全限定类名书写。
    这里的别名只可以使用在  <mapper>下的CRDB子标签中的 resultType="employees" 中.
    mapper映射路径 是不可以使用别名来代替的
    <package>
    我们也可以给 包 起别名  然后 在mapper 中 就可以直接使用 实体类名 来封装  一般我们在实体类多的时候这么用.
    我们也可以用 注解@Alias("")来给实体类起别名.

    每一个在包 domain.blog 中的 Java Bean，在没有注解的情况下，会使用 Bean 的首字母小写的非限定类名来作为它的别名。
    比如 domain.blog.Author 的别名为 author；若有注解，则别名为其注解值。

    例如：
-->
    <typeAliases>
<!--        <typeAlias alias="departments" type="com.zhamao.pojo.departments"/>-->
<!--        <typeAlias alias="employees" type="com.zhamao.pojo.employees"/>-->
<!--        <typeAlias alias="salary" type="com.zhamao.pojo.salary"/>-->
<!--        <typeAlias alias="employeesMapper" type="com.zhamao.mapper.employeesMapper"/>-->
        <package name="com.zhamao.pojo"/>
    </typeAliases>
    
    
    <!-- 环境，可以配置多个，default：指定采用哪个环境 -->
    <environments default="test">
        <!-- id：唯一标识 -->
        <environment id="test">
            <!-- 事务管理器，JDBC类型的事务管理器
 				还有另一个 MANAGED 这种类型的管理器 不会有提交或回滚的操作 默认情况下它会关闭连接 如果想要阻止
                    <property name="closeConnection" value="false"/>
                请这么设置

			-->
            <transactionManager type="JDBC" />
            <!-- 数据源，池类型的数据源  有三种内建的数据源类型（也就是 type="[ UNPOOLED | POOLED | JNDI ]"） -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver" />
                                <!--在这里我们仍要注意,SSL安全认证设置为false,除非我们做了相关配置. 否则就会爆出org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database  导致我们的sql语句无法正常执行 -->
                <property name="url" value="jdbc:mysql://127.0.0.1:3306/yggl?useSSL=false&amp;useUnicode=true&amp;characterEncoding=utf-8&amp;" />

                <property name="username" value="root" />
                <property name="password" value="123456" />
            </dataSource>
        </environment>

    </environments>
    <!--注册Mapper文件,-->
    <mappers>
        <mapper resource="com/zhamao/mapper/employeesMapper.xml"/>
        <mapper resource="com/zhamao/mapper/departmentsMapper.xml"/>
        <mapper resource="com/zhamao/mapper/salaryMapper.xml"/>
    </mappers>
</configuration>
```



### mapper.xml(CRUD)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- mapper:根标签，namespace：这里要写接口的路径,文件中sql语句 执行的主体类是在项目中的哪个位置.-->
<mapper namespace="com.zhamao.mapper.salaryMapper">
    <!-- statement，内容：sql语句。id：主体类方法名
       resultType：sql查询结果返回值,
     -->
    <select id="getSalary" resultType="com.zhamao.pojo.salary">
        select EmployeeID,inCome,OutCome from yggl.salary
    </select>
    <!--parameterType: 传参类型 -->
    <select id="getEmployeesByID" parameterType="String" resultType="com.zhamao.pojo.employees" >
        select * from yggl.employees where EmployeeID = #{EmployeeID}
    </select>
	<!--要注意的点: 这里传参类型为实体类, 所以我们在接口中传的参数也应该为对应的实体类
		int addEmployee(employees emp);
		如果我们的参数类型为一个实体类的话,
		我们可以直接使用 实体类中的参数,  只要名字与属性名相匹配就行.
	-->
    <!--最最应该注意的是, 在mybatis中 所有的增删改 都是在事务中进行的, 所以我们在执行完 sql语句后 要记得在java代码中提交事务,
        //提交事务
        sqlSession.commit();
    -->
    <insert id="addEmployee" parameterType="com.zhamao.pojo.employees">
        INSERT INTO employees
            value (#{EmployeeID},#{Name},#{Education},#{Birthday},#{Sex},#{WorkYear},#{Address},#{PhoneNumber},#{DepartmentID});
    </insert>

</mapper>
```



### db.properties

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/yggl?useSSL=false&useUnicode=true&characterEncoding=utf-8
username=root
password=123456
```

















## ***构建项目流程

1.导包   pxm.xml

2.配置 jdbc链接  db.properties      

3.配置文件 , mybatis-config.xml  并配置  **事务管理器** 

4.编写工具类.mybatisUtils.java

```java
package com.zhamao.utils;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;

public class MybatisUtils{
    private static SqlSessionFactory sqlSessionFactory;
    static{
        try {
            String resource = "mybatis-config.xml";
            InputStream inputStream =  Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        }catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }


}
```



5.编写实体类, 实体类与表对标

6.编写 mapper接口,

7.编写Mapper.xml, 并将 Mapper.xml与对应的mapper绑定

8.在 config中 映射 Mapper.xml文件

9.编写测试类.

```java
public void testGetStudent(){
    SqlSession sqlSession = MyBatisUtils.getSqlSession();//获取sqlsession
    System.out.println(sqlSession.getMapper(StudentMapper.class).getStudent(1)); //通过sqlsession.getMapper()来获取Mapper接口中的信息.
}
```

















## 一些技巧及设计思想

### 传参对象与map的区别

```xml
<!--传参为对象, 好处是 我们可以 从对象属性中 获取想要的值,不需要传递一大堆不同类型的对象.
	
	坏处是, 我们在做修改或者别的操作时,  很多时候我们只修改 一个字段,  如果这个实体类有一百个属性 而我们又只需要一个或者几个
	时就会非常棘手.
-->
	<insert id="addEmployee" parameterType="com.zhamao.pojo.employees">
        INSERT INTO employees
            value (#{EmployeeID},#{Name},#{Education},#{Birthday},#{Sex},#{WorkYear},#{Address},#{PhoneNumber},#{DepartmentID});
    </insert> 

<!-----------------------分割线----------------------------------------->
<!--map就是为了解决这个比较棘手的问题,  避免我们必须要传递对象的尴尬之处.   通过键值对 我们可以模拟出 对象中  属性:值  的
	情况.  key为 属性名,value为 值.  有了这个我们甚至可以不需要实体类. 	
-->
	<insert id="addEmployee" parameterType="map">
        INSERT INTO employees
            value (#{EmployeeID},#{Name},#{Education},#{Birthday},#{Sex},#{WorkYear},#{Address},#{PhoneNumber},#{DepartmentID});
    </insert>
```





### 为什么实体类属性名要与表字段名一致

MyBatis中有一个类型处理器. 这个处理器会自动把 select 后面的字段    当做实体类中的属性名  来赋值.

比如

```java
class user{
	id;
	name;
	password;
}

select id,name,pwd from user
我们可以这么想象  类加载器  调用了 user的构造器  来给 user的id属性 name属性 以及 pwd属性赋值.  
但是我们的实体类中 并没有pwd属性,我们有的是password属性   所以最后构建出来的 user类 的password值为null
```

我们可以通过 给字段起别名的 方法来解决该问题  

```sql
select id,name,pwd as password from user
```

但我们可以想象到 这么做会很麻烦,应该存在更加牛逼的方案才对.

### resultMap(接上文)

```xml
 <resultMap id="起map名" type="映射对象(实体类)">
      <result column="字段名" property="实体类属性名"/>
</resultMap>
```









### 分页( limit )

为什么使用分页?		加快查找速度,减少一次性处理的数据量.   例如 电商网站 商品有**页一样.

```sql
select * from employees limit 0,5;        (第一个参数起始下标,第二个参数查找容量)
```

与增删改查的思维逻辑是一样的 不过是sql语句不一样罢了.   

同样的我们需要给这个select标签两个参数.    使用 map类型.       











下面两种 原理还是 limit 不过是使用方式不同 ,了解即可

![image-20211213142048374](F:/图像/typora图像保存位置/image-20211213142048374.png)

![image-20211213142103523](F:/图像/typora图像保存位置/image-20211213142103523.png)



![image-20211213141956573](F:/图像/typora图像保存位置/image-20211213141956573.png)















### 使用注解来代替xml

```java
public interface employeesMapper {
    @Select("select * from employees")
    List<employees> getEmployees();
//当我们只需要使用一些简单的sql时, 我们可以使用注解来进行开发,  可以节省开发时间.    使用注解开发的一大好处就是,不需要在配置mapper.xml文件.  这一切都会由注解类来进行配置.      
    /**当然注解开发也有他的弊端,  在mapper中 我们有各种各样的 数据类型 传参类型,以及起别名等等操作来 让我们的结构逻辑更清晰.   当 实体类属性名 与 表字段名不一致时 也可以顺利获取想要的数据.     这是 注解开发所做不到的.
    */
    
}

```

最重要的我们是要了解  注解是如何做到  在不配置xml 的情况下  , 清楚地知道 我们的方法名, 返回值类型. 传参,  已经类的路径的.   

答案是  通过反射机制.     

```java
        SqlSession sqlSession = MyBatisUtils.getSqlSession();
        //读取mapper的class文件
        employeesMapper employeesMapper = sqlSession.getMapper(employeesMapper.class);
		//这里我们通过反射  把mapper类 返回给了 sqlSession.  sqlSession通过强大的反射机制, 来获取 这个类的一系列信息.  包括我们的 类路径,方法名,返回值,传参等等.
        List<employees> arrayList = employeesMapper.getEmployees();
```

教学老师 提到了  这个注解开发 的本质是  **动态代理**     动态代理我还没学,**静态代理请移步**  java高级  设计模式来复习.    



动态代理是一种设计模式,  而注解开发 则是  用反射机制 来实现了 这一种设计模式.









#### **CRUD**以及@Param("")

![image-20211213152935935](F:/图像/typora图像保存位置/image-20211213152935935.png)

![image-20211213153054127](F:/图像/typora图像保存位置/image-20211213153054127.png)

#### #{}  和${}的区别

#{}是预编译的  可以预防 sql注入

${}是字符串拼接的可以被 sql注入















## 一些对象的生命周期

### SqlSessionFactoryBuilder

创建SqlSessionFactory后就不再使用了.

### SqlSessionFactory

创建后 理应一直存在  是一个生产sqlSession的工厂.

### SqlSession

每一个线程 都应有一个 sqlsession    会话嘛  想想javaweb中的session.   







## 日志

### 环境搭建

```xml
<!--mybatis-config.xml-->

<!--设置 用来设置一些功能 比如日志的版本  这里设定日志系统为 log4j    
	2021年12月13日13:56:13
	近期log4j2  也就是 log4j的升级版 出现了巨大漏洞. 可以通过sql注入来远程连接服务器  被部分 mc服务器服主们发现并上传b站.
	SLF4J | LOG4J | LOG4J2(bug) | JDK_LOGGING | COMMONS_LOGGING | STDOUT_LOGGING(mybatis自带) | NO_LOGGING(不选择日志)
-->

    <settings>
        <setting name="logImpl" value="LOG4J"/>
    </settings>


<!--pom.xml-->
<!--导入jar包  日志系统有很多 有的是mybatis自带的. 这种的不需要导包 在setting中配置一下即可使用. 但是一些外来的日志系统需要进行导包.-->

    <!-- https://mvnrepository.com/artifact/log4j/log4j -->
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.17</version>
    </dependency>

```



### 配置文件    log4j.properties

```properties
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置

log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out			
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/sqllog.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```





























## 一对多查询

### 按照结果嵌套处理(多表查询)

```xml
  <!--按照结果嵌套处理-->
    <select id="getAllStudent" resultMap="getAllStudent2">
        select s.id sid,s.name sname,t.name tname from student s,teacher t where s.tid = t.id
    </select>

    <resultMap id="getAllStudent2" type="Student">
        <!--property代表在实体类中属性名    column 在sql语句中的字段对应的 名字       -->
        <result property="id" column="sid"/>
        <result property="name" column="sname"/>
<!--    association  代表这个属性是一个对象类型     javaType 它在java代码中的 数据类型  该实例为  Teacher类
        association  可以进行子标签嵌套.
     -->
        <association property="teacher" javaType="Teacher">
            <result property="name" column="tname"/>
        </association>
    </resultMap>
```





### 按照查询嵌套处理(子查询)

```xml
<!--根据查询嵌套处理,   子查询    查询结果中的对象的信息, 其实是通过另一条 简单查询语句查到的信息来获取的.
    两条查询语句属于从属关系,   子语句中的 where判定条件  可以从父语句中返回的信息中获取
    拿本实例来讲  select * from student   的第三个字段为 tid   是老师的id
    而 select * from teacher where id = #{tid} 中  where的 id = ?    这个?  就是 上面那条查询语句中获取的 tid 的值.
-->
    <select id="getAllStudent2" resultMap="getAllStudent1">
        select id,name,tid from student
    </select>
    <select id="getTeacher" resultType="Teacher">
        select id,name from teacher where id = #{id}
    </select>
    <resultMap id="getAllStudent1" type="Student">
<!--            property代表在实体类中属性名    column 在sql语句中的字段对应的 名字       -->
        <result property="id" column="id"/>
        <result property="name" column="name"/>
        <!--    association 当association作为一个闭合标签时,其内部的property="" column="" 代表的是 父sql    select="" 该属性才代表 子sql
             -->
        <association property="teacher" column="tid" javaType="Teacher"  select="getTeacher"/>
    </resultMap>
```

为了方便理解 多配一张图

![image-20220108235341906](F:\图像\typora图像保存位置\image-20220108235341906.png)	确实符合猜想

![image-20220108235450508](F:/图像/typora图像保存位置/image-20220108235450508.png)















## 多对一查询

### java

```java
public class Teacher {
    private int id;
    private String name;
    private List<Student> students;
}
-----------------------------------------------------------------------------------------
public interface TeacherMapper {
    public Teacher getTeacherAllStudent(@Param("id") int id);
}
```

### xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zhamao.dao.TeacherMapper">

    <select id="getTeacherAllStudent" resultMap="getTeacherAllStudent">
        select t.id tid,t.name tname,s.name sname from teacher t,student s where t.id = #{id} and s.tid = t.id
    </select>

    <resultMap id="getTeacherAllStudent" type="Teacher">
        <result property="id" column="tid"/>
        <result property="name" column="tname"/>
<!--    当查询结果集中 包含 集合 这一数据结构时  ,我们用collection 来设置集合信息   collection标签 规范类型 不使用 javaType=""属性
        使用 ofType=""来设置  集合中 泛型的规范.    比如当前实例collection标签  代表实体类 teacher中的  List<Student>类型.
        按照往常的理解 我们可能会用javaType="Student" , 甚至javaType="List<Student>"来表达.    但是 ofType="Student" 才是正确的表达方式.
-->     <collection property="students" ofType="Student">
            <result property="name" column="sname"/>
        </collection>
        
    </resultMap>
</mapper>
```









































## 动态sql拼接

### 什么是动态sql

动态 SQL 是 MyBatis 的强大特性之一。如果你使用过 JDBC 或其它类似的框架，你应该能理解根据不同条件拼接 SQL 语句有多痛苦，例如拼接时要确保不能忘记添加必要的空格，还要注意去掉列表最后一个列名的逗号。利用动态 SQL，可以彻底摆脱这种痛苦。

使用动态 SQL 并非一件易事，但借助可用于任何 SQL 映射语句中的强大的动态 SQL 语言，MyBatis 显著地提升了这一特性的易用性。

如果你之前用过 JSTL 或任何基于类 XML 语言的文本处理器，你对动态 SQL 元素可能会感觉似曾相识。在 MyBatis 之前的版本中，需要花时间了解大量的元素。借助功能强大的基于 OGNL 的表达式，MyBatis 3 替换了之前的大部分元素，大大精简了元素种类，现在要学习的元素种类比原来的一半还要少。

- if
- choose (when, otherwise)
- trim (where, set)
- foreach







### 环境搭建

1.表

```sql
CREATE TABLE `blog`(
`id` VARCHAR(50) NOT NULL COMMENT '博客id',
`title` VARCHAR(100) NOT NULL COMMENT '博客标题',
`author` VARCHAR(30) NOT NULL COMMENT '博客作者',
`create_time` DATETIME NOT NULL COMMENT '创建时间',
`views` INT(30) NOT NULL COMMENT '浏览量'
)ENGINE=INNODB DEFAULT CHARSET=utf8
```

2.新的工具类(id生成器)

```java
public class IdUtils {
    public static String getId(){
        return UUID.randomUUID().toString().replace("-","");
    }

}
```

3.插入数据

```java
@Test
public void test(){
    SqlSession sqlSession = MybatisUtils.getSqlSession();
    BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);

    mapper.addBlog(new Blog(IdUtils.getId(),"我的教导主任","炸毛",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"我是扩阴器","炸毛",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"哼,想逃?闪电旋风劈","尻比",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"啊对对对","王喜顺",new Date(),2000));
    mapper.addBlog(new Blog(IdUtils.getId(),"我最后一瓶甜水","梁潇",new Date(),2000));

    sqlSession.commit();
    sqlSession.close();
}
```





### 动态sql的好处

可以减少创建重复的sql语句, 我们可以像在 jsp中使用 动作一样.  在xml中 使用标签 来达到 动态拼接sql语句的效果, 这样可以达到 一条sql语句, 实现多种查询,     通俗来讲 就是    把    重写sql    给智能化了

里面的 <if></if>  标签的语法 一看就能明白 就不解释了.

```xml
<select id="getBlog" parameterType="map" resultType="Blog">
    select title,author,create_time,views from blog where 1=1
    <if test="title != null">
        and title = #{title}
    </if>
    <if test="author != null">
        and author = #{author}
    </if>
</select>
```



着重解释一下 该sql语句中的    where 1=1   .    

![image-20220109195739321](F:\图像\typora图像保存位置\image-20220109195739321.png)



### <  where> 结合上文 对 where的理解

原来   where 1=1 只是缓兵之计.  开发者们早已想到并解决了这个问题

where标签 会  识别拼接条件 是否是 第一个   如果是的话   会自动把 句首的 and去掉. 

```xml
<select id="getBlog" parameterType="map" resultType="Blog">
    select title,author,create_time,views from blog
    <where>
        <if test="title != null">
            and title = #{title}
        </if>
        <if test="author != null">
            and author = #{author}
        </if>
    </where>
</select>
```

### 一些动态sql标签

1.choose、when、otherwise  (switch ) 

​	选择语句   when条件 .   无符合条件时执行otherwise  

```xml
<select id="findActiveBlogLike"
     resultType="Blog">
  SELECT * FROM BLOG
  <where>
    <if test="state != null">
         state = #{state}
    </if>
    <if test="title != null">
        AND title like #{title}
    </if>
    <if test="author != null and author.name != null">
        AND author_name like #{author.name}
    </if>
  </where>
</select>
```

2.set   (updata set  (sql语句))    会自动去除最后一条语句中的  ,   所以放心大胆的写.

```xml
<update id="updateAuthorIfNecessary">
  update Author
    <set>
      <if test="username != null">username=#{username},</if>
      <if test="password != null">password=#{password},</if>
      <if test="email != null">email=#{email},</if>
      <if test="bio != null">bio=#{bio}</if>
    </set>
  where id=#{id}
</update>
```





3.foreach

![image-20220111141543156](F:/图像/typora图像保存位置/image-20220111141543156.png)













## Sql 片段

在 Mapper.xml中 使用使用 < sql>标签

![image-20220111134434998](F:/图像/typora图像保存位置/image-20220111134434998.png)









## 缓存

缓存的作用就是,将查到的数据,暂时存放到内存中,以减少连接数据库对资源的消耗. 

一般我们只有哪些,经常需要查询, 并且不经常修改的数据才会放到缓存中. 

**注意** 缓存不存在于数据库.

缓存分为一级缓存和二级缓存.





基本上就是这样。这个简单语句的效果如下:

- 映射语句文件中的所有 select 语句的结果将会被缓存。
- 映射语句文件中的所有 insert、update 和 delete 语句会刷新缓存。
- 缓存会使用最近最少使用算法（LRU, Least Recently Used）算法来清除不需要的缓存。
- 缓存不会定时进行刷新（也就是说，没有刷新间隔）。
- 缓存会保存列表或对象（无论查询方法返回哪种）的 1024 个引用。
- 缓存会被视为读/写缓存，这意味着获取到的对象并不是共享的，可以安全地被调用者修改，而不干扰其他调用者或线程所做的潜在修改。





![image-20220111173740620](F:/图像/typora图像保存位置/image-20220111173740620.png)





### 一级缓存

一级缓存是默认开启的, 也关闭不掉.      

当我们的两次查询中 穿插了 增删改 等操作时,缓存也会被清理. 

![image-20220111151556564](F:/图像/typora图像保存位置/image-20220111151556564.png)









### 二级缓存

![image-20220111172900532](F:/图像/typora图像保存位置/image-20220111172900532.png)

### 自定义缓存(Ehcache)

