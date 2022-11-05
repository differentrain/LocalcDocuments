# Localc

[<img src="https://github.com/differentrain/LocalcDocuments/raw/main/Img/English_get.png" width=106/>](https://www.microsoft.com/store/apps/9MWVH00SS87R) 　

A light but powerful calculator for coding and debugging.

[English](https://github.com/differentrain/LocalcDocuments/blob/main/README.md) 　　 [中文](https://github.com/differentrain/LocalcDocuments/blob/main/README_CN.md)

[Open source command-line version](https://github.com/differentrain/Loexp)

## Getting Started

Localc has four number-boxes for storing operands. You can switch display-format between hexadecimal, decimal, octal and binary.

![img_main_gui](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_main_gui.png)

As shown in the illustration, unary-operations buttons NEG(negation), NOT(bitwise NOT) are placed in number-box, as same as MAX(max value of current integer type), MIN(min value of current integer type), CLR(set number to 0), BKSP(backspace). When you click these button, the number-box owns them will perform  corresponding operations. if you press related [shortcuts](https://github.com/differentrain/LocalcDocuments#shortcuts), the operation will be performed on the selected number-box.

The area marked by a small square is the global integer type used for calculating. The default option is set to Int64(Signed 64-bit integer). The option chould be changed by clicking buttons in this area.

Now let us find out how to use Localc for simple calculation.

There is no equals sign button in Loaclc's Num-pad who contains only binary-operations buttons. If you know about [Reverse Polish Notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation), you must know how dos it works easily:

+	Binary-operations perform on the numbers stored in the selected number-box(first operand) and the next number-box(second operand). 
+	The result will be stored in the selected number-box.
+	If 4th number-box is selected, the number stored in it is deemed as the second operand, and the result will be stored in 3th number-box.

If 3th number-box's value is `3`, and 4th number-box's is selected and it's value is `4` , the value of 3th number-box is set to `7` by clicking ADD(+) button.

## Conversion Between Text And Bytes
![img_str_pad](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_str_pad.png)

The top text-box on Str-pad is used for entering normal text, and the bottom text-box for entering the text of hex-bytes. It is very easy to convert text to hex-bytes or convert hex-bytes to text: just input string into one of them, the text in another one would be changed with selected codepage.

The elements of hex-bytes can be space(`0x20`), comma(`,`) or hex-number. A Hex-number does not need `0x` prefix, but **MUST** contains and contains **only** two digits.

For example, `0x01,0X02, 03 04 F2` is a correct format, but `01 02 3 04` is incorrect.

The button in Str-pad specifies that whether normal text or hex-bytes will be deemed as conversion source when codepage selection is changed. It's default option is set to `Text`, if you change the codepage selection, Localc will convert the text to hex-bytes. You can set it to `Bytes` by clicking the button.


### new feature in 1.0.2  

A text-box is added to Str-pad for representing the first eight bytes of hex-bytes with hex-number.

## Expressions
![img_exp_pad.png](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_exp_pad.png)

The combo-box specifies the integer type for calculating expression. `Inherit` means that Localc will use global integer type (Int64, in illustration) for calculating expressions. You can also change it to another independent value.

Localc supports these expression tokens:

**All tokens ignore case.**

|  token  | meaning  | remark |
|  :---:  | ---  |--- |
|+|ADD||
|-|SUB or NEG|NEG does not support unsigned integer|
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
|(|Left bracket||
|)|Right bracket||
|max|The max value of current int-type for calculating||
|min|The min value of current int-type for calculating||
|`nb1`<br/>-<br/>`nb4`|References the value of target number-box|If the size of int-type for expression is less than global int-type, the value will be truncated|
|$*\<varName\>*|References the value defined in [variables list](https://github.com/differentrain/LocalcDocuments#variables)|If the size of int-type for expression is less than 64-bit, the value will be truncated|

Integer number in expression uses `_` and `,` as separators, so `1,2_3` and '0x1_2_3' are correct formats. 

Octal-numbers must start with `@` prefix, and binary-numbers must start with `#` prefix.

For hex-numbers, `0x` prefix is usually required, but if a hex number contains *A-F* digits, the prefix can be ignored, so either `0x1F` or `1F` is correct. 

### Floating-point Mode

You may also want to operate on the floating-point numbers.

If expressions start with a single quotation mark(`'`), all number in this expression will be deemed as floating-point number. 

If the expressions start with two single quotation marks(`''`), or a double quotation mark(`"`), all numbers in this expression will be deemed as double floating-point number.

Floating-point number format examples:

+	-0.1
+	.2
+	1E3
+	1E+3
+	1E-3

**In floating-point mode, hex/oct/bin numbers are deemed as binary representation of the floating-point numbers, and must start with related prefix.**

Floating-point mode supports all tokens above except bitwise operators, in addition to these tokens below:

|  token  | meaning  | 
|  :---:  | ---  | 
|inf|Floating-point Infinity|
|∞|Floating-point Infinity|
|nan|Floating-point NaN|
|pi|Mathematical constant π|
|e|Mathematical constant E|
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
|cif|cif(v), converts the signed integer represented by v to floating-pointer|
|cuf|cuf(v), converts the unsigned integer represented by v to floating-pointer|

## Variables
![img_var_pad.png](https://github.com/differentrain/LocalcDocuments/raw/main/Img/img_var_pad.png)

You can add variables to variable-list, and reference them via `$varName` in expressions. You can also modify an exist variable by clicking it.

The text-box who is used for set the vaule of variable provides calculation for [expressions](https://github.com/differentrain/LocalcDocuments#expressions), **but the integer type for calculating is set to `Int64`**. 

## Drag-Drop

You can drag a number-box and drop it on another number-box to swap them values. By pressing `Shift` key, The value in dragged number-box would be copied to the target number-box. And you can reorder number-boxes simply by pressing `Control` key.

You can also drag a number-box to Exp-pad as a reference, and the result-area(if it is not empty or invalid value) in Exp-pad can be dragged to any number-box too. 

On Var-pad, If you drag a number-box to the text-box which is used for entering variable value, the value will be copied to the text-box. You can also drag and drop number-box on a existed variable who is in the variable-list to update it's value, and the variable can be dragged to number-box.

## Shortcuts

**\*  : Perform on the selected number-box.**

|  shortcuts  | effect  | remark |
|  :---:  | ---  |--- |
|`0`<br/>-<br/>`9`|Enter `0` -`9`|*\** Only available on Num-pad or Bit-Pad|
|`A`<br/>-<br/>`F`|Enter `A` -`F`|*\** Only available on Num-pad or Bit-Pad|
|`Escape`|CLR|*\** Only available on Num-pad or Bit-Pad|
|`Backspack`|BKSP|*\** Only available on Num-pad or Bit-Pad|
|`+`|ADD|*\** Only available on Num-pad or Bit-Pad|
|`-`|SUB|*\** Only available on Num-pad or Bit-Pad|
|`*`|MUL|*\** Only available on Num-pad or Bit-Pad|
|`/`|DIV|*\** Only available on Num-pad or Bit-Pad|
|`%`|MOD|*\** Only available on Num-pad or Bit-Pad|
|`&`|AND|*\** Only available on Num-pad or Bit-Pad|
|`\|`|OR|*\** Only available on Num-pad or Bit-Pad|
|`^`|XOR|*\** Only available on Num-pad or Bit-Pad|
|`~`|NOT|*\** Only available on Num-pad or Bit-Pad|
|`N`|NEG|*\** Only available on Num-pad or Bit-Pad|
|`Ctrl`\+`C`|Copy|*\** Only available on Num-pad or Bit-Pad|
|`Ctrl`\+`V`|Paste|*\** Only available on Num-pad or Bit-Pad|
|`Ctrl`\+`X`|Copy and set the value to 0|*\** Only available on Num-pad or Bit-Pad|
|`F1`|Select 1st number-box||
|`F2`|Select 2nd number-box||
|`F3`|Select 3rd number-box||
|`F4`|Select 4th number-box||
|`F5`|Toggle global integer type between signed/unsigned||
|`F6`|Change global integer size||
|`F9`|HEX|*\** |
|`F10`|DEX|*\** |
|`F11`|OCT|*\** |
|`F12`|BIN|*\** |
