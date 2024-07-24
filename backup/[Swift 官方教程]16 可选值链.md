[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

无需解包即可访问可选值的成员
## [可选值链作为强制解包的一种方式 (Optional Chaining as an Alternative to Forced Unwrapping)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Optional-Chaining-as-an-Alternative-to-Forced-Unwrapping)

定义两个基类:
```swift
class Person {
    var residence: Residence?
}

class Residence {
    var numberOfRooms = 1
}
```

强制链式解包:
```swift
let john = Person()
let roomCount = john.residence!.numberOfRooms // 错误
```

可选链式解包:
```swift
john.residence = Residence()
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
```
## [为可选值链定义一个模型类 (Defining Model Classes for Optional Chaining)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Defining-Model-Classes-for-Optional-Chaining)

居民:
```swift
class Person {
    var residence: Residence?
}
```

居住登记:
```swift
class Residence {
    var rooms: [Room] = []
    var numberOfRooms: Int {
        return rooms.count
    }
    subscript(i: Int) -> Room {
        get {
            return rooms[i]
        }
        set {
            rooms[i] = newValue
        }
    }
    func printNumberOfRooms() {
        print("The number of rooms is \(numberOfRooms)")
    }
    var address: Address?
}
```

房间:
```swift
class Room {
    let name: String
    init(name: String) { self.name = name }
}
```

地址:
```swift
class Address {
    var buildingName: String?
    var buildingNumber: String?
    var street: String?
    func buildingIdentifier() -> String? {
        if let buildingNumber = buildingNumber, let street = street {
            return "\(buildingNumber) \(street)"
        } else if buildingName != nil {
            return buildingName
        } else {
            return nil
        }
    }
}
```
## [通过可选值链访问属性 (Accessing Properties Through Optional Chaining)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Accessing-Properties-Through-Optional-Chaining)

访问居民的属性:
```swift
let john = Person()
if let roomCount = john.residence?.numberOfRooms {
    print("John's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
```

通过可选值链为属性赋值:
```swift
let someAddress = Address()
someAddress.buildingNumber = "29"
someAddress.street = "Acacia Road"
john.residence?.address = someAddress
```
因为 `address` 为 `nil`, 最后的赋值语句并不会执行计算
## [使用可选链来调用方法 (Calling Methods Through Optional Chaining)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Calling-Methods-Through-Optional-Chaining)

通过可选链来调用方法:
```swift
if john.residence?.printNumberOfRooms() != nil {
    print("It was possible to print the number of rooms.")
} else {
    print("It was not possible to print the number of rooms.")
}
```
此时函数的返回值不是 `Void` 而是 `Void?`

通过可选链赋值的整个表达式可以用于判断:
```swift
if (john.residence?.address = someAddress) != nil {
    print("It was possible to set the address.")
} else {
    print("It was not possible to set the address.")
}
```
## [通过可选链访问下标 (Accessing Subscripts Through Optional Chaining)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Accessing-Subscripts-Through-Optional-Chaining)

因为 `residence?[0]` 为 `nil`, 下面的操作都会失败:
```swift
if let firstRoomName = john.residence?[0].name {
    print("The first room name is \(firstRoomName).")
} else {
    print("Unable to retrieve the first room name.")
}
```

```swift
john.residence?[0] = Room(name: "Bathroom")
```

为 `residence` 赋值并访问下标:
```swift

let johnsHouse = Residence()
johnsHouse.rooms.append(Room(name: "Living Room"))
johnsHouse.rooms.append(Room(name: "Kitchen"))
john.residence = johnsHouse

if let firstRoomName = john.residence?[0].name {
    print("The first room name is \(firstRoomName).")
} else {
    print("Unable to retrieve the first room name.")
}
```
### [访问可选类型的下标 (Accessing Subscripts of Optional Type)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Accessing-Subscripts-of-Optional-Type)

如果下标访问返回的是可选类型, 那么可以通过可选链访问它:
```swift
var testScores = ["Dave": [86, 82, 84], "Bev": [79, 94, 81]]
testScores["Dave"]?[0] = 91
testScores["Bev"]?[0] += 1
testScores["Brian"]?[0] = 72
```
字典的 key 下标返回的就是可选类型
## [连接多个层级的链 (Linking Multiple Levels of Chaining_](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Linking-Multiple-Levels-of-Chaining)

```swift
if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
```

```swift
let johnsAddress = Address()
johnsAddress.buildingName = "The Larches"
johnsAddress.street = "Laurel Street"
john.residence?.address = johnsAddress


if let johnsStreet = john.residence?.address?.street {
    print("John's street name is \(johnsStreet).")
} else {
    print("Unable to retrieve the address.")
}
```
## [链接具有可选类型返回值的方法 (Chaining on Methods with Optional Return Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/optionalchaining#Chaining-on-Methods-with-Optional-Return-Values)

通过可选链调用返回值是可选类型的方法:
```swift
if let buildingIdentifier = john.residence?.address?.buildingIdentifier() {
    print("John's building identifier is \(buildingIdentifier).")
}
```

更深一层的调用:
```swift
if let beginsWithThe =
    john.residence?.address?.buildingIdentifier()?.hasPrefix("The") {
    if beginsWithThe {
        print("John's building identifier begins with \"The\".")
    } else {
        print("John's building identifier doesn't begin with \"The\".")
    }
}
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->