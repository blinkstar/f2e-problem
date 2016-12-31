## 字符串操作方法

下面介绍与操作字符串有关的几个方法。

<span style="color: red;font-weight: bold">第一个就是 concat() ，用于将一或多个字符串拼接起来，返回拼接得到的新字符串。</span>
先来看一个例子。

    var stringValue = "hello ";
    var result = stringValue.concat("world");
    console.log(result);          // "hello world"
    console.log(stringValue);     // "hello"

在这个例子中，通过 stringValue 调用 concat() 方法返回的结果是 "hello world" --
但 stringValue 的<span style="color: red;font-weight: bold">值则保持不变。</span>

实际上， concat() 方法可以接受任意多个参数，也就是说可以通过它拼接任意多个字符串。再来看一个例子：

    var stringValue = "hello ";
    var result = stringValue.concat("world", "!");

    console.log(result);        // "hello world!"
    console.log(stringValue);   // "hello"

这个例子将 "world" 和 "!" 拼接到了 "hello" 的末尾。虽然 concat() 是专门用来拼接字符串的方法，但实践中使用更多的还是加号操作符 (+)。
而且，使用加号操作符在大多数情况下都比使用 concat() 方法要简便易行 (特别是在拼接多个字符串的情况下)。


<span style="color: red;font-weight: bold">ECMAScript 还提供了三个基于子字符串创建新字符串的方法：slice()、substr() 和 substring()。</span>

这三个方法都会返回被操作字符串的一个子字符串，而且也都接受<span style="color: red;font-weight: bold">一或两个参数</span>。

第一个参数指定子字符串的开始位置，第二个参数(在指定的情况下)表示子字符串到哪里结束。    