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

这个例子中的变量 text 有 28 个字符，其中6个字符长的转义序列表示1个字符。
任何字符串的长度都可以通过访问其 length 属性取得，例如：

    alert(text.length);  // 输出 28

这个属性返回的字符数包括16位字符的数目。如果字符串中包含双字节字符，那么 length 属性可能不会精确地返回字符串中的字符数目。