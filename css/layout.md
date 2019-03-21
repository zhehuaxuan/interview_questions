## Position有哪几种？他们有什么特点？

postion有四种relative，absolute，static，fixed

**static（默认）**

不脱离文档流，按照正常文档流进行排列；
**relative（相对定位）**

不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；
**absolute(绝对定位)**

脱离文档流，参考距其最近一个不为static的父级元素通过top, bottom, left, right 定位；
**fixed(固定定位)**

脱离文档流，所固定的参照对像是可视窗口。

Tips❓:什么是脱离文档流？脱离文档流就是脱离按照浏览器解析的DOM布局顺序，然后对于display:block的元素，元素会变成内联。

## CSS实现元素水平垂直居中？

首先元素分类：内联+块状

**内联样式：**

```html
<div id="outer">
    <span>居中我吧</span>
</div>
```

```css
#outer{
    height:100px;
    <!-- 垂直居中 -->
    line-height:100px; 
    <!-- 水平居中 -->
    text-align:center;
}
```

**块状样式：**

第一种实现方法*Flex布局*：

```html
<div id="outer">
   <div id="inner">
       居中我吧
    </div>
</div>
```

```css
#outer {
    height:400px;
    width:400px;
    border:1px solid #ccc;
    display: flex;
    <!-- 水平居中 -->
    justify-content: center; 
    <!-- 垂直居中 -->
    align-items: center;
}
#inner{
    width:100px;
    height:100px;
    background:red;
}
```

第二种实现方法*相对布局*：

```css
#outer {
   height: 400px;
   width: 400px;
   border: 1px solid #ccc;
   position: relative;
}

#inner {
   width: 100px;
   height: 100px;
   background: red;
   position: absolute;
   left: 50%;
   top: 50%;
   transform: translateX(-50%) translateY(-50%);
}
```

## BFC（**块级格式化上下文：block formatting context**）

**什么是**BFC?

BFC就是块级格式化上下文，它**是一个独立的渲染区域**，规定了块级元素了里面的所有元素都会在里面进行布局，不会影响外面的布局

**满足什么样的条件就是**BFC?

> 1. 根元素，即HTML元素
> 2. float的值不为none
> 3. overflow的值不为visible
> 4. display的值为inline-block、table-cell、table-caption
> 5. position的值为absolute或fixed　

**BFC有什么特点？**

> 1. 内部的Box会在垂直方向上一个接一个放置。
> 2. Box垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的margin会发生重叠。
> 3. 每个元素的margin box 的左边，与包含块border box的左边相接触。
> 4. BFC的区域不会与float box重叠。
> 5. BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
> 6. 计算BFC的高度时，浮动元素也会参与计算。

**作用：**

> 1. 自适应两栏布局
> 2. 可以阻止元素被浮动元素覆盖
> 3. 可以包含浮动元素——清除内部浮动
> 4. 分属于不同的BFC时可以阻止margin重叠

### 4. CSS的伪类和伪元素

CSS里面有哪些常见的伪类？哪些常见的伪元素？他们有什么区别？对应有什么作用？

**伪类更多定义状态**。常见的伪类有：:hover，:active，:focus，:visited，:link，:not，:first-child，:last-child

伪类应用场景：

1.表单验证

2.折叠面板

3.元素的index

**伪元素，不存在于DOM树中的虚拟元素，它们可以像正常的html元素一样定义css，但无法使用JavaScript获取**。常见伪元素有 ::before，::after，::first-letter，::first-line等等。

CSS3规定伪类使用**:**，伪元素使用**::** （都可以使用:，为了区别CSS3进行了规范）

伪元素的应用场景：

1.根据::befer和::after在元素的前面和后面添加东西

2.美化选中的文本

```html
<p>Custom text selection color</p>
```

```css
::selection {
    color: red;
    background-color: yellow;
}
```



### 5. CSS实现一个正方形和一个三角形

**正方形：**

```html
<div id="square"></div>
```

```css
#square{
    width:0px;
    height:0px;
    border:50px solid red;
    box-sizing: content-box;
}
```

上述实现一个边长为100px的正方形。

**三角形:**

```html
<div id="triangle"></div>
```

```css
 #triangle {
            width: 0;
            height: 0;
            border-top: 40px solid transparent;
            border-left: 40px solid transparent;
            border-right: 40px solid transparent;
            border-bottom: 40px solid #ff0000;
            box-sizing: content-box;
}
```

### 6. 实现一个外圈半径为10px，内圈半径为5px的双圆环

```html
<div id="circle"></div>
```

```css
#circle{
	width:10px;
    height:10px;
    border:5px solid red;
    border-radius: 10px;
    box-sizing: content-box;
}
```

### 怎么实现三列布局（左侧和右侧宽度固定，中间自适应），什么是圣杯布局，什么是双飞燕布局？







### 移动端开发Rem布局的原理？包括px，em，rpn的区别和应用场景？







### 如何在界面上实现一个圆？

svg

canvas

border-radius

background

map+area

直接放一张圆形图片

### 假如现在页面里放在head的css文件下载速度很慢，页面会出现什么情况？

### 假如我现在在页面动态添加了一个CSS文件，页面一定会回流吗？

例如页面这个CSS文件中有translate3d呢？
那假如我在页面里面加了一个<div style="position:absolute;width:0;hegiht:0"></div>呢，会回流吗
CDN的原理是啥？

