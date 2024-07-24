[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

## [枚举语法 (Enumeration Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Enumeration-Syntax)
---
🕐 定义: 
```swift
enum CompassPoint {
    case north
    case south
    case east
    case west
}

enum Planet {
    case mercury, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

🕑 获取:
```swift
var d = CompassPoint.west
```

🕒 若变量的类型已知, 则可以省略枚举类型:
```swift
d = .east
```
## [在 switch 中使用枚举值 (Matching Enumeration Values with a Switch Statement)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Matching-Enumeration-Values-with-a-Switch-Statement)
---
```swift
switch d {
case .north:
    print("north")
case .south:
    print("south")
case .east:
    print("east")
case .west:
    print("west")
}
```
## [遍历枚举的 case (Iterating over Enumeration Cases)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Iterating-over-Enumeration-Cases)
---
使用 `CaseIterable` 协议:
```swift
enum Beverage: CaseIterable {
    case coffee, tea, juice
}
```

🕐 查看枚举数:
```swift
let n = Beverage.allCases.count
print(n)
```

🕑 遍历:
```swift
for i in Beverage.allCases {
    print(i)
}
```
## [关联值 (Associated Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Associated-Values)
---
给枚举值设置类型: 
```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}
```

获取枚举值并为其设定类型值:
```swift
var code = Barcode.upc(8, 85909, 51226, 3)
code = .qrCode("ABCDEFGHIJKLMNOP")
```

 在 `switch` 中提取枚举值的类型值:
```swift
switch code {
case .upc(let a, let b, let c, let d):
    print("UPC: \(a), \(b), \(c), \(d).")
case .qrCode(let a):
    print("QR code: \(a).")
}
```
## [原始值 (Raw Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Raw-Values)
---
给枚举添加类型, 随后设置原始值:
```swift
enum ch: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
```
每个原始值必须是同一类型且唯一
### [隐式原始值赋值 (Implicitly Assigned Raw Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Implicitly-Assigned-Raw-Values)

🕐 `Int` 类枚举给首个原始值赋值,  后续的原始值会自动赋值并自增:
```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```

🕑 `String` 类枚举的原始值为其本身转换为字符串类型:
```swift
enum CompassPoint: String { case north, south, east, west }
```

🕒 获取原始值:
```swift
let e = Planet.earth.rawValue
let w = CompassPoint.west.rawValue
```
### [从原始值进行初始化 (Initializing from a Raw Value)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Initializing-from-a-Raw-Value)

从原始值获取对应的枚举值:
```swift
let p = Planet(rawValue: 7)
```
返回的是可选值
## [递归枚举 (Recursive Enumerations)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations#Recursive-Enumerations)
---
使用 `indirect` 定义递归枚举:
```swift
enum Expression {
    case num(Int)
    indirect case add(Expression, Expression)
    indirect case multi(Expression, Expression)
}
```
可以被改写为:
```swift
indirect enum Expression {
    case num(Int)
    case add(Expression, Expression)
    case multi(Expression, Expression)
}
```

创建对应的枚举常量:
```swift
let five = Expression.num(5)
let four = Expression.num(4)
let sum = Expression.add(five, four)
let product = Expression.multi(sum, Expression.num(2))
```

运用它们:
```swift
func evaluate(_ e: Expression) -> Int {
    switch e {
    case let .num(v):
        return v
    case let .add(left, right):
        return evaluate(left) + evaluate(right)
    case let .multi(left, right):
        return evaluate(left) * evaluate(right)
    }
}
print(evaluate(product))
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->