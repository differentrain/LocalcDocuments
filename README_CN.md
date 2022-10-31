
# Localc

[<img src="https://github.com/differentrain/LocalcDocuments/raw/main/Img/Chinese_Simplified_Get.png" width=106/>](https://www.microsoft.com/store/apps/9MWVH00SS87R) 　

一个轻巧但强大的计算器，用于编程与调试。

[中文](https://github.com/differentrain/LocalcDocuments/blob/main/README_CN.md) 　　 
[English](https://github.com/differentrain/LocalcDocuments/blob/main/README.md)

## 起步

Localc 利用四个数字框来存储操作数。你可以在十六进制/十进制/八进制/二进制之间切换其显示形式。

![img_main_gui](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_main_gui.png)

如图所示，一元运算的按钮 NEG(求反) 和 NOT(位运算 NOT) 皆位于数字框中。MAX(当前整数类型的最大值) 、MAX(当前整数类型的最小值)、CLR(数字置0)、BKSP(退格)等按钮也在其中。 当你点击这些按钮，其所属的数字框就会执行相应的操作。而如果你按下了相关[快捷键](https://github.com/differentrain/LocalcDocuments/blob/main/README_CN.md#%E5%BF%AB%E6%8D%B7%E9%94%AE)，操作将会执行于当前被选中的数字框。

被小方框标出的区域表示用于计算的全局整数类型。它的默认值是 `Int64`(有符号64位整数)，点击此区域可以修改这个值。

现在我们看看怎么用 Localc 进行最简单的计算。

在 Localc 的数字面板中只有二元运算符，没有等号。如果你了解过 [逆波兰表达式](https://en.wikipedia.org/wiki/Reverse_Polish_notation), 你肯定很容易理解以下规则:

+	二元运算将被选中的数字框作为第一个操作数，二把此数字框的下一个数字框作为第二个操作数。
+	计算结果放入被选中的数字框中。
+	如果是第四个数字框被选中，则它被视为第二个操作数，且运算结果存储于第三个数字框中。

举例来说，加入第三个数字框的值是`3`，而第四个数字框的值是`4`，而此时第四个数字框被选中，那么点击 ADD(+) 按钮后，第三个数字框的值将变成 `7`。

## 在文本和字节数组之间转换

![img_str_pad](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_str_pad.png)

在文本和字节数组之间转换的操作很简单。上方的文本框用于输入普通文本，而下方的文本框用来输入十六进制字节数组。 在其中一个文本框输入相应内容，另一个文本框就会根据所选择的代码页显示出相应的转换结果。  

十六进制字节数组的元素可以是空格(`0x20`)、逗号(`,`) ，或者一个十六进制数。这个十六进制数不需要 `0x` 前缀, 但 **必须** 包括且 **只** 包括两位数字。

例如  `0x01,0X02, 03 04 F2` 是正确的, 但 `01 02 3 04` 则不正确。

Str面板中的按钮说明了，当所选择的代码页发生变动时，究竟是将普通文本还是十六进制数组作为转换源进行转换。 它的默认设置是 `Text`, 当你选择其他的代码页时， Localc 将会将文本转化为字节数组。点击此按钮可以将这个选项改成 `Bytes`.

## 表达式
![img_exp_pad.png](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_exp_pad.png)

复合框表示表达式计算时依据的整数类型。 `Inherit` 表示 Localc 将使用全局整数类型（图片中是Int64）进行表达式计算。你也可以将它改成其他的单独的值。

Localc 支持以下表达式符号:

**所有符号均不区分大小写。**

|  符号  | 含义  | 备注 |
|  :---:  | ---  |--- |
|+|ADD||
|-|SUB 或 NEG|NEG 不支持无符号整数|
|\*|MUL||
|/|DIV||
|%|MOD||
|&amp;|AND||
|\||OR||
|^|XOR||
|~|NOT||
|<<|SAL or SHL||
|>>|SAR||
|>>>|SHR||
|<|ROL||
|>|ROR||
|(|左括号||
|)|右括号||
|max|当前参与计算的整数类型的最大值||
|min|当前参与计算的整数类型的最小值||
|`nb1`<br/>-<br/>`nb4`|引用指定数字框的值|如果表达式的整数类型小于全局整数类型，则此值将会被截断|
|$*\<varName\>*|引用定义于[变量列表](https://github.com/differentrain/LocalcDocuments/blob/main/README_CN.md#%E5%8F%98%E9%87%8F)的变量的值|如果表达式的整数类型小于64位，则此值将会被截断|

表达式的整数类型使用 `_` 和 `,` 作为分隔符，因此 `1,2_3` 和 '0x1_2_3' 是正确的表示形式。 

八进制数必须包括 `@` 前缀, 二进制数必须包括 `#` 前缀。

对于十六进制数而言, `0x` 前缀通常是必要的, 但如果一个十六进制数含有 *A-F* 的数字位，则可以省略前缀, 因此 `0x1F` 或 `1F` 都是允许的. 

### 浮点模式

你可能要用到浮点数计算。

如果表达式以单引号(`'`)作为起始, 表达式中所有的数字都被视为单浮点数。 

如果表达式以两个单引号(`''`), 或者一个双引号(`"`)作为起始, 表达式中所有的数字都被视为双浮点数。

下面是浮点数允许的格式举例:

+	-0.1
+	.2
+	1E3
+	1E+3
+	1E-3

**在浮点数模式中，16/8/2 进制的数字必须包括前缀，将被视为以二进制形式所表示的浮点数。**

浮点模式支持以上除位运算之外的所有符号，并且还支持以下符号：

|  符号  | 含义  | 
|  :---:  | ---  | 
|inf|浮点数无穷|
|∞|浮点数无穷|
|nan|浮点数无穷NaN|
|pi|数学常数π|
|e|数学常数E|
|[pow](https://learn.microsoft.com/en-us/dotnet/api/system.math.pow)| Pow(v1,v2)|
|[exp](https://learn.microsoft.com/en-us/dotnet/api/system.math.exp)| Exp(v)=Pow(e,v)|
|[acos](https://learn.microsoft.com/en-us/dotnet/api/system.math.acos)|Acos(v)|
|[asin](https://learn.microsoft.com/en-us/dotnet/api/system.math.asin)|Asin(v)|
|[atan](https://learn.microsoft.com/en-us/dotnet/api/system.math.atan)|ATan(v)|
|[cos](https://learn.microsoft.com/en-us/dotnet/api/system.math.cos)|Cos(v)  |
|[cosh](https://learn.microsoft.com/en-us/dotnet/api/system.math.cosh)|Cosh(v)|
|[sin](https://learn.microsoft.com/en-us/dotnet/api/system.math.sin)|Sin(v)  |
|[sinh](https://learn.microsoft.com/en-us/dotnet/api/system.math.sinh)|Sinh(v)|
|[tan](https://learn.microsoft.com/en-us/dotnet/api/system.math.tan)|Tan(v)  |
|[tanh](https://learn.microsoft.com/en-us/dotnet/api/system.math.tanh)|Tanh(v)|
|[sqrt](https://learn.microsoft.com/en-us/dotnet/api/system.math.sqrt)|Sqrt(v)|
|[log](https://learn.microsoft.com/zh-cn/dotnet/api/system.math.log?view=#system-math-log(system-double-system-double))|Log(v1,v2)|
|[lg](https://learn.microsoft.com/en-us/dotnet/api/system.math.log10)| Lg(v)=Log(10,v)|
|[In](https://learn.microsoft.com/en-us/dotnet/api/system.math.log?view=#system-math-log(system-double))|In(v)=Log(e,v)|
|[lb](https://learn.microsoft.com/en-us/dotnet/api/system.math.log2)| Ib(v)=Log(2,v)|
|[ld](https://learn.microsoft.com/en-us/dotnet/api/system.math.log2)|Id(v)=Log(2,v)|
|cif|cif(v), 将v视作一个有符号整数，并将其转换为浮点数|
|cuf|cuf(v), 将v视作一个无符号整数，并将其转换为浮点数|

## 变量
![img_var_pad.png](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_var_pad.png)

你可以把变量加入变量列表中，并通过 `$varName` 在表达式中进行引用.你也可以单击已存在的变量，对它进行修改。

用来输入变量值的文本框提供了对 [表达式](https://github.com/differentrain/LocalcDocuments/blob/main/README_CN.md#%E8%A1%A8%E8%BE%BE%E5%BC%8F) 的计算功能, **不过其用于计算的整数类型是 `Int64` **. 

## 拖拽

你可以把一个数字框拖拽到另一个数字框上来交换它们的值。如果拖拽时按住`Shift`键，则被拖拽的数字框的值将复制到目标数字框。按住`Ctrl`键则可以调整数字框的顺序。

你也可以将数字框拖拽到Exp面板来进行参考，而Exp面板的结果区(如果有效)也可以拖拽到任意数字框上。

把数字框拖拽到Var面板中的变量值输入框上，其值也将复制到输入框。你也可以把数字框拖拽到现有的变量上面以更新它的值，同理，变量也可以拖拽到数字框上。

## 快捷键

**\*  : 作用于当前选择的数字框。**

|  shortcuts  | effect  | remark |
|  :---:  | ---  |--- |
|`0`<br/>-<br/>`9`|输入 `0` -`9`|*\** 只在Num面板和Bit面板中可用|
|`A`<br/>-<br/>`F`|输入 `A` -`F`|*\** 只在Num面板和Bit面板中可用|
|`Escape`|CLR|*\** 只在Num面板和Bit面板中可用|
|`Backspack`|BKSP|*\** 只在Num面板和Bit面板中可用|
|`+`|ADD|*\** 只在Num面板和Bit面板中可用|
|`-`|SUB|*\** 只在Num面板和Bit面板中可用|
|`*`|MUL|*\** 只在Num面板和Bit面板中可用|
|`/`|DIV|*\** 只在Num面板和Bit面板中可用|
|`%`|MOD|*\** 只在Num面板和Bit面板中可用|
|`&`|AND|*\** 只在Num面板和Bit面板中可用|
|`\|`|OR|*\** 只在Num面板和Bit面板中可用|
|`^`|XOR|*\** 只在Num面板和Bit面板中可用|
|`~`|NOT|*\** 只在Num面板和Bit面板中可用|
|`N`|NEG|*\** 只在Num面板和Bit面板中可用|
|`Ctrl`\+`C`|复制|*\** 只在Num面板和Bit面板中可用|
|`Ctrl`\+`V`|粘贴|*\** 只在Num面板和Bit面板中可用|
|`Ctrl`\+`X`|复制并将其值清零|*\** 只在Num面板和Bit面板中可用|
|`F1`|选择第1个数字框||
|`F2`|选择第2个数字框||
|`F3`|选择第3个数字框||
|`F4`|选择第4个数字框||
|`F5`|切换全局整数类型有/无符号||
|`F6`|改变全局整数类型大小||
|`F9`|HEX|*\** |
|`F10`|DEX|*\** |
|`F11`|OCT|*\** |
|`F12`|BIN|*\** |
