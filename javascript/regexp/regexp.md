# 正则表达式的模式匹配

正则表达式 (regular expression) 是一个描述字符模式的对象。JavaScript 的 RegExp 类表示正则表达式，String 和 RegExp 都定义了方法，
后者使用正则表达式进行强大的模式匹配和文本检索与替换功能。JavaScript 的正则表达式语法是 Perl 5 的正则表达式语法的大型子集。

## 1 正则表达式的定义

JavaScript 中的正则表达式用 RegExp 对象表示，可以使用 RegExp() 构造函数来创建 RegExp 对象，不过 RegExp 对象更多的是通过一种特殊的
直接量语法来创建。就像通过引号包裹字符的方式来定义字符串直接量一样，正则表达式直接量定义为包含在一对斜杠 (/) 之间的字符，例如：

    var pattern = /s$/;

运行这段代码创建一个新的 RegExp 对象，并将它赋值给变量 pattern 。这个特殊的 RegExp 对象用来匹配所有以字母 "s" 结尾的字符串。用构造函数
RegExp() 也可以定义个与之等价的正则表达式，代码如下：

    var pattern = new RegExp("s$");

### RegExp 直接量和对象的创建

就像字符串和数字一样，程序中每个取值相同的原始类型直接量均表示相同的值，这是显而易见的。程序运行时每次遇到对象直接量 (初始化表达式) 诸如
{} 和 [] 的时候都会创建新对象。比如，如果在循环体中写 var a = [],则每次遍历都会创建一个新的空数组。

正则表达式直接量则与此不同，ECMAScript 3 规定，一个正则表达式直接量会在执行到它时转换为一个 RegExp 对象，同一段代码所表示正则表达式直接
量的每次运算都返回同一个对象。ECMAScript 5 规范则做了相反的规定，同一段代码所表示直接量的每次运算都返回新对象。IE 一直都是按照
ECMAScript 5 规范实现的，多数最新版本的浏览器也开始遵循 ECMAScript 5 ，尽管目前该标准并未全面广泛推行。

在这里揭示了一种非常容易忽略的情况，比如，这段代码在 Firefox 3.6 和 Firefox 4+ 中的运行结果不一致：

    function getRE() {
        var re = /[a-z]/;
        re.foo = "bar";
        return re;
    }

    var reg = getRE(),
        re2 = getRE();

    console.log(reg === re2);    // 在 Firefox 3.6 中返回 true，在 Firefox 4+ 中返回 false
    reg.foo = "baz";
    console.log(re2.foo);   // 在 Firefox 3.6 中返回 "baz"，在 Firefox 4+ 中返回 "bar"

原因可以在 ECMAScript 5 规范中找到，也就是说在 ECMAScript 3 规范中，用正则表达式创建的 RegExp 对象会共享同一个实例，而在
ECMAScript 5 中则是两个独立的实例。而最新的 Firefox 4、Chrome 和 Safari 5 都遵循 ECMAScript 5 标准，以至于 IE6~IE8都
没有很好地遵循 ECMAScript 3 标准，不过在这个问题上反而处理对了。很明显 ECMAScript 5 的规范更符合开发者的期望。


正则表达式的模式规则是由一个字符序列组成的。包括所有字母和数字在内，大多数的字符都是按照直接量仅描述待匹配的字符的。如此说来，
正则表达式 /java/ 可以匹配任何包含 "java" 子串的字符串。除此之外，正则表达式中还有其他具有特殊语义的字符，这些字符并不按照
字面含义进行匹配。比如，正则表达式 /s$/ 包含两个字符，第一个字符 "s" 按照字母含义匹配，第二个字符 $ 是一个具有特殊语义的元
字符，用以匹配字符串的结束。因此这个正则表达式可以匹配任何以 "s" 结束的字符串。  
