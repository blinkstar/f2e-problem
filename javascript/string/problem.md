## 1. 找到字符串 "Lorem ipsum dolor sit amet, consectetur adipisicing elit" 中所有字母 "e" 所在的位置。

    var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit";
        var positions = new Array();
        var pos = stringValue.indexOf("e");

        while(pos > -1){
            positions.push(pos);
            pos = stringValue.indexOf("e", pos + 1);
        }
        console.log(positions);

## 2. 请对 String 类添加 toMoney 方法，实现如下效果：

    "120.88".toMoney()                 =>      "120.88"
    "12000.88".toMoney()               =>      "12,000.88"
    "12000000000.88".toMoney()         =>      "12,000,000,000.88"
