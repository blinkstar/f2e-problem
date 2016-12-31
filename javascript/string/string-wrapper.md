# String 包装类型

String 类型是字符串的对象包装类型，可以像下面这样使用 String 构造函数来创建。

    var stringObject = new String("hello world");

String 对象的方法也可以在所有基本的字符串值中访问到。其中，继承的 valueOf()、toLocaleString() 和 toString() 方法，都返回对象所表示
的基本字符串值。

String 类型的每个实例都有一个 <span style="color: red;font-weight: bold">length 属性</span>，表示字符串中包含多少个字符。来看下面的例子。

    var stringValue = "hello world";
    alert(stringValue.length);  // "11"

这个例子输出了字符串 "hello world" 中字符数量，即 "11" 。应该注意的是，即使字符串中包含双字节字符 (不是占一个字节的 ASCII 字符)，每个
字符也仍然算一个字符。

String 类型提供了很多方法，用于辅助完成对 ECMAScript 中字符串的解析和操作。

## 1 字符方法

两个用于访问字符串中特定<span style="color: red;font-weight: bold">字符</span>的方法是：<span style="color: red;font-weight: bold">chartAt() 和 charCodeAt() 。</span>
这两个方法都接收一个参数，即基于 0 的字符位置。其中，charAt() 方法以单字符字符串的形式返回给定位置的那个字符 (ECMAScritp 中没有字符类型)。例如：

    var stringValue = "hello world";
    console.log(stringValue.charAt(1)); // "e"

字符串 "hello world" 位置 1 处的字符是 "e" ，因此调用 charAt(1) 就返回了 "e" 。

如果你想得到的不是字符而是<span style="color: red;font-weight: bold">字符编码</span>，那么就要像下面这样使用 charCodeAt() 了。

    var stringValue = "hello world";
    console.log(stringValue.charCodeAt(1));    // 输出 "101"

这个例子输出的是 "101" ，也就是小写字母 "e" 的字符编码。

ECMAScript 5 还定义了另一个访问个别字符的方法。在支持的浏览器中，可以使用方括号加数字索引来访问字符串中的特定字符，如下面的例子所示。

    var stringValue = "hello world";
    console.log(stringValue[1]);  // "e"

使用方括号表示法访问个别字符的语法得到了 IE8 及 Firefox、Safari、Chrome 和 Opera 所有版本的支持。如果是在 IE7 及更早版本中使用这种
语法，会返回 undefined 值 (尽管根本不是特殊的 undefined 值)。
