# call、apply、bind的用法

call、apply、bind的作用是为了改变函数运行时this的指向

this就是当前行为执行的主体

### call

call函数传入两个参数，第一个参数为对象，第二个及后面的参数用来传参。当第一个参数的列表为null或undefined时，默认指向window

```
var arr = [1, 2, 3, 4, 5];
var max = Math.max.call(null, arr[0], arr[1], arr[2], arr[3], arr[4])//89
```

Eg:

```javascript
var obj = {
  message:"My name is:"
}

function getName(firstName,lastName){
  console.log(this.message + fisrtName + " " + lastName);
}

getName.call(obj,"Dot","Dolby");
```

### apply

apply函数同样接收两个参数，第一个参数是要绑定的this的值，第二个参数是一个参数数组。当第一个参数为null、undefined的时候，默认指向window

```javascript
var arr = [1, 2, 3, 89, 46];
var max = Math.max.apply(null,arr);
```

> apply传入的多个参数，会依次作为形参进入函数中，比如max函数无法处理一个数组，但却可以同时处理多个参数，这样就可以调用了。看看下面的例子

Eg:

```javascript
var obj = {
	message:"My name is:"
}
function getName(firstName,lastName){
  console.log(this.message,firstName + " " + lastName);
}
getNmae.apply(obj,["Dot","Dolby"]);
```

### bind

bind函数也可以传入多个参数，指向要绑定的this的值。但值得注意的是，bind不会直接执行。需要使用括号调用才可以

Eg:

```javascript
				 var obj = {
            msg: "this is a message"
        }
        function getName() {
            console.log(this.msg)
        }

        getName.bind(obj)();
```

> 如果我们只用getName.bind(obj);是不会被调用的，只是绑定了this

