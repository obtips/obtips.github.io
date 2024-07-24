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



<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->