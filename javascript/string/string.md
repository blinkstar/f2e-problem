# String 类型

String 类型用于表示由零或多个16位 Unicode 字符组成的字符序列，即字符串。字符串可以由双引号 (") 或单引号 (') 表示，因此下面两种字符串
的写法都是有效的：

    var firstName = "Nicholas";
    var lastName = 'Zakas';

与PHP中的双引号和单引号会影响对字符串的解释方式不同，ECMAScript 中的这两种语法形式没有什么区别。用双引号表示的字符串和用单引号表示的
字符串完全相同。不过，以双引号开头的字符串也必须以双引号结尾，而以单引号开头的字符串必须以单引号结尾。例如，下面这种字符串表示法会导致
语法错误：

    var firstName = 'Nicholas";  // 语法错误 (左右引号必须匹配)

## 1 字符字面量

String 数据类型包含一些特殊的字符字面量，也叫转义序列，用于表示非打印字符，或者具有其他用途的字符。这些字符字面量如下表所示：

<table>
	<thead>
		<tr><th>字面量</th><th>含义</th></tr>
	</thead>
	<tbody>
		<tr><td>\n</td><td>换行</td></tr>
		<tr><td>\t</td><td>制表</td></tr>
		<tr><td>\b</td><td>空格</td></tr>
		<tr><td>\r</td><td>回车</td></tr>
		<tr><td>\f</td><td>进纸</td></tr>
		<tr><td>\\</td><td>斜杠</td></tr>
		<tr><td>\'</td><td>单引号(')，在单引号表示的字符串中使用。例如： 'He said, \'hey.\''</td></tr>
		<tr><td>\"</td><td>双引号(")，在双引号表示的字符串中使用。例如： "He said, \"hey.\""</td></tr>
		<tr><td>\xnn</td><td>以十六进制代码nn表示的一个字符(其中n为0~F)。例如，\x41 表示 "A"</td></tr>
		<tr><td>\unnnn</td><td>以十六进制代码nnnn表示的一个Unicode字符(其中n为0~F)。例如，\u03a3表示希腊字符 Σ</td></tr>
	</tbody>
</table>

这些字符字面量可以出现在字符串中的任意位置，而且也将被作为一个字符来解析，如下面的例子所示：

    var text = "This is the letter sigma: \u03a3.";

这个例子中的变量 text 有 28 个字符，其中6个字符长的转义序列表示1个字符 Σ 。
任何字符串的长度都可以通过访问其 length 属性取得，例如：

    alert(text.length);  // 输出 28

这个属性返回的字符数包括16位字符的数目。如果字符串中包含双字节字符，那么 length 属性可能不会精确地返回字符串中的字符数目。

## 2 字符串的特点

<span style="color: red;font-weight: bold">ECMAScript 中的字符串是不可变的，也就是说，字符串一旦创建，它的值就不能改变。</span>
要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的字符串填充该变量。例如：

    var lang = "Java";
    lang = lang + "Script";

以上示例中的变量 lang 开始时包含字符串 "Java" 。而第二行代码把 lang 的值重新定义为 "Java" 与 "Script" 的组合，即 "JavaScript"。
实现这个操作的过程如下：

* 首先创建一个能容纳 10 个字符的新字符串，
* 然后在这个字符串中填充 "Java" 和 "Script"，
* 最后一步是销毁原来的字符串 "Java" 和字符串 "Script"，因为这两个字符串已经没用了。

这个过程是在后台发生的，而这也是在某些旧版本的浏览器中 (例如版本低于 1.0 的 Firefox、IE6等) 中拼接字符串时速度很慢的原因所在。但这些浏览器
后来的版本已经解决了这个低效问题。

## 3 转换为字符串

要把一个值转换为一个字符串有两种方式。第一种是使用几乎每个值都有的 toString() 方法。这个方法唯一要做的就是返回相应的字符串表现。来看
下面的例子：

    var age = 11;
    var ageAsString = age.toString();     // 字符串 "11"
    var found = true;
    var foundAsString = found.toString(); // 字符串 "true"

数值、布尔值、对象和字符串值(没错，每个字符串也都有一个 toString()方法，该方法返回字符串的一个副本) 都有 toString() 方法。
<span style="color: red;font-weight: bold">但 null 和 undefined 值没有这个方法。</span>

多数情况下，调用 toString() 方法不必传递参数。但是，在调用**数值**的 toString() 方法时，可以传递一个参数：输出数值的基数。默认情况下，
toString() 方法以十进制格式返回数值的字符串表示。而通过传递基数，toString() 可以输出以二进制、八进制、十六进制，乃至其他任意有效
进制格式表示的字符串值。下面给出几个例子：

    var num = 10;
    console.log(num.toString());      // "10"
    console.log(num.toString(2));     // "1010"
    console.log(num.toString(7));     // "13"
    console.log(num.toString(8));     // "12"
    console.log(num.toString(10));    // "10"
    console.log(num.toString(16));    // "a"

通过这个例子可以看出，通过指定基数，toString() 方法会改变输出的值。而数值 10 根据基数的不同，可以在输出时被转换为不同的数值格式。注意，
默认的 (没有参数的) 输出值与指定基数 10 时的输出值相同。

<span style="color: red;font-weight: bold">在不知道要转换的值是不是 null 或 undefined 的情况下，还可以使用转型函数 String() ，
这个函数能够将任何类型的值转换为字符串。</span>

String() 函数遵循下列转换规则：

* 如果值有 toString() 方法，则调用该方法 (没有参数) 并返回相应的结果：
* 如果值是 null，则返回 "null";
* 如果值是 undefined ，则返回 "undefined" 。

下面再看几个例子：

    var value1 = 10;
    var value2 = true;
    var value3 = null;
    var value4;

    console.log(String(value1));   // "10"
    console.log(String(value2));   // "true"
    console.log(String(value3));   // "null"
    console.log(String(value4));   // "undefined"

这里先后转换了4个值：数值、布尔值、null 和 undefined 。数值和布尔值的转换结果与调用 toString() 方法得到的结果相同。
因为 null 和 undefined 没有 toString() 方法，所以 String() 函数就返回了这两个值的字面量。

要把某个值转换为字符串，可以使用加号操作符把它与一个字符串 ("") 加在一起。