[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

构造是一个实例被创建前的准备工作, 其通过构造函数实现
## [为存储值设置初始值 (Setting Initial Values for Stored Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization#Setting-Initial-Values-for-Stored-Properties)
---
### [构造函数 (Initializers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Initializers)

🕐 使用 `init` 创建构造函数:
```swift
struct Db {
    var rows: Int
    init() {
        rows = 10
    }
}
```

🕑 调用构造函数:
```swift
var db = Db()
print(db.rows) // 10
```
### [默认属性值 (Default Property Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Default-Property-Values)

上述也可以直接通过属性赋默认值实现:
```swift
struct Db {
    var rows = 10
}
```

> 如果实例中的属性的默认值总是固定的, 那么最好使用"默认属性值"; 从语法和性能上都更佳
## [定制构造函数 (Customizing Initialization)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Customizing-Initialization)
---
### [初始化参数 (Initialization Parameters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Initialization-Parameters)

可以给构造函数添加参数:
```swift
struct Exchange {
    var n: Double
    init(fromUS x: Double) {
        n = x * 7.12
    }
    init(fromJP y: Double) {
        n = y * 0.0048
    }
}

let s1 = Exchange(fromUS: 100)
let s2 = Exchange(fromJP: 100)
print(s1.n, s2.n)
```
### [参数名和实参标签 (Parameter Names and Argument Labels)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Parameter-Names-and-Argument-Labels)

🕐 通过参数名和类型来区分多个构造函数:
```swift
struct Point {
    let x, y, z: Double
    init(x: Double, y: Double, z: Double) {
        self.x = x
        self.y = y
        self.z = z
    }
    init(s: Double) {
        x = s
        y = s
        z = s
    }
}
```

🕑 调用时必须指明实参标签:
```swift
let a = Point(x: 1.0, y: 2.1, z: 3.2)
let b = Point(s: 1.8)
```
如果没有设置实参标签, 则会自动将参数名设置为实参标签
### [忽略实参标签 (Initializer Parameters Without Argument Labels)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Initializer-Parameters-Without-Argument-Labels)

使用 `_` 忽略实参标签:
```swift
struct Db {
    var rows: Int
    init(_ num: Int) {
        rows = num
    }
}

var db = Db(10)
```
### [可选值类型 (Optional Property Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Optional-Property-Types)

可选值类型在初始化时会自动赋值为 `nil`
### [初始化时访问常量值 (Assigning Constant Properties During Initialization)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Assigning-Constant-Properties-During-Initialization)

常量一旦赋值后就不能再修改
## [默认构造函数 (Default Initializers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Default-Initializers)
---
`struct` 或 `class` 会自动提供构造函数来完成属性值赋值的过程 (当没有自定义构造函数时)
### [结构体的成员式构造函数 (Memberwise Initializers for Structure Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Memberwise-Initializers-for-Structure-Types)
🕐 没有其他初构造函数时, 结构体会自动为每个属性提供构造函数:
```swift
struct Point {
    var x = 0.0, y = 0.0
}
```

🕑 调用其构造函数:
```swift
let point1 = Point(y: 20.0)
let point2 = Point(x: 10.0)
let point3 = Point(x: 3.0, y: 4.0)
```
## [值类型的初始化委派 (Initializer Delegation for Value Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Initializer-Delegation-for-Value-Types)
---
🕐 构造函数中可以调用其他构造函数, 使用 `self.init()`

🕑 如果自定义了构造函数, 则默认构造函数或成员式构造函数将不可用
### 示例

🕐 定义一个包含 3 个构造函数的值类型:
```swift
struct Point {
    var x = 0.0
    var y = 0.0
    var z = 0.0
    init() {}
    init(x: Double, y: Double, z: Double) {
        self.x = x
        self.y = y
        self.z = z
    }
    init(x: Double, y: Double) {
        let newX = x * 10
        let newY = y * 5
        let newZ = (newX * newY) / 2
        self.init(x: newX, y: newY, z: newZ)
    }
}
```

🕐 调用其无参构造函数 (行为同默认构造函数):
```swift
var p1 = Point()
```

🕑 调用其有参构造函数 (行为同成员式构造函数):
```swift
var p2 = Point(x: 1.2, y: 1.6, z: 2.8)
```

🕒 调用具有初始化委派行为的构造函数:
```swift
var p3 = Point(x: 3.2, y: 2.1)
```
## [类的继承和构造 (Class Inheritance and Initialization)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Class-Inheritance-and-Initialization)
---
要确保本身定义的值和继承来的值在构造后都具有初始值
### [设计构造函数和便利构造函数 (Designated Initializers and Convenience Initializers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Designated-Initializers-and-Convenience-Initializers)

- 设计构造函数: 确保所有属性被构造化 (必须要有一个)
- 便利构造函数: 调用设计构造函数, 对构造过程进行简化, (按情况添加)
### [设计构造函数和便利构造函数的语法 (Syntax for Designated and Convenience Initializers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Syntax-for-Designated-and-Convenience-Initializers)

🕐 设计构造函数:
```swift
init(<#parameters#>) {
   <#statements#>
}
```

🕑 便利构造函数:
```swift
convenience init(<#parameters#>) {
   <#statements#>
}
```
### [类的构造委托 (Initializer Delegation for Class Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Initializer-Delegation-for-Class-Types)

🕐 设计构造函数和便利构造函数符合以下 3 条规则:
- 设计构造函数必须从其直接父类中调用一个设计构造函数
- 便利构造函数只能调用当前类中其他的构造函数
- 便利构造函数最终一定会调用一个设计构造函数

🕑 如下图所示:
![[Pasted image 20240122133125.png|400]]

🕒 更复杂的形式:
![[Pasted image 20240125110357.png|400]]
### [构造的两个阶段 (Two-Phase Initialization)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Two-Phase-Initialization)

🕐 构造分为两个阶段:
1. 给所有存储属性值赋值
2. 对实例中的属性进行修改 (定制操作)

🕑 为了确保构造的安全, 编译器会进行以下 4 个检查:
- 在调用父类的设计构造函数前, 必须确保通过自身的设计构造函数将为所有属性设定初始化值
- 在给继承属性赋值之前必须先调用父类的设计构造函数, 否则会被父类的设计构造函数覆盖掉
- 便利构造函数在给任何属性赋值前必须先调用其他构造函数, 否则会被自身的设计构造函数覆盖
- 只有构造的第一阶段结束后, 才能调用实例中的方法, 访问实例中的属性值等

🕒 这是一个构造第一阶段的调用链图示, 确保所有属性值都有初始值:
![[Pasted image 20240125140333.png|400]]

随后第二阶段的定制操作开始执行:
![[Pasted image 20240125140508.png|400]]
### [构造函数的继承与重写 (Initializer Inheritance and Overriding)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Initializer-Inheritance-and-Overriding)

- 默认子类不会继承超类的构造函数, 因为超类的构造函数不一定能够满足子类的要求
- 如果子类的设计构造函数与超类的设计构造函数相同, 要加上 `override`
- 如果子类的构造函数与父类的便利构造函数相同, 不需要加 `override`, 因为按照之前的规则, 子类是无法直接调用父类的便利构造函数
#### 示例

🕐 定义一个基类并调用:
```swift
class Pet {
    var age = 0
    var say: String {
        return "I'm \(age) years old."
    }
}

var p = Pet()
print(p.say) // I'm 0 years old.
```
这里自动提供了设计构造函数

🕑 创建一个子类并重写基类的设计构造函数:
```swift
class Cat: Pet {
    override init() {
        super.init()
        age = 2
    }
}

var c = Cat()
print(c.say) // I'm 2 years old.
```
因为重写了基类的设计构造函数, 因而需要 `override`

🕒 创建一个子类隐式调用基类的设计构造函数:
```swift
class Dog: Pet {
    var name: String
    init(name: String) {
        self.name = name
        // super.init() 隐式调用
    }
    override var say: String {
        return "\(super.say) And call me \(name)"
    }
}

var d = Dog(name: "Chichi")
print(d.say) // I'm 0 years old. And call me Chichi
```
因为子类没有进行定制操作, 所以基类的设计构造函数会被隐式调用
### [构造函数的自动继承 (Automatic Initializer Inheritance)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Automatic-Initializer-Inheritance)

如果子类中新增的属性都提供了默认值, 则:
- 子类没有提供设计构造函数, 则超类的设计构造函数会被自动继承
- 子类实现或继承了其超类的所有的设计构造函数, 则自动继承超类的所有便利构造函数
### [设计构造函数和便利构造函数的应用 (Designated and Convenience Initializers in Action)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Designated-and-Convenience-Initializers-in-Action)

🕐 基类:
```swift
class Food {
    var name: String
    init(name: String) {
        self.name = name
    }
    convenience init() {
        self.init(name: "[Unnamed]")
    }
}
```

![[Pasted image 20240122171918.png|400]]

🕑 创建 `Food` 的子类, 重写 `init` 为便利构造函数:
```swift
class RecipeIngredient: Food {
    var quantity: Int
    init(name: String, quantity: Int) {
        self.quantity = quantity
        super.init(name: name)
    }
    override convenience init(name: String) {
        self.init(name: name, quantity: 1)
    }
}
```

![[Pasted image 20240122172017.png|400]]

🕒 创建 `RecipeIngredient` 的子类:
```swift
class ShoppingListItem: RecipeIngredient {
    var purchased = false
    var description: String {
        var output = "\(quantity) x \(name)"
        output += purchased ? " ✔" : " ✘"
        return output
    }
}
```
因为其所有属性都具有默认值, 并且没有自定义任何构造函数, 因而自动继承超类的构造函数

![[Pasted image 20240122172224.png|400]]
## [可失败的构造函数 (Failable Initializers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Failable-Initializers)

🕐 使用 `?` 标记该构造函数可能会失败, 此时将返回该实例类型的可选值:
```swift
struct Pet {
    let name: String
    init?(name: String) {
        if name.isEmpty { return nil }
        self.name = name
    }
}
```
使用 `retrun nil` 表示构造失败

🕑 调用并解包可选值:
```swift
let c = Pet(name: "mimi")

if let cat = c {
    print(cat.name)
}
```

🕒 可选值为空可直接判断:
```swift
let d = Pet(name: "")

if d == nil {
    print("error")
}
```
### [枚举类的可失败构造函数 (Failable Initializers for Enumerations)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Failable-Initializers-for-Enumerations)

🕐 基础示例:
```swift
enum Pet {
    case cat, dog, rabbit
    init?(type: Character) {
        switch type {
        case "c":
            self = .cat
        case "d":
            self = .dog
        case "r":
            self = .rabbit
        default:
            return nil
        }
    }
}
```

🕑 调用示例:
```swift
let p = Pet(type: "c")
if p != nil {
    print("cat")
}
```
### [带原始值的枚举类的可失败构造函数 (Failable Initializers for Enumerations with Raw Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Failable-Initializers-for-Enumerations-with-Raw-Values)

带有原始值的枚举类会自动接受 `init?(rawValue: )`

🕐 采用这种方式对上面的枚举类重写:
```swift
enum Pet: Character {
    case cat = "c", dog = "d", rabbit = "r"
}
```

🕑 调用示例:
```swift
let p = Pet(rawValue: "c")
if p != nil {
    print("cat")
}
```
### [初始化失败的传播 (Propagation of Initialization Failure)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Propagation-of-Initialization-Failure)

简单的说就是通过继承链或调用链进行传播

🕐 创建一个基类:
```swift
class Pet {
    let name: String
    init?(name: String) {
        if name.isEmpty {return nil}
        self.name = name
    }
}
```

🕑 一个子类调用基类的可失败构造函数:
```swift
class Cat: Pet {
    let age: Int
    init?(name: String, age: Int) {
        if age < 2 { return nil }
        self.age = age
        super.init(name: name)
    }
}
```
因为子类的构造函数是可失败的, 其才能够调用基类的可失败构造函数, 并且不需要加 `?`

🕒 调用示例:
```swift
if let c = Cat(name: "mimi", age: 10) {
    print(c.name, c.age)
}
```
### [重写可失败的构造函数 (Overriding a Failable Initializer)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Overriding-a-Failable-Initializer)

子类可以重写父类的可失败构造函数为普通构造函数, 反之不行

🕐 简单示例, 创建一个基类:
```swift
class Pet {
    var name: String?
    init() {}
    init?(name: String) {
        if name.isEmpty { return nil }
        self.name = name
    }
}
```

🕑 创建一个子类重写基类的构造函数:
```swift
class Cat: Pet {
    override init() {
        super.init()
        self.name = "[Unknown]"
    }
    override init(name: String) {
        super.init()
        if name.isEmpty {
            self.name = "[Unknown]"
        } else {
            self.name = name
        }
    }
}
```

🕒 创建一个子类重写基类的构造函数, 并调用基类的可失败构造函数:
```swift
class Dog: Pet {
    override init() {
        super.init(name: "[Unknown]")!
    }
}
```
此时要加上 `!`, 这表示你认为这样已经绝对安全了
### [隐式解包的可失败构造函数 (The init! Failable Initializer)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#The-init-Failable-Initializer)

也就是 `init!()`
## [必要的构造函数 (Required Initializers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Required-Initializers)

🕐 在构造函数前使用 `required` 关键字标明子类都必须要实现该构造函数:
```swift
class SomeClass {
    required init() {
        // initializer implementation goes here
    }
}
```

🕑 在子类中实现该构造函数也必须加上 `required`, 此时不必使用 `override`
```swift
class SomeSubclass: SomeClass {
    required init() {
        // subclass implementation of the required initializer goes here
    }
}
```
## [使用闭包或函数设置一个默认值 (Setting a Default Property Value with a Closure or Function)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/initialization/#Setting-a-Default-Property-Value-with-a-Closure-or-Function)

🕐 基本结构:
```swift
class SomeClass {
    let someProperty: SomeType = {
        return someValue
    }()
}
```

🕑 闭包是在构造的过程中执行的, 这意味着此时其他属性不一定都构造完成了, 因而不能在其中调用其它属性或使用 `self`


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->