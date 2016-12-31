## 字符串操作方法

下面介绍与操作字符串有关的几个方法。

### <span style="color: red;font-weight: bold">第一个就是 concat() ，用于将一或多个字符串拼接起来，返回拼接得到的新字符串。</span>

先来看一个例子。

    var stringValue = "hello ";
    var result = stringValue.concat("world");
    console.log(result);          // "hello world"
    console.log(stringValue);     // "hello "

在这个例子中，通过 stringValue 调用 concat() 方法返回的结果是 "hello world" --
但 stringValue 的<span style="color: red;font-weight: bold">值则保持不变。</span>

实际上， concat() 方法可以接受任意多个参数，也就是说可以通过它拼接任意多个字符串。再来看一个例子：

    var stringValue = "hello ";
    var result = stringValue.concat("world", "!");

    console.log(result);        // "hello world!"
    console.log(stringValue);   // "hello "

这个例子将 "world" 和 "!" 拼接到了 "hello" 的末尾。虽然 concat() 是专门用来拼接字符串的方法，但实践中使用更多的还是加号操作符 (+)。
而且，使用加号操作符在大多数情况下都比使用 concat() 方法要简便易行 (特别是在拼接多个字符串的情况下)。


### <span style="color: red;font-weight: bold">ECMAScript 还提供了三个基于子字符串创建新字符串的方法：slice()、substr() 和 substring()。</span>

这三个方法都会返回被操作字符串的一个子字符串，而且也都接受<span style="color: red;font-weight: bold">一或两个参数</span>。

第一个参数指定子字符串的开始位置，第二个参数(在指定的情况下)表示子字符串到哪里结束。

具体来说，slice() 和 substring() 的第二个参数指定的是子字符串最后一个字符后面的位置。
而 substr() 的第二个参数指定的则是返回的字符个数。
如果没有给这些方法传递第二个参数，则将字符串的长度作为结束的位置。

<span style="color: red;font-weight: bold">与 concat() 方法一样，slice()、substr() 和 substring() 也不会修改字符串本身的值</span> --
它们只是返回一个基本类型的字符串值，对原始字符串没有任何影响。请看下面的例子。

    var stringValue = "hello world";
    console.log(stringValue.slice(3));          // "lo world"
    console.log(stringValue.substring(3));      // "lo world"
    console.log(stringValue.sbustr(3));         // "lo world"

    console.log(stringValue.slice(3, 7));       // "lo w"
    console.log(stringValue.substring(3, 7));   // "lo w"
    console.log(stringValue.substr(3, 7));      // "lo worl"

这个例子比较了以相同的方式调用 slice()、substr() 和 substring() 得到的结果，而且多数情况下的结果是相同的。在只指定一个参数3的情况下，
这三个方法都返回 "lo world"，因为 "hello" 中的第二个 "l" 处于位置 3 。而在指定两个参数 3 和 7 的情况下，slice() 和 substring() 返回
"lo w" ("world" 中的 "o" 处于位置 7 ，因此结果中不包含 "o") 。但 substr() 返回 "lo worl"，因为它的第二个参数指定的是要返回的字符个数。

** <span style="color: red;font-weight: bold">在传递给这些方法的参数是负值的情况下，它们的行为就不尽相同了。</span> **

* 其中，slice() 方法会将传入的负值与字符串的长度相加，
* substr() 方法将负的第一个参数加上字符串的长度，而将负的第二个参数转换为 0 。
* 最后，substring() 方法会把所有负值参数都转换为 0 。

下面来看例子。

    var stringValue = "hello world";
    console.log(stringValue.slice(-3));         // "rld"
    console.log(stringValue.substring(-3));     // "hello world"
    console.log(stringValue.substr(-3));        // "rld"

    console.log(stringValue.slice(3, -4));      // "low"
    console.log(stringValue.substring(3, -4));  // "hel"
    console.log(stringValue.substr(3, -4));     // "" (空字符串)

这个例子清晰地展示了上述三个方法之间的不同行为。在给 slice() 和 substr() 传递一个负值参数时，它们的行为相同。这是因为 -3 会被转换为 8
(字符串长度加参数 11+(-3)=8)，实际上相当于调用了 slice(8) 和 substr(8)。 但 substring() 方法则返回了全部字符串，因为它将 -3 转换
成了 0 。

IE 的 JavaScript 实现在处理向 substr() 方法传递负值的情况时存在问题，它会返回原始的字符串。IE9 修复了这个问题。

当第二个参数是负值时，这三个方法的行为各不相同。

* slice() 方法会把第二个参数转换为 7，这就相当于调用了 slice(3, 7)，因此返回 "lo w" 。
* substring() 方法会把第二个参数转换为 0，使调用变成了 substring(3, 0)，而由于这个方法会将较小的数作为开始位置，将较大的数作为结束位置，
  因此最终相当于调用了 substring(0, 3)。
* substr() 也会将第二个参数转换为 0，这也就意味着返回包含零个字符的字符串，也就是一个空字符串。
