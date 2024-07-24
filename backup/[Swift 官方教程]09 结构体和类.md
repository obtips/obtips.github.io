[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

## [对比结构体和类 (Comparing Structures and Classes)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Comparing-Structures-and-Classes)
---
类和结构体很像, 多数情况下结构体+枚举就够了
### [定义语法 (Definition Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Definition-Syntax)

```swift
struct Resolution {
    var width = 0
    var height = 0
}
class VideoMode {
    var resolution = Resolution()
    var interlaced = false
    var frameRate = 0.0
    var name: String?
}
```
### [结构体和类实例 (Structure and Class Instances)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Structure-and-Class-Instances)

```swift
let someResolution = Resolution()
let someVideoMode = VideoMode()
```
### [访问属性 (Accessing Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Accessing-Properties)

```swift
someResolution.width
someVideoMode.interlaced
```
### [结构体成员初始化 (Memberwise Initializers for Structure Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Memberwise-Initializers-for-Structure-Types)

```swift
let vga = Resolution(width: 640, height: 480)
```
## [结构体和枚举是值类型 (Structures and Enumerations Are Value Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Structures-and-Enumerations-Are-Value-Types)
---
结构和枚举都是值类型
## [类是引用类型 (Classes Are Reference Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Classes-Are-Reference-Types)

类是引用类型
### [身份运算符 (Identity Operators)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Identity-Operators)

使用 `==` 鉴定两个对象是否是同一个实例
### [指针 (Pointers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Pointers)

Swift 中的引用并不是直接的实例内存地址, 即不是指针, 但是也提供了指针类型



<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->