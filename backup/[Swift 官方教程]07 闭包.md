[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

类似 lambda 表达式.

建议: 跟着例子从上往下一步步跟着理解, 最后2小节难一点
## [闭包表达式 (Closure Expressions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Closure-Expressions)
---
### [sorted 方法 (The Sorted Method)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#The-Sorted-Method)

根据方法对元素进行排序:
```swift
func backward(_ s1: String, _ s2: String) -> Bool {
    return s1 > s2
}

let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
var reversedNames = names.sorted(by: backward)
print(reversedNames)
```
### [闭包表达式语法 (Closure Expression Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Closure-Expression-Syntax)

🕐 上述可以被改写为:
```swift
var reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 > s2
})

print(reversedNames)
```
即将匿名函数放在 `{}` 内,  `in` 后接函数体 

🕑 因为函数体就一个表达式, 可以被写在一行:
```swift
var reversedNames =  names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )

print(reversedNames)
```
### [从上下文中推断类型 (Inferring Type From Context)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Inferring-Type-From-Context)

因为可以从上下文中推断类型, 上述可以被改写为:
```swift
var reversedNames =  names.sorted(by: { s1, s2 in return s1 > s2 } )

print(reversedNames)
```
### [单行表达式的隐式返回 (Implicit Returns from Single-Expression Closures)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Implicit-Returns-from-Single-Expression-Closures)

单行表达式可省略 return:
```swift
var reversedNames =  names.sorted(by: { s1, s2 in s1 > s2 } )

print(reversedNames)
```
### [参数名简记法 (Shorthand Argument Names)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Shorthand-Argument-Names)

使用 **$x** 来快速获取参数:
```swift
var reversedNames =  names.sorted(by: { $0 > $1 } )

print(reversedNames)
```
 x 的最大值+1表示该闭包所接受的参数数量
### [运算符方法 (Operator Methods)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Operator-Methods)

因为 String 实现了比较操作符方法, 即接受两个 String 参数并返回布尔值, 这刚好符合要求:
```swift
var reversedNames =  names.sorted(by: > )

print(reversedNames)
```
## [尾闭包 (Trailing Closures)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Trailing-Closures)
---
调用闭包类型参数时, 可以将闭包写在后面:
```swift
func someFunc(closure: () -> Void) {
    // function body goes here
}
```

🕐 常规调用:
```swift
someFunc(closure: {
    // closure's body goes here
})
```

🕑 尾调用:
```swift
someFunc() {
    // trailing closure's body goes here
}
```
### 示例 1

🕐 例如上面的例子可改写为:
```swift
var reversedNames =  names.sorted() { $0 > $1 }

print(reversedNames)
```

🕑 如果闭包是唯一参数, 括号可以省略:
```swift
var reversedNames =  names.sorted { $0 > $1 }

print(reversedNames)
```
### 示例 2

下面以数组的 `map` 方法为例子:
```swift
let d = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let a = [16, 58, 510]

let s = a.map { (n) -> String in
    var n = n
    var output = ""
    repeat {
        output = d[n % 10]! + output
        n /= 10
    } while n > 0
    return output
}
```
### 示例 3

当有多个闭包参数时, 通过尾闭包传递第一个参数时名称可以省略, 后面的要标出:
```swift
func loadFile(from server: String, upload: (String) -> Void, onFailure: () -> Void) {
    print("Downloaded file from \(server)")
    if server.count <= 10 {
        upload("Uploaded \(server.count) bytes.")
    } else {
        onFailure()
    }
}
```
调用:
```swift
loadFile(from: "Youtube") { file in
    print(file)
} onFailure: {
    print("Couldn't upload the file.")
}
```
## [值获取 (Capturing Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Capturing-Values)

闭包可以从上下文环境中获取值:
```swift
func getIncrease(step: Int) -> () -> Int {
    var total = 0
    func increaser() -> Int {
        total += step
        return total
    }
    return increaser
}
```
每调用一次 `f()` 返回的值都会增加:
```swift
let f = getIncrease(step: 10)
print(f())
print(f())
```
即闭包外的量与闭包绑定了
## [闭包为引用类型 (Closures Are Reference Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Closures-Are-Reference-Types)

即值传递类型为指针传递
## [闭包逃逸 (Escaping Closures)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/#Escaping-Closures)
---
指的是被作为参数传递的闭包, 在函数返回后还可以被调用.

🕐 常见的方式是将其存储到外部变量中:
```swift
var outer: [() -> Void] = []

func toOuter(c: @escaping () -> Void) {
    outer.append(c)
}
```
使用 `@escaping` 定义一个可逃逸的闭包

🕑 定义一个具有非逃逸的闭包的函数:
```swift
func noOuter(c: () -> Void) {
    c()
}
```

🕒 定义一个类调用这两个函数:
```swift
class SomeClass {
    var x = 10
    func doThing() {
        toOuter { self.x = 99 } // 等价为 { [self] in x = 99 }
        noOuter { x = 200 }
    }
}
```
对于可逃逸闭包, 需要显示指明要捕获 self, 或者将其添加到闭包的捕获列表中, 即上面的 `[self]`

🕓 调用该类的方法:
```swift
let myClass = SomeClass()

myClass.doThing()
print(myClass.x) // 200
```

🕔 调用该类的逃逸闭包:
```swift
outer.first?()
print(myClass.x) // 99
```

🕑 对于值类型则情况不同:
```swift
struct SomeStruct {
    var x = 10
    mutating func doSomething() {
        noOuter { x = 200 }  // Ok
        toOuter { x = 100 }     // Error
    }
}
```
值类型的 self 是隐式传递的, 但是逃逸闭包不能捕获值类型的 self, 因而这里将报错. 

> 值类型不允许共享可变性, 也就是多个代码部分对同一数据的读写权限. 值类型被传递时将会创建一个独立的副本, 那么你修改了一个其中一个副本并不会影响到另一个副本; 因而, 假设值类型可以逃逸, 那么在逃逸闭包中对其修改后是新创建一个副本还是修改原有副本? (值类型的定义已结束)
## [自动闭包 (Autoclosures)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures#Autoclosures)
---
自动闭包用于封装一个表达式, 其返回值为表达式的执行结果

🕐 延迟执行:
```swift
var a = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
let c = { a.remove(at: 0) }

print(a.count) // 5
print("Remove \(c())")
print(a.count) // 4
```
自动闭包中的表达式只有被调用的时候才会执行

🕑 作为参数时的延迟执行:
```swift
func test(c: () -> String) {
    print("Remove \(c())")
}

test(c: { a.remove(at: 0) })
print(a.count) // 3
```

🕒 可以在闭包参数前使用 `@autoclosure`, 从而在传参时省略 {}:
```swift
func test(c: @autoclosure () -> String) {
    print("Remove \(c())")
}
test(c: a.remove(at: 0))
```

🕒 可以和 `@escaping` 一起使用:
```swift
var outer: [() -> String] = []

func collect(_ c: @autoclosure @escaping () -> String) {
    outer.append(c)
}
```
传递自动闭包:
```swift
collect(a.remove(at: 0))
collect(a.remove(at: 0))
print("Collected \(outer.count) closures.")
```
调用闭包:
```swift
for c in outer {
    print("Now serving \(c())")
}
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->