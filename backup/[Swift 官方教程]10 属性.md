[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

**Stored Properties** 由类和结构体提供, **Computed Properties** 由类,结构体和枚举提供
## [存储型属性 (Stored Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Stored-Properties)
---
实例中的变量或常量
```swift
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}
```
### [常量结构实例的存储型属性 (Stored Properties of Constant Structure Instances)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Stored-Properties-of-Constant-Structure-Instances)

如果一个实例是常量类型, 无法修改其 **stored properties**
### [惰性存储型属性 (Lazy Stored Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Lazy-Stored-Properties)

即 **stored properties** 值在它被第一次使用时才进行计算, 且必须是 `var`, 因为常量必须在初始化完成之前总是具有值:
```swift
class DataImporter {
    var filename = "data.txt"
}

class DataManager {
    lazy var importer = DataImporter()
    var data: [String] = []
}
```
### [存储型属性和实例变量 (Stored Properties and Instance Variables)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Stored-Properties-and-Instance-Variables)

Swift 和 Oc 之间属性和实例变量的操作差异, 不管
## [计算型属性 (Computed Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties#Computed-Properties)
---
即通过计算得到的值, 并不是直接赋值存储的:
```swift
struct MyStruct {
    var a: Int
    var b: Int
    var c: Int {
        get {
            let m = a * 10
            let n = b * 10
            return m + n
        }
        set(num) {
            a = num / 10
            b = num / 2
        }
    }
}
```

访问 **computed properties** 是调用其 `get` 方法:
```swift
var s = MyStruct(a: 3, b: 5)
print(s.c) // 80
```

访问 **computed properties** 是调用其 `set` 方法:
```swift
s.c = 10
print(s.a, s.b) // 1 5
```
### [更简洁的 Setter 声明 (Shorthand Setter Declaration)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Shorthand-Setter-Declaration)

`set` 中的参数可以被 `newValue` 替代:
```swift
struct MyStruct {
    var a: Int
    var b: Int
    var c: Int {
        get {
            let m = a * 10
            let n = b * 10
            return m + n
        }
        set {
            a = newValue / 10
            b = newValue / 2
        }
    }
}
```
### [更简短的 Getter 声明 (Shorthand Getter Declaration)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Shorthand-Getter-Declaration)

`get` 中的如果是单行表达式, 则可以简写:
```swift
struct MyStruct {
    var a: Int
    var b: Int
    var c: Int {
        get {
            a*10 + b*10
        }
        set {
            a = newValue / 10
            b = newValue / 2
        }
    }
}
```
### [仅可读的计算型属性 (Read-Only Computed Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Read-Only-Computed-Properties)

一个计算值没有 `set` 方法则为仅可读的, 此时可以对 `get` 进行略写:
```swift
struct MyStruct {
    var a: Int
    var b: Int
    var c: Int {
        a*10 + b*10
    }
}
```
## [属性观察器 (Property Observers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Observers)
---
🕐 在属性被修改的前后被调用. 它可以应用的对象:
- 自定义的 **stored properties**
- 继承来的 **stored properties** 和 **computed properties***
对于自定义的 **computed properties***, 应该在 `set` 中对其进行观察

🕑 有以下 2 种观察者:
- `willSet`: 值被存储前调用; 默认有 `newValue` 参数表示要设置的新值
- `didSet`: 值被存储后调用; 默认有 `oldValue` 参数表示被替换的旧值

🕒 一个总和增加便提示差值的示例:
```swift
class Counter {
    var total: Int = 0 {
        willSet(newNum) {
            print("Set total to \(newNum)")
        }
        didSet {
            if total > oldValue  {
                print("Added \(total - oldValue) steps")
            }
        }
    }
}

let c = Counter()
c.total = 200
c.total = 100
c.total = 300
```

🕓 对于观察者在父子类中的调用, 以及 `in-out` 的值的细节, 用到再说
## [属性包装器 (Property Wrappers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Wrappers)
---
🕐 使用 `@propertyWrapper` 和 `wrappedValue` 定义一个属性包装器:
```swift
@propertyWrapper
struct TwelveOrLess {
    private var number = 0
    var wrappedValue: Int {
        get { number }
        set { number = min(newValue, 12) }
    }
}
```
随后将其运用在属性上:
```swift
struct SmallRectangle {
    @TwelveOrLess var height: Int
    @TwelveOrLess var width: Int
}
```
访问该属性实际上是访问对应的包装器的 `wrappedValue`:
```swift
var rectangle = SmallRectangle()
print(rectangle.height) // 0

rectangle.height = 999
print(rectangle.height) // 12
```

🕑 以上等价于:
```swift
struct SmallRectangle {
    private var _height = TwelveOrLess()
    private var _width = TwelveOrLess()
    var height: Int {
        get { return _height.wrappedValue }
        set { _height.wrappedValue = newValue }
    }
    var width: Int {
        get { return _width.wrappedValue }
        set { _width.wrappedValue = newValue }
    }
}
```
### [为被包装的属性设置Setting Initial Values for Wrapped Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Setting-Initial-Values-for-Wrapped-Properties)

上述代码中被包装的属性不能设定初始值, 下面通过为包装器添加初始化值的方法实现:
```swift
@propertyWrapper
struct SmallNumber {
    private var maximum: Int
    private var number: Int


    var wrappedValue: Int {
        get { return number }
        set { number = min(newValue, maximum) }
    }


    init() {
        maximum = 12
        number = 0
    }
    init(wrappedValue: Int) {
        maximum = 12
        number = min(wrappedValue, maximum)
    }
    init(wrappedValue: Int, maximum: Int) {
        self.maximum = maximum
        number = min(wrappedValue, maximum)
    }
}
```

🕐 调用 `init()`:
```swift
struct ZeroRectangle {
    @SmallNumber var height: Int
    @SmallNumber var width: Int
}

var zeroRectangle = ZeroRectangle()
print(zeroRectangle.height, zeroRectangle.width)
```

🕑 调用 `init(wrappedValue:)`:
```swift
struct UnitRectangle {
    @SmallNumber var height: Int = 1
    @SmallNumber var width: Int = 1
}

var unitRectangle = UnitRectangle()
print(unitRectangle.height, unitRectangle.width)
```
这里的 `wrappedValue` 指的就是被包装属性的初始值

🕒 调用 `init(wrappedValue:maximum:)`:
```swift
struct NarrowRectangle {
    @SmallNumber(wrappedValue: 2, maximum: 5) var height: Int
    @SmallNumber(wrappedValue: 3, maximum: 4) var width: Int
}

var narrowRectangle = NarrowRectangle()
print(narrowRectangle.height, narrowRectangle.width)
```

🕓 上述方式可以灵活混合使用:
```swift
struct MixedRectangle {
    @SmallNumber var height: Int = 1
    @SmallNumber(maximum: 9) var width: Int = 2
}

var mixedRectangle = MixedRectangle()
print(mixedRectangle.height, mixedRectangle.width)
```
### [投射属性包装器中的值 (Projecting a Value From a Property Wrapper)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Projecting-a-Value-From-a-Property-Wrapper)
🕐 在包装器中使用 `projectedValue` 可以将内部值投射到外部:访问方式为 `$` + 被包装的属性名
```swift
@propertyWrapper
struct SmallNumber {
    private var number: Int
    private(set) var projectedValue: Bool

    var wrappedValue: Int {
        get { return number }
        set {
            if newValue > 12 {
                number = 12
                projectedValue = true
            } else {
                number = newValue
                projectedValue = false
            }
        }
    }

    init() {
        self.number = 0
        self.projectedValue = false
    }
}

struct SomeStructure {
    @SmallNumber var someNumber: Int
}
```

🕑 访问方式为 `$` + 被包装的属性名:
```swift
var someStructure = SomeStructure()

someStructure.someNumber = 4
print(someStructure.$someNumber) // false

someStructure.someNumber = 55
print(someStructure.$someNumber) // true
```
## [全局和局部量 (Global and Local Variables)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Global-and-Local-Variables)

全局量总是延迟计算, 而局部量不会
## [类型属性 (Type Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Type-Properties)

属于某个类型的属性, 无论该类型的实例有多少个, 都共享该属性
### [类型属性语法 (Type Property Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Type-Property-Syntax)

使用 `static` 属性:
```swift
struct SomeStructure {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }
}
enum SomeEnumeration {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 6
    }
}
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 27
    }
    class var overrideableComputedTypeProperty: Int {
        return 107
    }
}
```
### [查询和设置类型属性 (Querying and Setting Type Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Querying-and-Setting-Type-Properties)

直接通过类型访问即可:
```swift
print(SomeStructure.storedTypeProperty)
// Prints "Some value."
SomeStructure.storedTypeProperty = "Another value."
print(SomeStructure.storedTypeProperty)
// Prints "Another value."
print(SomeEnumeration.computedTypeProperty)
// Prints "6"
print(SomeClass.computedTypeProperty)
// Prints "27"
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->