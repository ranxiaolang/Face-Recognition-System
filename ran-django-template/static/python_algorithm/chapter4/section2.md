# 栈的应用
###使用场景
1.符号匹配  
2.计算机表达式的转换  
3.CPU内部栈主要是用来进行子程序调用和返回  
4.进制转换  
###1.括号匹配问题
大多数计算机语言中都需要检测括号是否匹配，那么如何实现符号成对检测？  

**算法思路**：
* 从第一个字符开始扫描
* 当遇见普通字符时忽略，
* 当遇见左符号时压入栈中
* 当遇见右符号时从栈中弹出栈顶符号，并进行匹配
* 匹配成功：继续读入下一个字符
* 匹配失败：立即停止，并报错
* 结束：
  成功: 所有字符扫描完毕，且栈为空
  失败：匹配失败或所有字符扫描完毕但栈非空


###2.计算机表达式转换
计算机的本质工作就是做数学运算，那计算机可以读入字符串
"9 + (3 - 1) * 5 + 8 / 2"并计算值吗？

**中缀表达式和后缀表达式**  
后缀表达式（由波兰科学家在20世纪50年代提出）  
将运算符放在数字后面 ===》 符合计算机运算  
我们习惯的数学表达式叫做中缀表达式===》符合人类思考习惯  
实例
```
5 + 4 => 5 4 +    
1 + 2 * 3 => 1 2 3 * +    
8 + ( 3 – 1 ) * 5 => 8 3 1 – 5 * +  
```
**算法思路**  
中缀转后缀：
遍历中缀表达式中的数字和符号
* 对于数字：直接输出
* 对于符号：  

（1）左括号：进栈        
（2）运算符号：与栈顶符号进行优先级比较    
若栈顶符号优先级低：此符号进栈  
（默认栈顶若是左括号，左括号优先级最低）
若栈顶符号优先级不低：将栈顶符号弹出并输出，之后进栈
（3）右括号：将栈顶符号弹出并输出，直到匹配左括号   
* 遍历结束：将栈中的所有符号弹出并输出


> **练习拓展：计算机如何基于后缀表达式结算结果**  
> 例如：8 3 1 – 5 * +
* 计算规则：  
* 遍历后缀表达式中的数字和符号  
* 对于数字：进栈  
* 对于符号：  
  （1）从栈中弹出右操作数
  （2）从栈中弹出左操作数
  根据符号进行运算
  将运算结果压入栈中
遍历结束：栈中的唯一数字为计算结果