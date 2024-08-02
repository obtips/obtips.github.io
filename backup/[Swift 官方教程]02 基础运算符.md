[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

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
即 `??`: [01 基础部分: 提供备选值 (Providing a Fallback Value)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Providing-a-Fallback-Value)

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


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->