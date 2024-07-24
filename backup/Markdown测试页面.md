[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

建议: 这部分理解看得懂就可以了, 不用作额外的练习
## [常量与变量 (Constants and Variables)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Constants-and-Variables)
---
🕐 先赋类型再赋值:
```swift
var user: String
user = "root"
```

🕑 赋值时自动推断类型:
```swift
let user = "root"
var passwd = 123456
```

> 在实践中, 更多使用的是这种方式

🕒 同时操作多个量:
```swift
var x = 0.0, y = 0.1, z = 0.2
var m, n: Double
```
## [注释 (Comments)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Comments)
---
🕐 单行注释:
```swift
// This is a comment
```

🕑 多行注释:
```swift
/* This is also a comment
but is written over multiple lines. */
```

🕒 多级注释 (可进行展开或折叠):
```
/* This is the start of the first multiline comment.
    /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */
```
## [分号 (Semicolons)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Semicolons)
---
不作强制要求, 但也可使用:
```swift
let name = "root"; print(name)
```
## [整数 (Integers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Integers)
---
一般整数使用 `Int` 即可, 如果要使用指定位数的也有
### [整数范围 (Integer Bounds)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Integer-Bounds)

获取类型的最值:
```swift
let minValue = UInt8.min
let maxValue = UInt8.maxv
```
### [Int](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Int)

类型 `Int` 的位数根据平台而定
### [UInt](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#UInt)

类型 `UInt` 的位数根据平台而定
## [浮点数 (Floating-Point Numbers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Floating-Point-Numbers)
---
- `Double` : 64-bit (至少表示 15 位小数)
- `Float` : 32-bit (差不多表示 6 位小数)
## [类型安全与类型推断 (Type Safety and Type Inference)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Type-Safety-and-Type-Inference)
---
- 类型安全: 自动检查类型是否匹配
- 类型推断: 根据值自动推断合适的类型
## [数值字面量 (Numeric Literals)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Numeric-Literals)
---
🕐 不同进制表示法:
```swift
let decimalInteger = 17
let binaryInteger = 0b10001 // 二进制
let octalInteger = 0o21 // 八进制
let hexadecimalInteger = 0x11 // 十六进制
```

🕑 不同进制的指数表示法:
```swift
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0 // 只支持十六进制
```

🕒 填充及下划线分隔表示法:
```swift
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
```
## [数值类型转换 (Numeric Type Conversion)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Numeric-Type-Conversion)
---
🕐 赋值不在数值类型范围内的值将会报错

🕑 不同数值类型间不能直接操作,需显式进行类型转换:
```swift
let x: UInt16 = 2_000
let y: UInt8 = 1
let z = x + UInt16(y)
```
## [类型别名 (Type Aliases)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Type-Aliases)
---
给类型取一个别名:
```swift
typealias MyType = UInt16
var n = MyType.min
```
## [布尔值 (Booleans)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Booleans)
---
🕐 赋值:
```swift
let t = true
let f = false
```

🕑 不是非 0 就是 true, 布尔就是布尔:
```swift
let n = 1
if n {
    // error
}
```

> 这是与其他语言较为不同的地方
## [元组 (Tuples)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Tuples)
---
🕐 元组定义与赋值:
```swift
let info = ("root", 123456)
let (user, passwd) = info
```

🕑 赋值时使用下划线忽略:
```swift
let (user1, _) = info
```
### 索引 (Index)

> 这是比较新颖的地方, 某种程度上看起来像是 python 的字典

🕐 通过数值索引获取元素:
```swift
print(info.0, info.1)
```

🕑 通过名称获取元素:
```swift
let info = (user: "root", passwd: 123456)
print(info.user, info.passwd)
```
## [可选类型 (Optionals)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Optionals)
---
🕐 定义方式: 在类型后加上 `?`

🕑 可选类型要么有值要么为 `nil`:
```swift
var n: Int? = 404
n = nil // 可选类型可赋值 nil
```

> Swift 是非空类型的安全系统, 其要求每个量的类型都是明确的, 因此直接给量赋 `nil` 是不安全的. 推荐在可能出现 `nil` 的地方都使用可选类型, 可以把可选类型理解为一个安全的包装器
### [可选类型绑定 (Optional Binding)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Optional-Binding)

即在条件表达式中使用赋值语句提取可选类型中的值

🕐 当有值时, 条件表达式为 `true`, 同时提取值:
```swift
if let n = Int("123") { // 类型转换会返回可选值
    print("The number is \(n)")
} else {
    print("error")
}
```

🕑 当条件表达式中的局部变量名与外层相同时可简写:
```swift
let n = Int("123")
if let n {
    print("My number is \(n)")
}
```

🕒 同时进行多个可选类型绑定:
```swift
if let a = Int("4"), let b = Int("42"), a < b && b < 100 {
    print("\(a) < \(b) < 100")
}
```

> 到这里可以将"可选类型绑定"理解为: 在条件语句中赋值可选类型, 就好像是使用普通类型一样
### [提供备选值 (Providing a Fallback Value)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Providing-a-Fallback-Value)

使用 `??` 解包可选类型, 当其为 `nil` 时提供备选值:
```swift
let name: String? = nil
let greeting = "Hello, " + (name ?? "root") + "!"
print(greeting)
```
### [强制解包 (Force Unwrapping)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Force-Unwrapping)

使用 `!` 解包可选值, 若为 `nil` 将触发错误:
```swift
let s = "123s"
let i = Int(s)
let n = i!
```
### [隐式解包 (Implicitly Unwrapped Optionals)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Implicitly-Unwrapped-Optionals)

适用于"当可选值有值后就一定保持有值"的情况

🕐 定义方式: 类型后加上 `!`, 相当于可隐式解包的可选类型

🕑 比可选类型多了自动隐式解包功能:
```swift
let user: String! = "root"
let name: String = user
```
## [错误处理 (Error Handling)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Error-Handling)
---
🕐 使用 `throws` 表明一个函数会抛出错误:
```swift
func f() throws {
	...
}
```

🕑 处理错误的语句:
```swift
do {
	try f()
} catch {
	...
} catch {
	... 
}
```
`try` 表明该函数可能会抛出错误, `catch` 用于捕获错误
## [断言和前置条件 (Assertions and Preconditions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Assertions-and-Preconditions)
---
"断言"和"前置条件"都是用于捕获意外的错误, 当不满足时中断程序执行; 前者只在开发环境中生效

> 与"错误处理"不同的是, 错误处理处理的是可预见的错误, 而这里的错误是意外的, 不可预知的, 因而不一定能够复现
### [使用断言 Debug (Debugging with Assertions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Debugging-with-Assertions)

```swift
let n = -3
assert(n >= 0, "this is an error description") // 描述可省略
```

手动触发断言错误:
```swift
let n = -3
if n > 0 {
    assertionFailure("error")
} else {
    print("pass")
}
```
### [执行前置条件 (Enforcing Preconditions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Enforcing-Preconditions)

```swift
let n = -3
precondition(n > 0, "this is an error descriptoin")
```

手动触发前置条件错误:
```swift
let n = -3
if n > 0 {
    preconditionFailure("error")
} else {
    print("pass")
}
```

> 关于这部分的使用还可以更进一步, 不过目前了解一下就足够了


建议: 这部分理解看得懂就可以了, 不用作额外的练习
## [术语 (Terminology)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Terminology)
---
学一下英语:
- _Unary_: 一元
- _Binary_: 二元
- _Ternary_: 三元
## [算术运算符 (Arithmetic Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Arithmetic-Operators)
---
🕐 加减乘除:
```swift
1 + 2
5 - 3
2 * 3
10.0 / 2.5 
```

🕑 字符串拼接:
```swift
"hello, " + "world"
```
### [取余运算符 (Remainder Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Remainder-Operator)

符号跟着被除数走:
```swift
9 % 4    // 1
-9 % 4   // -1
```
### [一元负号操作符 (Unary Minus Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Unary-Minus-Operator)

```swift
let x = 3
let y = -x
let z = -y
```
### [一元正号运算符 (Unary Plus Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Unary-Plus-Operator)

```swift
let n = +3
```

> 实际不会发生任何影响
## [复合赋值运算符 (Compound Assignment Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Compound-Assignment-Operators)
---
举个例子:
```swift
var n = 1
n += 2
```
## [比较运算符 (Comparison Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Comparison-Operators)
---
🕐 举个例子:
```swift
1 == 1
2 != 1
2 > 1
1 < 2
1 >= 1
2 <= 1
```

🕑 元组会逐个元素进行比较:
```swift
(1, "a") < (2, "c")
```
## [三元条件运算符 (Ternary Conditional Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Ternary-Conditional-Operator)
---
```swift
let x = 2
let b = true
let y = x + (b ? 10: 20)
```
## [空值合并运算符 (Nil-Coalescing Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Nil-Coalescing-Operator)
---
即 `??`: [[01 基础部分 (The Basics)#[提供备选值 (Providing a Fallback Value)](https //docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics Providing-a-Fallback-Value)|here]]
```swift
let n = "root"
var s: String?
let m = s ?? n
```
## [区间运算符 (Range Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Range-Operators)
---
获取区间内的离散数值
### [闭区间运算符 (Closed Range Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Closed-Range-Operator)

左闭右闭:
```swift
for i in 1...5 {
    print(i)
}
```
### [半开区间运算符 (Half-Open Range Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Half-Open-Range-Operator)

左闭右开:
```swift
for i in 1..<5 {
    print(i)
}
```
### [单侧区间 (One-Sided Ranges)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#One-Sided-Ranges)

🕐 右穷尽:
```swift
let m = ["a", "b", "c", "d"]
for i in m[2...] {
    print(i)
}
```

🕑 左穷尽:
```swift
let m = ["a", "b", "c", "d"]
for i in m[...2] {
    print(i)
}
```

🕒 左穷尽右开:
```swift
let m = ["a", "b", "c", "d"]
for i in m[..<2] {
    print(i)
}
```

🕓 判断数字是否在区间中:
```swift
let range = ...5
print(range.contains(7))
```
## [逻辑运算符 (Logical Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Logical-Operators)
---
### [非运算符 (Logical NOT Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Logical-NOT-Operator)

```swift
let f = false
if !f {
    print("true")
}
```
### [并且运算符 (Logical AND Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Logical-AND-Operator)

```swift
let t = true
let f = false
if t && f {
    print("true")
} else {
    print("false")
}
```
### [或运算符 (Logical OR Operator)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Logical-OR-Operator)

```swift
let t = true
let f = false
if t || f {
    print("true")
} else {
    print("false")
}
```
### [组合逻辑运算符 (Combining Logical Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Combining-Logical-Operators)

上述逻辑运算符可以组合使用
### [显式使用括号 (Explicit Parentheses)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators/#Explicit-Parentheses)

可以使用 `()` 改变优先级或者语法美观

建议: 重点理解一下字符串的底层表示, 相应部分从 **Unicode** 开始看起
## [字符串字面量 (String Literals)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#String-Literals)
---
```swift
let s = "hello"
```
### [多行字符串字面量 (Multiline String Literals)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Multiline-String-Literals)

🕐 多行字符串表示法, :
```swift
let s = """
hear me now and bear witness to my vow
night gathers and now my watch begins
"""
```

🕑 使用 `\` 在代码层面换行, 实际文字不换行:
```swift
let s = """
hear me now and bear witness\
to my vow
night gathers and now my watch begins
"""
```

🕒 首行缩进以末尾 `"""` 所在行的缩进为基准:

![[Pasted image 20240107172813.png]]
### [特殊字符 (Special Characters in String Literals)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Special-Characters-in-String-Literals)

转义字符有:
- `\0` (空字符), `\\` (反斜杠), `\t` (水平制表符), `\n` (换行), `\r` (回车), `\"` (双引号), `\'` (单引号)
- `\u{`_n_`}`, 其中 n 是 1-8 位的十六进制数, 即 Unicode 标量值

```swift
let a = "\u{24}"        // $,  Unicode scalar U+0024
let b = "\u{2665}"      // ♥,  Unicode scalar U+2665
let c = "\u{1F496}" // 💖, Unicode scalar U+1F496
```
### [扩展的字符串界定符 (Extended String Delimiters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Extended-String-Delimiters)

通过在字符串外层使用 `#` (任意个数)达到在原生字符串的效果

🕐 以下是等价的:
```swift
let s1 = #"Here are : \n"#
let s2 = ##"Here are : \n"##
let s3 = ###"Here are : \n"###
```

🕑 在 `\` 后添加界定符以恢复特殊字符的效果:
```swift
let s1 = #"Here are : \#n"#
let s2 = ##"Here are : \##n"##
let s3 = ###"Here are : \##n"###
```
## [初始化空字符串 (Initializing an Empty String)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Initializing-an-Empty-String)
---
🕐 初始化空字符串:
```swift
var s1 = ""
var s2 = String() 
```

🕑 判断是否为空:
```swift
if s.isEmpty {
	...
}
```
## [字符串的可变性 (String Mutability)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#String-Mutability)
---
是否可变取决于是 `var` 还是 `let`
## [字符串是值类型 (Strings Are Value Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Strings-Are-Value-Types)
---
值类型意味着是值存储和传递, 而不是指针
## [使用字符 (Working with Characters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Working-with-Characters)
---
🕐 字符串是字符数组:
```swift
for c in "Dog!🐶" {
    print(c)
}
```

🕑 定义字符:
```swift
let c: Character = "!"
```

🕒 将字符数组转换为字符串:
```swift
let c: [Character] = ["C", "a", "t", "!", "🐱"]
let s = String(c)
```
## [拼接字符和字符串 (Concatenating Strings and Characters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Concatenating-Strings-and-Characters)
---
🕐 拼接:
```swift
let a = "hello"
let b = " world"
let s = a + b
```

🕑 复合拼接:
```swift
var s = "hello"
s += " world"
```

🕒 末尾添加字符:
```swift
var s = "hello"
s.append("!")
```
## [字符串插值 (String Interpolation)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#String-Interpolation)
---
🕐 使用 `\()` 在字符串中进行插值:
```swift
var a = "root"
let b = "hello \(a)"
```

🕑 在扩展的字符串界定符中进行插值:
```swift
print(#"6 times 7 is \#(6 * 7)."#)
```
## [Unicode](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Unicode)
---
`String` 完全符合 *Unicode 标准*, 组成字符串的基本单位不再是"字符"
### [Unicode 标量值 (Unicode Scalar Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Unicode-Scalar-Values)

`String` 由 *Unicode 标量值*组成
### [扩展字素簇 (Extended Grapheme Clusters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Extended-Grapheme-Clusters)

`Character` 表示一个单独的"扩展字素簇", 即可由多个 *Unicode 标量值*组成的序列

🕐 如二者都表示 `é`:
```swift
let a: Character = "\u{E9}"
let b: Character = "\u{65}\u{301}" 
print(a == b) // true
```

🕑 扩展字素簇可通过组合或拆解的形式表示:
```swift
let a: Character = "\u{D55C}" // 한 
let b: Character = "\u{1112}\u{1161}\u{11AB}" // ᄒ, ᅡ, ᆫ
print(a == b) // true
```

🕒 可以给 Unicode 标量进行字符修饰; 如给它添加某个符号:
```swift
let a: Character = "\u{E9}\u{20DD}"
```
但是其仍然被视为 `Character`

🕔 组合地区指示符:
```swift
let a: Character = "\u{1F1FA}\u{1F1F8}"
print(a) // 🇺🇸
```
## [计算字符数量 (Counting Characters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Counting-Characters)
---
```swift
var s = "root"
print(s.count) // 4
```

> 计算字符数量需要遍历最底层 *Unicode 标量值*, 因而字符串越长性能也越差
## [访问和修改字符串 (Accessing and Modifying a String)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Accessing-and-Modifying-a-String)
---
### [字符串索引 (String Indices)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#String-Indices)

每个字符串值都有其对应的索引类型 *String.Index* 来标识每个字符所在的位置, 由于字符串的特殊组成, 需要遍历 *Unicode 标量值*来决定每个字符的位置, 因而不能直接使用数值索引

```swift
let s = "abcdefg"
```

🕐 获取首字符:
```swift
s[s.startIndex] // a
```

🕑 获取指定字符前或后的字符:
```swift
s[s.index(before: s.endIndex)] // g
s[s.index(after: s.startIndex)] // b
```
其中 *endIndex* 指向最后一个字符的下一位置

🕒 获取指定偏移位置的索引:
```swift
let index = s.index(s.startIndex, offsetBy: 3)
print(s[index]) // d
```

🕓 通过索引遍历字符串:
```swift
for i in s.indices {
    print(s[i])
}
```

> 这种索引类型适用于任何遵循 *Collection* 协议的类型, 比如 *Array*, *Dictionary* 和 *Set*
### [插入和移除 (Inserting and Removing)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Inserting-and-Removing)

```swift
var s = "abcdefg"
```

🕐 在指定索引处插入字符:
```swift
s.insert("h", at: s.endIndex)
```

🕑 移除指定索引处的字符:
```swift
s.remove(at: s.index(before: s.endIndex))
```

🕒 移除指定索引范围内的字符:
```swift
let range = s.index(s.endIndex, offsetBy: -2) ..< s.endIndex
s.removeSubrange(range)
```

> 上述方法适用于任何遵循 *Collection* 协议的类型, 比如 *Array*, *Dictionary* 和 *Set*
## [子串 (Substrings)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Substrings)
---
子串是一个类型 `Substring`, 相当于是字符串的视图, 当你对子串进行修改时, 其会被转换为字符串
![[Pasted image 20240221154649.png|350]]

🕐 通过索引获取子串:
```swift
var s = "abc,def,g"
let index = s.firstIndex(of: ",") ?? s.endIndex
let a = s[..<index]
```

🕑 将字串转换为字符串:
```swift
let b = String(a)
```
## [字符串比较 (Comparing Strings)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Comparing-Strings)
---
🕐 比较字符串的值是否相等:
```swift
let a = "I'm root"
let b = "I'm root"
if a == b {
    print("equal")
}
```

🕑 需要注意扩展字素簇的情况:
```swift
let a = "Voulez-vous un caf\u{E9}?"
let b = "Voulez-vous un caf\u{65}\u{301}?"
if a == b {
    print("equal")
}
```
因为 *\\\u{65}\\\u{301}* 为 *\\\u{E9}* 的扩展表示
### [前缀与后缀 (Prefix and Suffix Equality)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Prefix-and-Suffix-Equality)

```swift
let list = [
    "Act 1 Scene 1: Verona, A public place",
    "Act 1 Scene 2: Capulet's mansion",
    "Act 1 Scene 3: A room in Capulet's mansion",
    "Act 1 Scene 4: A street outside Capulet's mansion",
    "Act 1 Scene 5: The Great Hall in Capulet's mansion",
    "Act 2 Scene 1: Outside Capulet's mansion",
    "Act 2 Scene 2: Capulet's orchard",
    "Act 2 Scene 3: Outside Friar Lawrence's cell",
    "Act 2 Scene 4: A street in Verona",
    "Act 2 Scene 5: Capulet's mansion",
    "Act 2 Scene 6: Friar Lawrence's cell"
]
```

判断 `String` 是否拥有指定的前缀或后缀:
```swift
for i in list {
    if i.hasPrefix("Act 1") { // 是否拥有前缀
        print("prefix")
    }
    
    if i.hasSuffix("cell") { // 是否拥有后缀
        print("suffix")
    }
}
```
## [字符串的 Unicode 表示形式 (Unicode Representations of Strings)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Unicode-Representations-of-Strings)
---
获取 `String` 的不同表示方式

```swift
let dogString = "Dog‼🐶"
```
### [UTF-8 形式 (UTF-8 Representation)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#UTF-8-Representation)
![[Pasted image 20240226165335.png]]
```swift
for codeUnit in dogString.utf8 {
    print("\(codeUnit) ", terminator: "")
}
// 68 111 103 226 128 188 240 159 144 182
```
### [UTF-16 形式 (UTF-16 Representation)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#UTF-16-Representation)
![[Pasted image 20240226165345.png|550]]
```swift
for codeUnit in dogString.utf16 {
    print("\(codeUnit) ", terminator: "")
}
// 68 111 103 8252 55357 56374 
```
### [Unicode 标量值形式 (Unicode Scalar Representation)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/stringsandcharacters#Unicode-Scalar-Representation)
![[Pasted image 20240226165504.png|500]]
```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar.value) ", terminator: "")
}
// 68 111 103 8252 128054 
```

🕐 可以直接将该标量值转换为 `String`:
```swift
for scalar in dogString.unicodeScalars {
    print("\(scalar) ")
}
// D
// o
// g
// ‼
// 🐶
```

建议: 这部分没什么难点, 了解下各个类型的操作就行
## [集合的可变性 (Mutability of Collections)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Mutability-of-Collections)
---
是否可变取决于是 `var` 还是 `let`
## [数组 (Arrays)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Arrays)
---
同一类型值的顺序集合
### [数组类型简记法 (Array Type Shorthand Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Array-Type-Shorthand-Syntax)

数组的完整写法为: `Array<Element>`, 但通常简写为: `[Element]`
### [创建空数组 (Creating an Empty Array)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Empty-Array)

```swift
var a: [Int] = []
a.append(3)
a = []
```
### [创建有默认值的数组 (Creating an Array with a Default Value)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Array-with-a-Default-Value)

具有 3 个相同值的数组:
```swift
var a = Array(repeating: 0.0, count: 3)
```
### [合并两个数组 (Creating an Array by Adding Two Arrays Together)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Array-by-Adding-Two-Arrays-Together)

```swift
var a = Array(repeating: 0.0, count: 3)
var b = Array(repeating: 2.5, count: 4)
var c = a + b
```
### [通过数组字面量创建数组 (Creating an Array with an Array Literal)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Array-with-an-Array-Literal)

```swift
var a: [String] = ["Eggs", "Milk"]
```
### [访问和修改数组 (Accessing and Modifying an Array)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Accessing-and-Modifying-an-Array)

```swift
var a = [1, 2, 3, 4, 5]
```

🕐 获取的元素个数:
```swift
a.count
```

🕑 判断数组是否为空:
```swift
a.isEmpty
```

🕒 在"数组"末尾添加元素:
```swift
a.append(6)
```

🕓 通过索引获取和修改数组:
```swift
let e = array[0]
array[0] = "root"
array[4...6] = ["a", "b"]
```

🕔 插入或移除指定位置的元素:
```swift
a.insert(88, at: 0)
a.remove(at: 1)
```

🕕 弹出最后一位元素:
```swift
let p = a.removeLast()
```
### [遍历数组 (Iterating Over an Array)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Iterating-Over-an-Array)

🕐 遍历数组中的元素:
```swift
for v in array {
}
```

🕑 遍历数组的索引和元素:
```swift
for (i, v) in array.enumerated() {
}
```
## [集合 (Sets)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Sets)
---
同一类型的唯一值的无序集合
### [集合的哈希值 (Hash Values for Set Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Hash-Values-for-Set-Types)

集合类型必须是可哈希的, 因为要进行值比较
### [集合类型语法 (Set Type Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Set-Type-Syntax)

集合类型写作: `Set<Element>`
### [创建和初始化空集合 (Creating and Initializing an Empty Set)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-and-Initializing-an-Empty-Set)

```swift
var s = Set<Character>()
s.insert("a")
s = []
```
### [通过数组字面量创建集合 (Creating a Set with an Array Literal)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-a-Set-with-an-Array-Literal)

```swift
var s: Set<String> = ["Rock", "Classical", "Hip hop"]
```

可以简写为:
```swift
var s: Set = ["Rock", "Classical", "Hip hop"]
```
### [访问和修改集合 (Accessing and Modifying a Set)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Accessing-and-Modifying-a-Set)

🕐 获取个数:
```swift
s.count

```

🕑 判断否为空:
```swift
s.isEmpty
```

🕒 插入元素:
```swift
s.insert("a")

```

🕓 移除元素:
```swift
s.remove("a")
```
 
 🕓 是否包含某元素:
```
s.contains("a")
```
### [遍历集合 (Iterating Over a Set)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Iterating-Over-a-Set)

🕐 遍历集合元素:
```swift
for i in s {
}
```

🕑 排序后遍历:
```swift
for i in s.sorted() {
}
```
## [执行集合操作 (Performing Set Operations)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Performing-Set-Operations)
---
数学中的集合操作
### [基础集合操作 (Fundamental Set Operations)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Fundamental-Set-Operations)

![[Pasted image 20240107203713.png|550]]
### [集合的成员资格和等价性 (Set Membership and Equality)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Set-Membership-and-Equality)

```swift
let a: Set = ["🐶", "🐱"]
let b: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let c: Set = ["🐦", "🐭"]
```

🕐 判断集合是否相等:
```swift
a == b
```

🕑 集合操作:

```swift
a.isSubset(of: b) // 子集
a.isStrictSubset(of: b) // 严格子集
b.isSuperset(of: a) // 超集
b.isDisjoint(with: c) // 无交集
```
## [字典 (Dictionaries)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Dictionaries)
---
无序的, key 类型相同, value 类型相同
### [字典类型简记法 (Dictionary Type Shorthand Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Dictionary-Type-Shorthand-Syntax)

字典定义为: `Dictionary<Key, Value>`, 可以简写为: `[Key: Value]`
### [创建空字典 (Creating an Empty Dictionary)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Empty-Dictionary)

```swift
var d: [Int: String] = [:]
```

🕐 赋值:
```swift
d[16] = "sixteen"
```
### [通过字典字面量创建字典 (Creating a Dictionary with a Dictionary Literal)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-a-Dictionary-with-a-Dictionary-Literal)

```swift
var d: [String: Int] = ["a": 18, "b": 28]
```

🕐 可以简写为:
```swift
var d = ["a": 18, "b": 28]
```
### [访问和修改字典 (Accessing and Modifying a Dictionary)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Accessing-and-Modifying-a-Dictionary)

🕐 获取元素个数,
```swift
d.count
```

🕑 判断是否为空:
 ```swift
d.isEmpty
```

🕒 通过 key 添加或修改 value:
```swift
d["c"] = 19
```

🕓 更新并返回旧 value (可选类型):
```swift
var d  = ["a": 18, "b": 28]
if let v = d.updateValue(19, forKey: "a") {
    print(v)
}
```

🕔 获取 value (可选类型):
```swift
var d  = ["a": 18, "b": 28]
if let v = d["b"] {
    print(v)
}
```

🕕 通过赋值方式删除元素:
```swift
dict[key] = nil
```

🕖 通过 key 删除并返回对应的 value (可选类型):
```swift
var d  = ["a": 18, "b": 28]
if let v = d.removeValue(forKey: "a") {
    print(v)
}
```
### [遍历字典 (Iterating Over a Dictionary)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Iterating-Over-a-Dictionary)

🕐 遍历 key 和 value:
```swift
var d  = ["a": 18, "b": 28]
for (k, v) in d {
}
```

🕑 遍历 key :
```swift
for k in d.keys {
}
```

🕒 遍历 value:
```swift
for v in d.values {
}
```

🕓 将 key 或 value 转换为数组:
```swift
var d  = ["a": 18, "b": 28]
let a = [String](d.keys)
let b = [Int](d.values)
```

🕔 原地排序 key:
```swift
d.keys.sorted()
```

🕕 原地排序 value:
```swift
d.values.sorted()
```




<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->