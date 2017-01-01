## 3 字符串位置方法

有两个可以从字符串中查找子字符串的方法：indexOf() 和 lastIndexOf() 。这两个方法都是从一个字符串中搜索给定的子字符串，然后返回子字符串的
位置(如果没有找到该子字符串，则返回 -1)。

这两个方法的区别在于：indexOf() 方法从字符串的开头向后搜索子字符串，而 lastIndexOf() 方法是从字符串的末尾向前搜索子字符串。还是来看一个
例子吧。

    var stringValue = "hello world";
    console.log(stringValue.indexOf("o"));      // 4
    console.log(stringValue.lastIndexOf("o"));  // 7

子字符串 "o" 第一次出现的位置是 4，即 "hello" 中的 "o"；最后一次出现的位置是 7 ，即 "world" 中的 "o"。如果 "o" 在这个字符串中仅出现
了一次，那么 indexOf() 和 lastIndexOf() 会返回相同的位置值。

这两个方法都可以接收可选的第二个参数，表示从字符串中的哪个位置开始搜索。换句话说，indexOf() 会从该参数指定的位置向后搜素，忽略该位置之前
的所有字符；而 lastIndexOf() 则会从指定的位置向前搜索，忽略该位置之后的所有字符。看下面的例子。

    var stringValue = "hello world";
    console.log(stringValue.indexOf("o", 6));       // 7
    console.log(stringValue.lastIndexOf("o", 6));   // 4

在将第二个参数 6 传递给这两个方法之后，得到了与签名例子相反的结果。这一次，由于 indexOf() 是从位置 6 (字母 "w") 开始向后搜索，结果在
位置 7 找到了 "o"，因此它返回 7 。而 lastIndexOf() 是从位置 6 开始向前搜索。结果找到了 "hello" 中的 "o" ，因此它返回4 。

在使用第二个参数的情况下，可以通过循环调用 indexOf() 或 lastIndexOf() 来找到所有匹配的子字符串，如下面的例子所示：

    var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit";
    var positions = new Array();
    var pos = stringValue.indexOf("e");

    while(pos > -1){
        positions.push(pos);
        pos = stringValue.indexOf("e", pos + 1);
    }

    console.log(positions);  // "3, 24, 32, 35, 52"

这个例子通过不断增加 indexOf() 方法开始查找的位置，遍历了一个长字符串。在循环之外，首先找到了 "e" 在字符串中的初始位置；而进入循环后，
则每次都给 indexOf() 传递上一次的位置加 1 。这样，就确保了每次新搜索都从上一次找到的子字符串的后面开始。每次搜索返回的位置依次被保存
在数组 positions 中，以便将来使用。

## 4 trim() 方法

ECMAScript 5 为所有字符串定义了 trim() 方法。这个方法会创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果。例如：

    var stringValue = "         hello world        ";
    var trimmedStringValue = stringValue.trim();
    console.log(stringValue);                  // "         hello world        "
    console.log(trimmedStringValue);           // "hello world"

<span style="color: red;font-weight: bold">由于 trim() 返回的是字符串的副本，所以原始字符串中的前置及后缀空格会保持不变。</span>  

支持这个方法的浏览器有 IE9+、Firefox3.5+、Safari 5+、Opera 10.5+ 和 Chrome。此外，Firefox 3.5+、Safari 5+ 和 Chrome 8 + 还支持
非标准的 trimLeft() 和 trimRight() 方法，分别用于删除字符串开头和末尾的空格。

