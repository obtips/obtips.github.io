[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

在实例被回收前调用
## [析构函数如何工作 (How Deinitialization Works)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/deinitialization#How-Deinitialization-Works)

Swift 利用"自动引用计数 (Automatic reference counting)" 自动回收不再使用的实例

手动执行一些清理:
```swift
deinit{
	   
}
```
最多只能有一个

超类的解初始化和被自动继承, 如果子类有实现会自动在实现的最后被调用
## [解初始化实际使用 (Deinitializers in Action)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/deinitialization#Deinitializers-in-Action)

银行取钱和存钱:
```swift
class Bank {
    static var coinsInBank = 10_000
    static func distribute(coins numberOfCoinsRequested: Int) -> Int {
        let numberOfCoinsToVend = min(numberOfCoinsRequested, coinsInBank)
        coinsInBank -= numberOfCoinsToVend
        return numberOfCoinsToVend
    }
    static func receive(coins: Int) {
        coinsInBank += coins
    }
}
```

赌徒取钱和赢钱:
```swift
class Player {
    var coinsInPurse: Int
    init(coins: Int) {
        coinsInPurse = Bank.distribute(coins: coins)
    }
    func win(coins: Int) {
        coinsInPurse += Bank.distribute(coins: coins)
    }
    deinit {
        Bank.receive(coins: coinsInPurse)
    }
}
```
最后将钱返回给银行

测试1:
```swift
var playerOne: Player? = Player(coins: 100)
print("A new player has joined the game with \(playerOne!.coinsInPurse) coins")

print("There are now \(Bank.coinsInBank) coins left in the bank")
```

测试2:
```swift
playerOne!.win(coins: 2_000)
print("PlayerOne won 2000 coins & now has \(playerOne!.coinsInPurse) coins")
print("The bank now only has \(Bank.coinsInBank) coins left")
```

测试3:
```swift
playerOne = nil
print("PlayerOne has left the game")
print("The bank now has \(Bank.coinsInBank) coins")
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->