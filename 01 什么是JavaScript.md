## 什么是JavaScript

### 1.1 JavaScript的历史

略

### 1.2 JavaScript实现

JavaScript和ECMAScript通常被用来表达一样的含义。但是它们之间并不是相等的关系。一个完整的 JavaScript 实现应该由下列三个不同的部分组成：
- 核心（ECMAScript）
- 文档对象模型（DOM） 
- 浏览器对象模型（BOM）


#### 1.2.1 ECMAScript

ECMAScript就是对实现该标准（ECMA-262标准）规定的各个方面内容的语言的描述。JavaScript实现了 ECMAScript，Adobe ActionScript同样也实现了 ECMAScript。 目前来说最新的标准就是ECMA-262第10版。

#### 1.2.2 DOM

文档对象模型（DOM，Document Object Model）是针对 XML但经过扩展用于HTML的应用程序编程接口（API，Application Programming Interface）。DOM通过创建表示文档的树，让开发者可以随心所欲地控制网页的内容和结构。使用 DOM API，
可以轻松地删除、添加、替换、修改节点。 

#### 1.2.3 BOM

Internet Explorer 3和 Netscape Navigator 3有一个共同的特色，那就是支持可以访问和操作浏览器窗口的浏览器对象模型（BOM，Browser Object Model）。开发人员使用BOM可以控制浏览器显示的页面
以外的部分。而BOM真正与众不同的地方（也是经常会导致问题的地方），还是它作为 JavaScript实现
的一部分但却没有相关的标准。这个问题在HTML5中得到了解决，HTML5致力于把很多BOM功能写入正式
规范。HTML5发布后，很多关于BOM的困惑烟消云散。

### 小结

JavaScript是一门用来与网页交互的脚本语言，包含以下三个组成部分。 
- ECMAScript：由 ECMA-262定义并提供核心功能。 
- 文档对象模型（DOM）：提供与网页内容交互的方法和接口。 
- 浏览器对象模型（BOM）：提供与浏览器交互的方法和接口。 