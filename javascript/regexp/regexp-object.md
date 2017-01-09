## RegExp 对象

正则表达式是通过 RegExp 对象表示的。除了 RegExp() 构造函数之外，RegExp 对象还支持三个方法和一些属性。接下来会对 RegExp 模式匹配方法
和属性展开讲述。

RegExp() 构造函数带有两个字符串参数其中第二个参数是可选的，RegExp() 用以创建新的 RegExp 对象。

第一个参数包含正则表达式的主体部分，也就是正则表达式直接量中两条斜线之间的文本。需要注意的是，不论是字符串直接量还是正则表达式，都用 "\"
字符作为转义字符的前缀，因此当给 RegExp() 传入一个字符串表述的正则表达式时，必须将 "\" 替换成 "\\" 。

RegExp() 的第二个参数是可选的，如果提供第二个参数，它就指定正则表达式的修饰符。不过只能传入修饰符 g 、i 、m 或者它们的组合。比如：

    // 全局匹配字符串中的 5 个数字，注意这里使用了 "\\" ，而不是 "\"
    var zipcode = new RegExp("\\d{5}", "g");

RegExp() 构造函数非常有用，特别是在需要动态创建正则表达式的时候，这种情况往往没办法通过写死在代码中的正则表达式直接量来实现。例如，如果
待检索的字符是由用户输入的，就必须使用 RegExp() 构造函数，在程序运行时创建正则表达式。

### 1 RegExp 的属性

每个 RegExp 对象都包含5个属性。

属性 source 是一个只读的字符串，包含正则表达式的文本。

属性 global 是一个只读的布尔值，用以说明这个正则表达式是否带有修饰符 g 。

属性 ignoreCase 也是一个只读的布尔值，用以说明正则表达式是否带有修饰符 i 。

属性 multiline 是一个只读的布尔值，用以说明正则表达式是否带有修饰符 m 。

最后一个属性 lastIndex ，它是一个可读/写的整数。如果匹配模式带有 g 修饰符，这个属性存储在整个字符串中下一次检索的开始位置，这个属性会被
exec() 和 test() 方法用到。

### 2 RegExp 的方法

RegExp 对象定义了两个用于执行模式匹配操作的方法。它们的行为和上文介绍过的 String 方法很类似。


<span style="color: red;font-weight: bold">RegExp 最主要的执行模式匹配的方法是 exec()</span>

它与 String 方法的 match() 相似，只是 RegExp 方法的参数是一个字符串，而 String 方法的
参数是一个 RegExp 对象。
exec() 方法对一个指定的字符串执行一个正则表达式，简言之，就是在一个字符串中执行匹配检索。如果它没有找到任何匹配，它就返回 null ，但如果它找到
了一个匹配，它将返回一个数组，就像 match() 方法为非全局检索返回的数组一样。这个数组的第一个元素包含的是与正则表达式相匹配的字符串，余下的元素
是与圆括号内的子表达式相匹配的子串。属性 index 包含了发生匹配的字符位置，属性 input 引用的是正在检索的字符串。

<span style="color: red;font-weight: bold">和 match() 方法不同，不管正则表达式是否具有全局修饰符 g ，exec() 都会返回一样的数组。</span>

当 match() 的参数是一个全局正则表达式时，它返回由匹配结果组成的数组。
相比之下，exec() 总是返回一个匹配结果，并提供关于本次匹配的完整信息。

当调用 exec() 的正则表达式对象具有修饰符 g 时，它将把当前正则表达式对象的 lastIndex 属性设置为紧挨着匹配子串的字符位置。当一个正则表达式
第二次调用 exec() 时，它将从 lastIndex 属性所指示的字符处开始检索。如果 exec() 没有发现任何匹配结果，它会将 lastIndex 重置为 0 (在任何
时候都可以将 lastIndex 属性设置为 0，每当在字符串中找最后一个匹配项后，在使用这个 RegExp 对象开始新的字符串查找之前，都应当将 lastIndex
设置为 0) 。这种特殊的行为使我们可以在用正则表达式匹配字符串的过程中反复调用 exec() ，比如：

    var pattern = /Java/g;
    var text = "JavaScript is more fun than Java!";
    var result;
    while((result = pattern.exec(text)) != null){
        console.log("Matched '" + result[0] + "'" + " at position " + result.index + "; next search begins at " + pattern.lastIndex);
    };

<span style="color: red;font-weight: bold">另外一个 RegExp 方法是 test()</span>

它比 exec() 更简单一些。它的参数是一个字符，用 test() 对某个字符串进行检测，如果包含正则表达式的一个匹配结果，则返回 true：

    var pattern = /java/i;
    pattern.test("JavaScript");  // 返回 true

调用 test() 和调用 exec() 等价，当 exec() 的返回结果不是 null 时，test() 返回 true。由于这种等价性，当一个全局正则表达式调用方法 test()
时，它的行为和 exec() 相同，因为它从 lastIndex 指定的位置处开始检索某个字符串，如果它找到了一个匹配结果，那么它就立即设置 lastIndex 为
当前匹配子串的结束位置。这样一来，就可以使用 test() 来遍历字符串，就像用 exec() 方法一样。

<span style="color: red;font-weight: bold">与 exec() 和 test() 不同，String 方法 search()、replace() 和 match() 并不会用到 lastIndex 属性。</span>

实际上，String 方法只是简单地将 lastIndex 属性值重置为 0 。如果让一个i额带有修饰符 g 的正则表达式对多个字符串执行 exec() 或 test() ，
要么在每个字符串中找出所有的匹配以便将 lastIndex 自动重置为零，要么显式将 lastIndex 手动设置为 0 (当最后一次检索失败时需要手动设置 lastIndex)。
如果忘了手动设置 lastIndex 的值，那么下一次对新字符串进行检索时，执行检索的起始位置可能就不是字符串的开始位置，而可能是任意位置。

当然，如果 RegExp 不带有修饰符 g ，则不必担心会发生这种情况。

同时要记住，在 ECMAScript 5 中，正则表达式直接量的每次计算都会创建一个新的 RegExp 对象，每个新 RegExp 对象具有各自的 lastIndex 属性，
这势必会大大减少 "残留" lastIndex 对程序造成的意外影响。
