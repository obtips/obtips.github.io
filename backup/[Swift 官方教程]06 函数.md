[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

建议: 重点在隐式返回及其后面的部分
## [定义和调用 (Defining and Calling Functions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Defining-and-Calling-Functions)
---
```swift
func greet(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}

print(greet(person: "root"))
```
## [参数和返回值 (Function Parameters and Return Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Parameters-and-Return-Values)
---
### [无参 (Functions Without Parameters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Functions-Without-Parameters)

```swift
func greet() -> String {
    return "hello, world"
}

print(greet())
```
### [多参 (Functions With Multiple Parameters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Functions-With-Multiple-Parameters)

```swift
func greet(person: String, account: Int) -> String {
    return "Hello \(person), your account is \(account)."
}

print(greet(person: "Tim", account: 12330))
```
### [无返回值 (Functions Without Return Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Functions-Without-Return-Values)

```swift
func greet(person: String) {
    print("Hello, \(person)!")
}

greet(person: "Dave")
```

实际上返回了一个类型为 `Void` 的值, 是一个空 Tuple, 即 `()`
### [多返回值 (Functions with Multiple Return Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Functions-with-Multiple-Return-Values)

比如求最大最小值:
```swift
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for v in array[1..<array.count] {
        if v < currentMin {
            currentMin = v
        } else if v > currentMax {
            currentMax = v
        }
    }
    return (currentMin, currentMax)
}

let result = minMax(array: [7, 13, 28, 14, 5])
print(result.min, result.max)
```
#### [可选元组返回类型 (Optional Tuple Return Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Optional-Tuple-Return-Types)

```swift
func minMax(array: [Int]) -> (min: Int, max: Int)? {
    if array.isEmpty { return nil}
    
    var currentMin = array[0]
    var currentMax = array[0]
    for v in array[1..<array.count] {
        if v < currentMin {
            currentMin = v
        } else if v > currentMax {
            currentMax = v
        }
    }
    return (currentMin, currentMax)
}

if let result = minMax(array: [7, 13, 28, 14, 5]) {
    print(result.min, result.max)
}
```
### [隐式返回 (Functions With an Implicit Return)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Functions-With-an-Implicit-Return)

函数仅由一个返回表达式构成, 那么可以省略 `return`:
```swift
func greet(for person: String) -> String {
    "Hello, " + person + "!"
}

print(greet(for: "Dave"))
```
## [形参标签和实参名称 (Function Argument Labels and Parameter Names)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Argument-Labels-and-Parameter-Names)
---
默认使用形参标签作为实参名称
```swift
func greet(person: String, from hometown: String) -> String {
    return "Hello \(person)!  Glad you could visit from \(hometown)."
}

print(greet(person: "Bill", from: "Cupertino"))
```
### [可忽略的形参标签 (Omitting Argument Labels)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Omitting-Argument-Labels)

```swift
func greet(_ person: String, from hometown: String) -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)"
}

print(greet("Bill", from: "Cupertino"))
```
### [默认参数值 (Default Parameter Values)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Default-Parameter-Values)

```swift
func greet(person: String, from hometown: String = "New York") -> String {
    return "Hello \(person)! Glad you could visit from \(hometown)"
}

print(greet(person: "Bill"))
```
### [可变参数 (Variadic Parameters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Variadic-Parameters)

```swift
func arithmeticMean(_ numbers: Double...) -> Double {
    var total: Double = 0
    for i in numbers {
        total += i
    }
    return total / Double(numbers.count)
}

print(arithmeticMean(3, 8.25, 18.75))
```
### [引用参数 (In-Out Parameters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#In-Out-Parameters)

参数默认为常量值传递, 将其设置为 `inout` 就可以引用传递:
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}

var a = 3
var b = 107
swapTwoInts(&a, &b)

print(a,b)
```
此时参数传递要加上上 `&`

> inout 参数没有默认值, 可变参数不能为 inout
## [函数类型 (Function Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Types)
---
🕐 函数可作为一种类型:
```swift
func addTwoInts(_ a: Int, _ b: Int) -> Int {
    return a + b
}
```
由入参类型和出参类型组成. 例如该函数的类型为 `(Int, Int) -> Int`

🕑 该函数的类型为 `() -> Void`:
```swift
func printHelloWorld() {
    print("hello, world")
}
```
### [使用函数类型 (Using Function Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Using-Function-Types)

```swift
var myFunc: (Int, Int) -> Int = addTwoInts
print(myFunc(1, 2))
```
### [函数类型作为参数类型 (Function Types as Parameter Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Types-as-Parameter-Types)

```swift
func printResult(_ mathFunction: (Int, Int) -> Int, _ a: Int, _ b: Int) {
    print("Result: \(mathFunction(a,b))")
}
printResult(addTwoInts, 3, 5)
```
### [参数类型作为返回类型 (Function Types as Return Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Types-as-Return-Types)

定义两个函数:
```swift
func add(_ input: Int) -> Int {
    return input + 100
}

func sub(_ input: Int) -> Int {
    return input - 100
}
```

使用该函数类型:
```swift
func chooseFunction(_ num: Int) -> (Int) -> Int {
    if num < 100 {
        return add
    } else {
        return sub
    }
}

let num = 999
let myFunc = chooseFunction(num)
print(myFunc(num))
```
## [嵌套函数 (Nested Functions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Nested-Functions)
---
函数中嵌套函数:
```swift
func chooseFunction(_ num: Int) -> (Int) -> Int {
    func add(_ input: Int) -> Int {
        return input + 100
    }
    
    func sub(_ input: Int) -> Int {
        return input - 100
    }
    
    if num < 100 {
        return add
    } else {
        return sub
    }
}

let num = 999
let myFunc = chooseFunction(num)
print(myFunc(num))
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->