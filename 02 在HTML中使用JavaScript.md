## 在 HTML 中使用 JavaScript


### 2.1 `<script>`元素 
向 HTML页面中插入JavaScript的主要方法，就是使用`<script>`元素。

在使用`<script>`元素嵌入JavaScript代码时，只须为`<script>`指定 type属性（已废弃，可不指定）。然后，像下面这样把JavaScript代码直接放在元素内部即可： 
 

```
<script type="text/javascript"> 
    function sayHi(){  
        alert("Hi!"); 
    } 
</script>
```

注意，`type`是可选属性，只有这个值是`module`的时候，代码会被当成ES6模块，只有这个时候代码中才能出现`import`和`export`关键字。

#### 2.1.1 标签的位置 

按照传统的做法，所有`<script>`元素都应该放在页面的<head>元素中。这种做法的目的就是把所有外部文件（包括 CSS文件和JavaScript文件）的引用都放在相同的地方。可是，在文档的`<head>`元素中包含所有JavaScript文件，意味着必须等到全部JavaScript代码都被下载、解析和执行完成以后，才能开始呈现页面的内容（浏览器在遇到`<body>`标签时才开始呈现内容）。对于那些需要很多 JavaScript代码的页面来说，这无疑会导致浏览器在呈现页面时出现明显的延迟，而延迟期间的浏览器窗口中将是一片空白。为了避免这个问题，**现代Web应用程序一般都把全部JavaScript引用放在`<body>`元素中页面内容的后面**。

#### 2.1.2 延迟脚本 


HTML 4.01为`<script>`标签定义了`defer`属性。这个属性的用途是表明脚本在执行时不会影响页面的构造。也就是说，脚本会被延迟到整个页面都解析完毕后再运行。因此，在`<script>`元素中设置`defer`属性，相当于告诉浏览器立即下载，但延迟执行。 


```
<!DOCTYPE html> 
<html> 
  <head> 
    <title>Example HTML Page</title> 
    <script type="text/javascript" defer="defer" src="example1.js"></script> 
    <script type="text/javascript" defer="defer" src="example2.js"></script> 
  </head> 
  <body> 
    <!-- 这里放内容 --> 
  </body> 
</html>
```

#### 2.1.3 异步脚本

HTML5为`<script>`元素定义了`async`属性。这个属性与 `defer` 属性类似，都用于改变处理脚本的行为。同样与 `defer` 类似，`async`只适用于外部脚本文件，并告诉浏览器立即下载文件。但与`defer`不同的是，标记为 `async` 的脚本并不保证按照指定它们的先后顺序执行。例如：

```
<!DOCTYPE html> 
<html>   
  <head> 
    <title>Example HTML Page</title> 
    <script type="text/javascript" async src="example1.js"></script> 
    <script type="text/javascript" async src="example2.js"></script> 
  </head> 
  <body> 
    <!-- 这里放内容 --> 
  </body> 
</html>
```
注意，好的web开发方法不推荐使用这个方法。

#### 2.1.4 动态加载脚本

除了`<script>`标签，还有其他方式可以加载脚本。因为 `JavaScript`可以使用 DOM API，所以通过
向 DOM中动态添加 script 元素同样可以加载指定的脚本。只要创建一个 `script` 元素并将其添加到
DOM即可。 
```
let script = document.createElement('script'); 
script.src = 'gibberish.js'; 
document.head.appendChild(script); 
```

#### 2.1.5 XHTML中的变化

可扩展超文本标记语言（XHTML，Extensible HyperText Markup Language）是将 HTML作为 XML
的应用重新包装的结果。与 HTML 不同，在 XHTML 中使用 JavaScript 必须指定 `type` 属性且值为
`text/javascript`，HTML 中则可以没有这个属性。
```
<script type="text/javascript">  
  function compare(a, b) { 
    if (a < b) { 
      console.log("A is less than B"); 
    } else if (a > b) { 
      console.log("A is greater than B"); 
    } else { 
      console.log("A is equal to B"); 
    } 
  } 
</script> 
```

例如上述代码，在XHTML规则中不可行，因为`<`会被解析成标签的开始，解决方法是把其更换成`&lt;`。不过这种方法会影响阅读，也可以把其放在`CDATA`板块中，格式如下：
```
<script type="text/javascript"><![CDATA[ 
  function compare(a, b) {  
    if (a < b) { 
      console.log("A is less than B"); 
    } else if (a > b) { 
      console.log("A is greater than B"); 
    } else { 
      console.log("A is equal to B"); 
    } 
  } 
]]></script> 
```

在兼容 XHTML的浏览器中，这样能解决问题。但在不支持 CDATA块的非 XHTML兼容浏览器中
则不行。为此，CDATA标记必须使用 JavaScript注释来抵消： 
```
<script type="text/javascript">  
//<![CDATA[ 
  function compare(a, b) { 
    if (a < b) { 
      console.log("A is less than B"); 
    } else if (a > b) { 
      console.log("A is greater than B"); 
    } else { 
      console.log("A is equal to B"); 
    } 
  } 
//]]> 
</script> 
```

### 2.2 嵌入代码与外部文件 

推荐使用外部文件，其优点：
- 可维护性
- 可缓存
- 适应未来

### 2.3 文档模式

略

### 2.4 `<noscript>`元素

 
`<noscript>`元素可以包含任何可以出现在`<body>`中的 HTML元素，`<script>`除外。在下列两种
情况下，浏览器将显示包含在`<noscript>`中的内容： 
- 浏览器不支持脚本； 
- 浏览器对脚本的支持被关闭。 

任何一个条件被满足，包含在`<noscript>`中的内容就会被渲染。否则，浏览器不会渲染`<noscript>`
中的内容。 
```
<!DOCTYPE html> 
<html>  
  <head> 
  <title>Example HTML Page</title> 
  <script defer="defer" src="example1.js"></script> 
  <script defer="defer" src="example2.js"></script> 
  </head> 
  <body> 
  <noscript> 
    <p>This page requires a JavaScript-enabled browser.</p> 
  </noscript> 
  </body> 
</html> 
```

这个例子是脚本不可用时让浏览器显示一段话。如果浏览器支持脚本，则用户看不到他。

### 2.5 小结

- 要包含外部 JavaScript文件，必须将 src 属性设置为要包含文件的 URL。文件可以跟网页在同
一台服务器上，也可以位于完全不同的域。 
- 所有`<script>`元素会依照它们在网页中出现的次序被解释。在不使用 `defer` 和 `async` 属性的
情况下，包含在`<script>`元素中的代码必须严格按次序解释。 
- 对不推迟执行的脚本，浏览器必须解释完位于`<script>`元素中的代码，然后才能继续渲染页面的剩余部分。为此，通常应该把`<script>`元素放到页面末尾，介于主内容之后及`</body>`标签之前。 
- 可以使用 `defer`属性把脚本推迟到文档渲染完毕后再执行。推迟的脚本原则上按照它们被列出的次序执行。 
- 可以使用 `async`属性表示脚本不需要等待其他脚本，同时也不阻塞文档渲染，即异步加载。异步脚本不能保证按照它们在页面中出现的次序执行。 
- 通过使用`<noscript>`元素，可以指定在浏览器不支持脚本时显示的内容。如果浏览器支持并启用脚本，则`<noscript>`元素中的任何内容都不会被渲染。 