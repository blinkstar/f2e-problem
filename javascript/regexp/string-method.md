## 用于模式匹配的 String 方法

到目前为止，尽管已经讨论过创建正则表达式的语法，但还没有尝试过如何在 JavaScript 代码中使用这些正则表达式。下面将讨论 String 对象的一些
用以执行正则表达式模式匹配和检索替换操作的方法，后面还会继续讨论如何使用 JavaScript 正则表达式的模式匹配，不过将侧重于 RegExp 对象和它
的方法及属性。下面的讨论只是与正则表达式相关的方法和属性的概述。

### 1、search

String 支持4种使用正则表达式的方法。最简单的是 search() 。它的参数是一个正则表达式，返回第一个与之匹配的子串的起始位置，如果找不到匹配的
子串，它将返回 -1 。比如，下面的调用返回值为 4 :

    "JavaScript".search(/script/i);

<span style="color: red;font-weight: bold">如果 search() 的参数不是正则表达式，则首先会通过 RegExp 构造函数将它转换成正则表达式，</span>

<span style="color: red;font-weight: bold">search() 方法不支持全局检索，因为它忽略正则表达式参数中的修饰符 g 。</span>

### 2、replace

replace() 方法用以执行检索与替换操作。其中第一个参数是一个正则表达式，第二个参数是要进行替换的字符串。
这个方法会对调用它的字符串进行检索，使用指定的模式来匹配。如果正则表达式中设置了修饰符 g ，那么源字符串中所有与模式匹配的子串都将替换成
第二个参数指定的字符串；如果不带修饰符 g，则只替换所匹配的第一个子串。

如果 replace() 的第一个参数是字符串而不是正则表达式，则 replace() 将直接搜索这个字符串，而不是像 search() 一样首先通过 RegExp() 将
它转换为正则表达式。比如，可以使用下面的方法，利用 replace() 将文本中的所有 javascript (不区分大小写) 统一替换为 "JavaScript" ：

    // 将所有不区分大小写的 javascript 都替换成大小写正确的 JavaScript
    text.replace(/javascript/gi, "JavaScript");

但 replace() 的功能远不止这些。回忆一下前文所提到的，正则表达式中使用圆括号括起来的子表达式是带有从左到右的索引编号的，而且正则表达式
会记忆每个子表达式匹配的文本。如果在替换字符串中出现了 $ 加数字，那么 replace() 将用与指定的子表达式相匹配的文本来替换这两个字符。这是一个
非常有用的特性。比如，可以用它将一个字符串中的英文引号替换为中文半角引号：

    // 一段引用文本起始于引号，结束于引号，中间的内容区域不能包含引号
    var quote = /"([^"]*)"/g;
    // 用中文半角引号替换英文引号，同时要保持引号之间的内容 (存储在 $1 中) 没有被修改
    text.replace(quote, '“$1”');

replace() 方法的第二个参数可以是函数，该函数能够动态地计算替换字符串。

### 3、match

match() 方法是最常用的 String 正则表达式方法。

它的唯一参数就是一个正则表达式 (或通过 RegExp() 构造函数将其转换为正则表达式)，返回的是一个由匹配结果组成的数组。如果该正则表达式设置了
修饰符 g ，则该方法返回的数组包含字符串中的所有匹配结果。例如：

    "1 plus 2 equals 3".match(/\d+/g);   // 返回 ["1", "2", "3"]

如果这个正则表达式没有设置修饰符 g ，match() 就不会进行全局检索，它只检索第一个匹配。但即使 match() 执行的不是全局检索，它也返回一个数组。
在这种情况下，数组的第一个元素就是匹配的字符串，余下的元素则是正则表达式中用圆括号括起来的子表达式。因此，如果 match() 返回一个数组 a ，
那么 a[0] 存放的是完整的匹配，a[1] 存放的则是与第一个用圆括号括起来的表达式相匹配的子串，以此类推。为了和方法 replace() 保持一致，
a[n] 存放的是 $n 的内容。

例如，使用如下的代码来解析一个 URL:

    var url = /(\w+):\/\/([\w.]+)\/(\S*)/;
    var text = "Visit my blog at http://www.example.com/~david"
    var result = text.match(url);
    if(result != null){
        var fullurl = result[0];    // 包含 "http://www.example.com/~david"
        var protocol = result[1];   // 包含 "http"
        var host = result[2];       // 包含 "www.example.com"
        var path = result[3];       // 包含 "~david"
    }

值得注意的是，给字符串的 match() 方法传入一个非全局的正则表达式，实际上和给这个正则表达式的 exec() 方法传入的字符串是一模一样的，它返回
的数组带有两个属性：  index 和 input ，接下来对 exec() 方法的讨论中会提到。

### 4、split

String 对象的最后一个和正则表达式相关的方法是 split()。这个方法用以将调用它的字符串拆分为一个子串组成的数组，使用的分隔符是 split() 的参数，
例如：

    "123,456,789".split(",");       // 返回 ["123", "456", "789"]

split() 方法的参数也可以是一个正则表达式，这使得 split() 方法异常强大。例如，可以指定分隔符，允许两边可以留有任意多的空白符：

    "1, 2, 3, 4, 5".split(/\s*,\s*/);   // 返回 ["1","2","3","4","5"]

