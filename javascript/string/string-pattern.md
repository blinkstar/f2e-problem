## 字符串的模式匹配方法

String 类型定义了几个用于在字符串中匹配模式的方法。

### 1. 第一个方法就是 match()

在字符串上调用这个方法，本质上与调用 RegExp 的 exec() 方法相同。match() 方法只接受一个参数，要么是一个正则表达式，要么是一个 RegExp
对象。来看下面的例子。

    var text = "cat, bat, sat, fat";
    var pattern = /.at/;

    // 与 pattern.exec(text) 相同
    var matches = text.match(pattern);
    console.log(matches.index);         // 0
    console.log(matches[0]);            // "cat"
    console.log(pattern.lastIndex);     // 0

本例中的 match() 方法返回了一个数组：如果是调用 RegExp 对象的 exec() 方法并传递本例中的字符串作为参数，那么也会得到与此相同的数组：
数组的第一项是与整个模式匹配的字符串，之后的每一项 (如果有) 保存着与正则表达式中的捕获组匹配的字符串。

