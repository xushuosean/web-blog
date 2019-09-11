# this的指向问题

## 一、this初识

this是javascript中最复杂的机制之一。它尤为特殊，被自动定义在所有函数的作用域中。这篇文章将浅析this与函数的关系。

## 二、了解this

学习this的第一步就是明白this既不指向自身也不指向函数本身的词法作用域，而是指向当前行为的执行者，即：哪个函数调用函数，函数里面的this就指向哪个对象。

## 三、this指向

this的指向要分以下五种情况：

- 普通函数
- 自执行函数
- 事件绑定
- 构造函数
- call、apply和bind

------

### 1、普通函数

```javascript
function fn(){
  console.log(this);
}
fn();
```

> 此时，fn()执行，实际上是window.fn();此时this指向window

```javascript
function fn(){
  console.log(this);
}
var obj = {fn:fn,name:"sean"};
obj.fn();
```

> 此时，使用obj调用fn()，此时this指向obj

### 2、自执行函数

```javascript
(function(){
  console.log(this)
})();
```

> 此时，this指向window

再看下面这个代码

```javascript
var name = "gary";
function fn() {
    console.log(this.name);
    (function(){
         console.log(this.name)
     })();
}
var obj = { fn: fn, name: "sean" };
obj.fn();
```

> 此时控制台输出

![thisTest01](https://github.com/xushuosean/web-blog/blob/master/images/thisTest01.png)

> 所以，自调用函数的this指向永远指向window

### 3、事件绑定

- DOM零级事件

```javascript
oBtn.onclick = function(){
  console.log(this);				//this->oBtn
}
```

- DOM二级事件

```javascript
oBtn.addEventListener("click",function(){
	console.log(this);				//this->oBtn
})
```

### 4、构造函数

```javascript
function Test(name,age){
  this.name = name;
  this.age = age;
  this.print = function(){
    console.log(this.name + " " + this.age);
  }
}
var t = new Test("sean",22);
t.print();
```

> 此时，构造函数中的this，指向的是t这个实例，也就是说，哪个实例执行，this就指向谁

### 5、call、apply和bind

这一部分在我另一篇文章里，详情戳[这里](https://github.com/xushuosean/web-blog/blob/master/js/call%E3%80%81apply%E3%80%81bind%E7%9A%84%E7%94%A8%E6%B3%95.md)

------

#### 参考文章

------

[你还没懂this？](https://github.com/ljianshu/Blog/issues/7)

[javascript中this的指向问题](https://www.cnblogs.com/chengxs/p/8679313.html)

