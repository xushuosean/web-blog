# DOM操作（基础版）

DOM是document Object Model的缩写，简称文档对象模型。只要记住这是操作文档的就行了。

![](https://github.com/xushuosean/web-blog/blob/master/images/dom1.png)

### DOM基础选择器

1、**getElementById(id);**				//获取指定的id元素

2、**getElementsByClassName(class);**				//通过class获取元素，返回值是数组

3、**getElementsByTagName(p);**					//获取相同标签的节点列表，返回值是数组

4、**getElementsByName(name);**						//获取相同元素的节点列表，返回数组

**⚠️注**：不是所有的标签都有name值。

**⚠️注**：空格和换行键是文本标签

#### 强大的selector

document.querySelectorAll();

var oD = document.querySelector();			
		oD.childNode							//获取当前元素节点的所有子节点，返回一个数组

​		oD.parentNode						//获取当前元素节点的父元素，返回一个元素	

> class选择器返回的是数组对象，如果要使用其中的元素，通过索引解析出来
>
> selector会选择第一个符合规则的元素，selectorAll返回一个数组

### 节点选择器

（节点）关系选择器：都是属性，而不是方法
		父选子

```javascript
omsg.children							//返回一个数组
```

​		子选父

```javascript
omsg.parentNode
```

​		第一个子

```javascript
omsg.firstElementChild
```

​		最后一个子

```javascript
omsg.lastElementChild
```

​		上一个兄弟

```javascript
omsg.previousElementSibling
```

​		下一个兄弟

```javascript
omsg.nextElementSibling
```

### 元素属性节点的操作分类

​		属性的操作：

#### 1、作为属性操作：

#### **可见的操作**：

- 内置：系统提供，按照对象的操作方法进行操作

  可**获取**，可**设置**				***对属性进行操作***

  ```javascript
  console.log(obox.title);
  obox.title = "123321";
  console.log(obox.className);				//只能通过className,而不能通过class，因为class是个关键字
  ```

- 非内置：自定义，不可以通过对象的方法进行操作，通过专属方法

  get/set/romove-Attribute();				***对自定义的属性进行操作***

  **获得、设置、溢出**

  以上三种方法也可以操作内置对象，如果通过这三种方法操作class，直接写class就可以，因为class在此时，是一个字符串

  ```
  obox.getAttribute("class");
  ```

  #### 不可见的操作：

  内置：							***对内部内置属性进行操作***

  innerHTML

  nodeName

  nodeValue

  nodeType

  ```javascript
  obox.innerHTML;				//会返回标签及内容
  obox.innerText;				//只返回文本的内容
  obox.tagName;					//只能返回，不能操作
  
  ```

  非内置：对象的操作，直接写入对象内			***对新增自定义的属性进行操作***

  ```javascript
  obox.abc = "123456";
  console.log(obox.abc);
  
  ```

  可以只分为**内置属性**和**非内置属性**。除了已经定义在标签内部的非内置属性，其他的都按**点**调用。而标签内部的非内置属性使用get/set/romove-Attribute();调用。

#### 2、作为属性节点：（专用方法，与其他节点的方法不互通）

​		**attributes**							***会返回一个数组***

```javascript
<div class="box" a="10" b=20></div>
var obox = document.querySeloector(".box");
console.log(obox.attributes);
//获取属性节点的节点的属性和属性值
console.log(obox.attributes[0].nodeName);
console.log(obox.attributes[0].nodeValue);

```

***obox本身也就是元素节点***

```javascript
obox.nodeName;				//节点名称--文本是#text，
obox.nodeValue;				//节点值--文本是值
obox.nodeType;				//节点类型--属性节点为2，元素节点为1，文本是3？？？

```

|          | 节点类型(nodeType) | 节点名字(nodeName) | 节点值(nodeValue) |
| :------: | :----------------: | :----------------: | :---------------: |
| 元素节点 |         1          |       标签名       |       null        |
| 文本节点 |         3          |       #text        |       文本        |
| 注释节点 |         8          |      #comment      |    注释的文字     |
| 文档节点 |         9          |     #document      |       null        |
| 属性节点 |         2          |       属性名       |      属性值       |

**只要是节点，就是对象**

```
nodeName;			//名称
nodeValue;		//值
nodeType;			//类型

```

**节点属性**

**伪数组：假数组**

​		可以使用索引和长度遍历，但是不能使用数组的方法
​		arguments也是伪数组
​		DOM选择器返回的数组也是伪数组

真数组：

​		可以使用索引和长度遍历，但是可以使用数组的方法

操作style

​	批量操作.cssText

### DOM属性基本操作（**增/删/改/查**）

#### DOM元素的增加

**创建**：

```javascript
createElement();				//需要配合下面这个函数使用
appendChild();					//将创建好的元素插入某个标签内的最后
```

> ⚠️注：是插入到某个标签**内**的**最后**

**使用方法**：

```html
<div class="box" a="10" b=20 id="box" title="divTitle">
			<p>这是一个测试文本...</p>
  		<span>ssss</span>
  		<span>aaaa</span>
</div>
```

```javascript
var obox = document.getElementById("box");
var e = document.createElement("input");
e.value = "name";
obox.appendChild(e);
```

**删除**：

```javascript
obox.removeChild(e);						//删除obox内的e元素
obox.remover();									//直接删除当前元素
```

**修改**：

```javascript
var a = obox.lastElementChild;
a.outerHTML = "<p>" + a.innerHTML + "</p>";
```

### 非行内样式的操作

```javascript
getcomputedStyle(obox,false)						//获取样式，只能获取不能设置
```

```javascript
getcomputedStyle(obox,false).background;
```

获取非行内样式（**兼容问题**）

```javascript
    function getStyle(obj,attr){             //获取非行间样式，obj是对象，attr是值
        if(obj.currentStyle){                //针对ie获取非行间样式
            return obj.currentStyle[attr];
        }else{
            return getComputedStyle(obj,false)[attr];   //针对非ie
        };
    };
```

**获取元素尺寸类样式**

| 名称                     | 描述                                                       |
| ------------------------ | ---------------------------------------------------------- |
| offsetParent             | 获取元素最近的具有定位属性的父级元素。如果都没有则返回body |
| offsetLeft               | 获取元素相对具有定位属性的父级元素的左侧偏移距离           |
| offsetTop                | 获取元素相对具有定位属性的父级元素的顶部偏移距离           |
| scrollLeft/scrollTop     | 滚动条最顶端和窗口中可见内容最顶端之间的距离--滚动距离     |
| clientWidth/clientHeight | 元素视窗宽度/高度                                          |
| offsetWidth/offsetHeight | 元素实际宽度/高度—*可以用来测量元素在网页中实际的宽高*     |

### 事件

```html
<div class="box"> 
</div>
```

```javascript
var obox = document.querySelector(".box");

obox.onclick = function(){
  console.log(1);
}
```

**事件源**：obox，触发事件的源头

```javascript
e.target
```

事件类型：onclick，通过什么行为触发

事件处理函数：function，触发这个行为时，要做的事情

### **事件的分类：**

| 事件分类     | 描述   |
| ------------ | ------ |
| onclick      | 单击   |
| ondblclick   | 双击   |
| onmousedown  | 按下   |
| onmousemove  | 移动   |
| onmouseover  | 放上去 |
| onmouseout   | 离开   |
| onmouseup    | 抬起   |
| onmouseenter | 进入   |
| onmouseleave | 离开   |

onmouseleave和onmouseenter不支持事件冒泡

**表单事件分类：**

| 表单事件分类 | 描述               |
| ------------ | ------------------ |
| onsubmit     | 提交               |
| onfocuse     | 获得焦点           |
| onblur       | 失去焦点           |
| onchange     | 改变文本区域的内容 |

页面事件分类

| 页面事件分类 | 描述     |
| ------------ | -------- |
| onload       | 加载完成 |

事件对象：类似于一个秘书，在本次实践过程中，记录事件发生的所有信息

默认不显示，需要手动获取

只在事件中存在，开始前及结束后，都不存在

### 获取事件对象

**event获取方法**

```javascript
window.event;					//IE中
eve										//直接获取
```

兼容方法

```javascript
function fn(eve){
  var e = eve || window.event;
}
```

⚠️注：event需要逐层传递，不要漏掉外部的function

**event的使用**

```javascript
e.button;								//返回按下鼠标按键的返回值，左0，中1，右2
e.clientX;
e.clientY;							//检测相对于浏览器的位置
e.pageX;
e.pageY;								//检测相对于文档的位置
e.screenX;
e.screenY;							//检测相对于屏幕的位置
e.offsetX;
e.offsetY;							//检测相对于元素左上角的位置
```

![](https://github.com/xushuosean/web-blog/blob/master/images/dom2.png)

------

冒泡事件：会依次向上触发**所有父级**的**相同事件**，如果中间没有父级，则继续向上触发

### 键盘事件

事件源：**document**

| 键盘事件   | 描述       |
| ---------- | ---------- |
| onkeydwon  | 键盘按下   |
| onkeyup    | 键盘抬起   |
| onkeypress | 按下并抬起 |

**事件对象**

获得事件对象：event

获得事件对象兼容

```javascript
var e = eve || window.event;
```

获得keycode

```javascript
var keyC = eve.keyCode || eve.which
```

**事件流**

三个阶段：

- 冒泡阶段：从里向外
- 目标（当前事件）阶段
- 捕获阶段：从外向内

只有事件监听才可以进入捕获，目标状态不区分捕获和冒泡

浏览器默认冒泡

```javascript
obox.addEventListener("click",function(){},flase);
```

第三个值默认为false

**事件委托**

将多个相同元素的相同事件，添加到页面上现存的共同的父元素，利用事件冒泡，配合事件源，找到真正点击的元素

```javascript
oul.onclick = function(eve){
             var e = eve || window.event;
             var target = e.target || e.srcElement;
             if(target.nodeName == "LI"){
                 console.log(target.innerHTML);
             }
         }
```

**优势**

1. 节省性能
2. 可一个页面上暂时不存在的元素绑定事件

**缺点**

1. this不够精准

事件委托的封装，可以使用this

```javascript
var oul = document.querySelector("ul");
		var oli = document.getElementsByTagName("li");
		oul.onclick = fn(oli,function(){
			console.log(this);
			console.log(this.innerHTML)
		})
		function fn(child,callback){
			return function(eve){
				var e = eve || window.event;
				var target = e.target || e.srcElement;
				for(var i = 0;i<child.length;i++){
					if(target == child[i]){
						callback.bind(target)();
					}
				}
			}
		}
```

