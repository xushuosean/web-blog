# CSS布局之居中

### 本文主要是介绍水平居中，垂直居中，还有水平垂直居中的方法

### 水平居中

1.**行内元素水平居中**
		使用text-align:center;就可以实现行内元素的水平居中，但是记得要在父元素中设置，会对子元素生效。此方法对，**inline、inline-block、inline-table、inline-flex**都有效。

```css
.parent{
  text-align:center;
}
```

​		此外，如果块级元素包着一个块级元素，**那么我们可以设置外部盒子text-align:center;给内部盒子设置display:inline-block;**这样也可以使得内部元素居中。但要注意的是，内部盒子已经设置了display:inline-block，就不可以再设置其他的display，**所以最好不要使用这种方法。**

```html
<div class="parent">
	<div class="child">
	</div>
</div>			//下面会沿用这个html结构
<style>
	.parent{
	text-align:center;
	}
	.child{
	display:inline-block
	}
</style>
```

2.**块级元素水平居中**

**使用margin居中**

​		margin：0 auto;但是使用这种方法，要记得给元素设置宽度，否则不会生效

```html
.child{
	width:200px;
	marign:0 auto;
}
```

**使用absolute+transform**

```html
.parent{
	position:relative;
}
.child{
	position:absolute;
	left:50%;
	transform:translate(-50%);
}
```

​		**absolute**定位，左 50%，然后使用**transform**向左移动50%；

3.**浮动元素水平居中**

- 已知宽度，通过子元素设置relative+负margin

  ```html
  .child{
  	width:200px;
  	float:left;
  	position:relative;
  	left:50%;
  	margin:-100px;
  }
  ```

- 未知宽度，父子元素都用相对定位

  ```
  .parent{
  	float:left;
  	postion:relative;
  	left:50%;
  }
  .child{
  	float:left;
  	position:relative;
  	right:50%;
  }
  ```

  父元素相对于左定位50%；且因为，父元素的宽度是由子元素撑起来的，所以当子元素相对于自身右定位50%时，水平居中

  **示例**
  		**当我们把child的定位取消时**

  ![屏幕快照 2019-08-21 下午9.17.25](/Users/sean/Documents/Typora/images/屏幕快照 2019-08-21 下午9.17.25.png)

  ​	**打开child的相对定位时**

  ![屏幕快照 2019-08-21 下午9.17.38](/Users/sean/Documents/Typora/images/屏幕快照 2019-08-21 下午9.17.38.png)

  4.**绝对定位元素水平居中**
  		这种方式通过子元素的绝对定位，外加margin:0 auto;

  ```html
  .parent{
  	position:relative;
  }
  .child{
  	postion:absolute;
  	width:100px;
  	height:100px;
  	background:red;
  	margin:0 auto;
  	left:0;
  	right:0;
  }
  ```



### 垂直居中

1.**单行内联元素垂直居中**
这种方法适合对单行文本的垂直居中，比如应用在顶部菜单栏中

```html
.parent{
	height:100px;
	line-height:100px;
}
```

2.**块级元素垂直居中**

​		使用absolute+负margin

```html
.parent{
	position:relative;
}
.child{
	height:100px;
	position:absolute;
	top:50%;
	margin-top:-50px;
}
```

​		使用absolute+tranform

```
.parent{
	position:relative;
}
.child{
	position:absolute;
	top:50%;
	transform:translateY(-50%);
}
```

### 水平垂直居中

​		可以参考上面的水平居中和垂直居中的方法，结合起来就可以了。