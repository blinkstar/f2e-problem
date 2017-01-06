### 1.4 选择、分组和引用

正则表达式的语法还包括指定选择项、子表达式分组和引用前一子表达式的特殊字符。

<span style="color: red;font-weight: bold">1、字符 "|" 用于分隔供选择的字符。</span>

例如，/ab|cd|ef/ 可以匹配字符串 "ab" ，也可以匹配字符串 "cd" ，还可以匹配字符串 "ef" 。/\\d{3}|[a-z]{4}/ 匹配的是三位数字或者四个
小写字母。

注意，选择项的尝试匹配是<span style="color: red;font-weight: bold">从左到右</span>，直到发现了匹配项。
<span style="color: red;font-weight: bold">如果左边的选择项匹配，就忽略右边的匹配项，即使它产生更好的匹配。</span>因此，当正则表达式
/a|ab/ 匹配字符串 "ab" 时，它只能匹配第一个字符。

<span style="color: red;font-weight: bold">2、子表达式</span>

正则表达式的圆括号有多种作用。一个作用是<span style="color: red;font-weight: bold">把单独的项组合成子表达式</span>，
以便可以像处理一个独立的单元那样用 "|" 、"*" 、"+" 或者 "?" 等来对单元内的项进行处理。
例如，/java(script)?/ 可以匹配字符串 "java" ，其后可以有 "script" 也可以没有。
/(ab|cd)+|ef/ 可以匹配字符串 "ef"，也可以匹配字符串 "ab" 或 "cd" 的一次或多次重复。

<span style="color: red;font-weight: bold">3、子模式</span>

在正则表达式中，<span style="color: red;font-weight: bold">圆括号的另一个作用是在完整的模式中定义子模式。</span>
当一个正则表达式成功地和目标字符串相匹配时，可以从目标串中抽出和圆括号中的子模式相匹配的部分。
例如，假定我们正在检索的模式是一个或多个小写字母后面跟随了一位或多位数字，则可以使用模式 /[a-z]+\d+/ 。
但假定我们真正关心的是每个匹配尾部的数字，那么如果将模式的数字部分放在圆括号中 (/[a-z]+(\d+)/)，就可以从检索到的匹配中抽取数字了。

<span style="color: red;font-weight: bold">4、引用</span>

带圆括号的表达式的另一个用途是允许在同一正则表达式的后部引用前面的子表达式。这是通过在字符 "\\" 后加一位或多位数字来实现的。这个数字
指定了带圆括号的子表达式在正则表达式中的位置。

