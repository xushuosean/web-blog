# GET和POST两种基本请求方法的区别



#### 面试回答:

**长度限制**：GET请求在URL中传送的参数是有**长度限制**的，而POST没有;

**安全性**：GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息;

**参数**：GET参数通过URL传递，POST放在Request body中;

**保留问题**：GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留;

**编码方式**：GET请求只能进行url编码，而POST支持多种编码方式;

**Cache**：GET请求会被浏览器主动cache，而POST不会，除非手动设置;

**回退**：GET在浏览器回退时是无害的，而POST会再次提交请求。

#### 深入:

**1.GET和POST是什么？有无区别？**

GET和POST本质上并没有区别，只是HTTP协议中的两种发送请求的方法； 

**2.HTTP是什么？**

**HTTP**是基于**TCP/IP**的关于数据如何在万维网中如何通信的协议。

 HTTP的底层是TCP/IP。所以GET和POST的底层也是TCP/IP，也就是说，GET/POST都是TCP链接。

GET和POST能做的事情是一样的。你要给GET加上request body，给POST带上url参数，技术上是完全行的通。

那么，“标准答案”里的那些区别是怎么回事？

**举例:**

TCP协议是面向连接的，可靠交付的，因此使用TCP协议可以保证数据的有效传输。

我们可以将TCP比作是车，而GET和POST则分别为小货车和大货车，他们都可以传送物品，但是如果不加以限制，超过了载重量，就很可能导致交通系统的瘫痪。

为了避免这种情况的发生，交通规则——HTTP诞生了，这就区分了汽车的种类及他们的载重量，于是GET和POST就被区分开来了。

HTTP规定，当执行GET请求时，要给小货车设置GET的标签（设置method为GET），而且要求把传送的货物（数据）用绳子绑在车顶（URL）上以便查看。

如果是POST请求，就要给大货车设置POST标签（设置method为POST），并把货物放在车厢里。

如果是POST请求，就要在车上贴上POST的标签，并把货物放在车厢里。

HTTP只是个行为准则，而TCP才是GET和POST怎么实现的基本。

但是，我们只看到HTTP对GET和POST参数的传送渠道（url还是requrest body）提出了要求。那么关于参数大小的限制又是从哪来的呢？

在网络世界中，还有另一个重要的角色：物流公司。

不同的浏览器（发起http请求）和服务器（接受http请求）就是不同的运输公司。

虽然理论上，你可以在车顶上无限的堆货物（url中无限加参数）。但是运输公司可不傻，装货和卸货也是有很大成本的，他们会限制单次运输量来控制风险，数据量太大对浏览器和服务器都是很大负担。

业界不成文的规定是，（大多数）浏览器通常都会限制url长度在2K个字节，而（大多数）服务器最多处理64K大小的url。

当然，你也可以在GET的时候往车厢内偷偷藏点货物，但是这是很不光彩；也可以在POST的时候在车顶上也放一些数据，让人觉得傻乎乎的。

超过的部分，恕不处理。如果你用GET服务，在request body偷偷藏了数据，不同服务器的处理方式也是不同的，有些服务器会帮你卸货，读出数据，有些服务器直接忽略。

所以，虽然GET可以带request body，也不能保证一定能被接收到哦。

好了，现在你知道，GET和POST本质上就是TCP链接，并无差别。但是由于HTTP的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。

### 重大区别

GET和POST还有一个重大区别。

简单的说：

GET产生一个TCP数据包；POST产生两个TCP数据包。

复杂的说：

对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据）；

而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。

### 但是！！！

也就是说，GET只需要汽车跑一趟就把货送到了，而POST得跑两趟，第一趟，先去和服务器打个招呼“嗨，我等下要送一批货来，你们打开门迎接我”，然后再回头把货送过去。

因为POST需要两步，时间上消耗的要多一点，看起来GET比POST更有效。因此Yahoo团队有推荐用GET替换POST来优化网站性能。但这是一个坑！跳入需谨慎。为什么？

1. GET与POST都有自己的语义，不能随便混用。

2. 据研究，在网络环境好的情况下，发一次包的时间和发两次包的时间差别基本可以无视。而在网络环境差的情况下，两次包的TCP在验证数据包完整性上，有非常大的优点。

3. 并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次。