[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

## [表示和抛出错误 (Representing and Throwing Errors)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling#Representing-and-Throwing-Errors)

使用符合 `Error` 协议的类型值来表示错误, 而枚举很适合:
```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}
```

抛出错误:
```swift
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```
## [处理错误 (Handling Errors)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling#Handling-Errors)
### [传播错误 (Propagating Errors Using Throwing Functions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling/#Propagating-Errors-Using-Throwing-Functions)

使用 `throw` 标记一个可抛出错误的函数, 方法或初始化器:
```swift
func canThrowErrors() throws -> String
```
如果没有该标记, 则必须在函数内部处理该错误.

函数` vend` 会传播错误:
```swift
struct Item {
    var price: Int
    var count: Int
}

class VendingMachine {
    var inventory = [
        "Candy Bar": Item(price: 12, count: 7),
        "Chips": Item(price: 10, count: 4),
        "Pretzels": Item(price: 7, count: 11)
    ]
    var coinsDeposited = 0

    func vend(itemNamed name: String) throws {
        guard let item = inventory[name] else {
            throw VendingMachineError.invalidSelection
        }

        guard item.count > 0 else {
            throw VendingMachineError.outOfStock
        }

        guard item.price <= coinsDeposited else {
            throw VendingMachineError.insufficientFunds(coinsNeeded: item.price - coinsDeposited)
        }

        coinsDeposited -= item.price

        var newItem = item
        newItem.count -= 1
        inventory[name] = newItem

        print("Dispensing \(name)")
    }
}
```

调用 `vend` 的函数:
```swift
let favoriteSnacks = [
    "Alice": "Chips",
    "Bob": "Licorice",
    "Eve": "Pretzels",
]
func buyFavoriteSnack(person: String, vendingMachine: VendingMachine) throws {
    let snackName = favoriteSnacks[person] ?? "Candy Bar"
    try vendingMachine.vend(itemNamed: snackName)
}
```
需要使用 `try` 关键字

结构体中传播错误:
```swift
struct PurchasedSnack {
    let name: String
    init(name: String, vendingMachine: VendingMachine) throws {
        try vendingMachine.vend(itemNamed: name)
        self.name = name
    }
}
```
### [使用 Do-Catch (Handling Errors Using Do-Catch)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling/#Handling-Errors-Using-Do-Catch)

```swift
var vendingMachine = VendingMachine()
vendingMachine.coinsDeposited = 8
do {
    try buyFavoriteSnack(person: "Alice", vendingMachine: vendingMachine)
    print("Success! Yum.")
} catch VendingMachineError.invalidSelection {
    print("Invalid Selection.")
} catch VendingMachineError.outOfStock {
    print("Out of Stock.")
} catch VendingMachineError.insufficientFunds(let coinsNeeded) {
    print("Insufficient funds. Please insert an additional \(coinsNeeded) coins.")
} catch {
    print("Unexpected error: \(error).")
}
```
最后的 `catch` 用于处理意外情况

`catch` 中匹配多个错误:
```swift
func eat(item: String) throws {
    do {
        try vendingMachine.vend(itemNamed: item)
    } catch VendingMachineError.invalidSelection, VendingMachineError.insufficientFunds, VendingMachineError.outOfStock {
        print("Invalid selection, out of stock, or not enough money.")
    }
}
```
### [转换错误为可选值 (Converting Errors to Optional Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling/#Converting-Errors-to-Optional-Values)

使用 `try?` 表达式, 如果发生错误则计算结果为 `nil`:
```swift
func someThrowingFunction() throws -> Int {
    // ...
}

let x = try? someThrowingFunction()
```
等同于:
```swift
let y: Int?
do {
    y = try someThrowingFunction()
} catch {
    y = nil
}
```

用于条件表达式:
```swift
func fetchData() -> Data? {
    if let data = try? fetchDataFromDisk() { return data }
    if let data = try? fetchDataFromServer() { return data }
    return nil
}
```
### [禁止错误传播 (Disabling Error Propagation)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling/#Disabling-Error-Propagation)

使用 `try!` 来表示不会发生错误:
```swift
let photo = try! loadImage(atPath: "./Resources/John Appleseed.jpg")
```
如果发生错误将会直接报错, 错误也不会被传播出去
## [指定清除动作 (Specifying Cleanup Actions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/errorhandling/#Specifying-Cleanup-Actions)

使用 `defer` 将必要的清除动作包含在其中, 无论代码块是否正常退出都会执行





<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->