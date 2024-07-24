[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

## [实例方法 (Instance Methods)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#Instance-Methods)
---
属于实例的方法
### [`self` 属性 (The self Property)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#The-self-Property)

`self` 指向自身实例, 一般用于区分同名的量
```swift
struct Point {
    var x = 0.0, y = 0.0
    func compare(x: Double) -> Bool {
        return self.x > x
    }
}
```
### [在实例方法中修改值类型 (Modifying Value Types from Within Instance Methods)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#Modifying-Value-Types-from-Within-Instance-Methods)

默认情况下, 值类型中的方法不能修改值类型的属性, 但可以通过 `mutating` 实现:
```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
var somePoint = Point(x: 1.0, y: 1.0)
somePoint.moveBy(x: 2.0, y: 3.0)
```

> 这里给出个人理解, 因为值类型就是一个值, 你调用了其中的方法对其进行修改, 那么之前的赋值就变了, 而值应该是保持不变的, 所以这么做更加的安全
### [在可变方法中给 `self` 赋值 (Assigning to self Within a Mutating Method)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#Assigning-to-self-Within-a-Mutating-Method)

🕐 可以直接给 `self` 赋值, 这是上述代码的另一种实现:
```swift
struct Point {
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        self = Point(x: x + deltaX, y: y + deltaY)
    }
}
```

在🕑 枚举中的用法:
```swift
enum TriStateSwitch {
    case off, low, high
    mutating func next() {
        switch self {
        case .off:
            self = .low
        case .low:
            self = .high
        case .high:
            self = .off
        }
    }
}
var ovenLight = TriStateSwitch.low
ovenLight.next()
ovenLight.next()
```
## [类型方法 (Type Methods)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/methods#Type-Methods)

即属于类型的方法, 在方法前使用 `static` , 对于类也可以使用 `class`


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->