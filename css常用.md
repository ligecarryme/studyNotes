```html
<span> // 文字
```

```css
display:flax;
justitfy-content: space-between; //两端
```

### header：

<img src="E:\学习笔记\前端\img\QQ截图20200915214225.png" style="zoom:67%;" />

<img src="E:\学习笔记\前端\img\QQ截图20200915214333.png" style="zoom:67%;" />

```css
border-radius: 3px;	//圆角		//元素居中 方式一
position: absolute;   
left: 50%
top: 50%
transform: translate(-50%, -50%)

margin-top:auto;     //方式二
margin-left:auto;
```

```css
box-sizing: border-box; // padding和border被包含在定义的width和height之内。 		
content-box; // 默认值，不被包含在定义的width和height中
```

### 布局属性

#### position

指定一个元素（静态的，相对的，绝对或固定）的定位方法的类型。
属性值  https://www.runoob.com/cssref/pr-class-position.html

#### display 

属性规定元素应该生成的框的类型。

`display:flex` 是一种布局方式。它即可以应用于容器中，也可以应用于行内元素。

> Flex是Flexible Box的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。

详情  https://www.jianshu.com/p/d9373a86b748/

#### float

设置对象浮动（left、right）

```css
float: right; //浮动在右侧
```

