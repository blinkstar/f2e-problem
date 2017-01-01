### 1. 找到字符串 "Lorem ipsum dolor sit amet, consectetur adipisicing elit" 中所有字母 "e" 所在的位置。

    var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit";
    var positions = new Array();
    var pos = stringValue.indexOf("e");

    while(pos > -1){
        positions.push(pos);
        pos = stringValue.indexOf("e", pos + 1);
    }
    console.log(positions);

### 2. 请对 String 类添加 toMoney 方法，实现如下效果：

  "120.88".toMoney()                 =>      "120.88"
  "12000.88".toMoney()               =>      "12,000.88"
  "12000000000.88".toMoney()         =>      "12,000,000,000.88"

    String.prototype.toMoney = function () {
            var stringValue = this.toString();
            var result = new Array();
            var arr = stringValue.split('.'),
                intStr = arr[0],
                floatStr = '.' + arr[1];

            result.unshift(floatStr);

            var pos = intStr.lastIndexOf("000");
            var zero = ',000';

            while(pos > -1){
                result.unshift(zero);
                intStr = intStr.substring(0, intStr.length - 3);
                pos = intStr.lastIndexOf("000");
            }

            result.unshift(intStr);
            console.log(result.join(''));
        };

        "120.88".toMoney();
        "12000.88".toMoney();
        "12000000000.88".toMoney();

[JS将number数值转化成为货币格式](//www.cnblogs.com/mingmingruyuedlut/archive/2013/05/19/3082177.html)
