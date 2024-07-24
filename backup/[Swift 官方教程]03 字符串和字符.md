[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

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


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->