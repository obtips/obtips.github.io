[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

建议: 重点在 Switch 及后面的部分
## [For-In 循环 (For-In Loops)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#For-In-Loops)
---
🕐 数组:
```swift
let a = [1, 2, 3, 4, 5, 6]
for i in a {
    print(i)
}
```

🕑 字典:
```swift
let d = ["a": 18, "b": 20, "c": 38]
for (k, v) in d {
    print(k, v)
}
```

🕒 区间运算:
```swift
for i in 1...5 {
    print(i)
}

for i in 1..<5 {
    print(i)
}
```

🕓 等差列:
```swift
for i in stride(from: 0, to: 20, by: 2) { //不含 20
    print(i)
}

for i in stride(from: 0, through: 20, by: 2) { // 含 20
    print(i)
}
```
## [While 循环 (While Loops)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#While-Loops)
---
有两种:
- `while`: 先判断再循环
- `repeat-while`: 先循环再判断

```swift
var a = 0
let b = 10
```
### [While](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#While)
```swift
while a < b {
    print(a)
    a += 1
}
```
### [Repeat-While](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Repeat-While)
```swift
repeat {
    print(a)
    a += 1
} while a < b
```
## [条件语句 (Conditional Statements)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Conditional-Statements)
---
### [If](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#If)
```swift
let n = 95

if n < 80 {
    print("c")
} else if n < 90 {
    print("b")
} else {
    print("a")
}
```

🕐 用于赋值语句:
```swift
let n = 70

let a: String? = if n < 80 {
    "root"
} else {
    nil
}
```

另一种等价形式 (因为用到了可选类型, 因而要提供类型信息):
```swift
let a = if n < 80 {
    "root"
} else {
    nil as String?
}
```

🕑 触发错误:
```swift
if ... {
    throw ...
} else {
}
```
### [Switch](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Switch)

🕐 必须要考虑所有 case, 否则要提供 default:
```swift
let ch: Character = "z"

switch ch {
case "a":
    print("case 1")
case "z":
    print("case 2")
default:
    print("default")
}
```

🕑 多 case 组合:
```swift
let ch: Character = "z"

switch ch {
case "a","A":
    print("case 1")
case "z":
    print("case 2")
default:
    print("default")
}
```

🕒 用于赋值:
```swift
let ch: Character = "z"

let s = switch ch {
case "a":
    "case 1"
case "z":
    "case 2"
default:
    "default"
}
```
#### 自动向下匹配 [ (No Implicit Fallthrough)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#No-Implicit-Fallthrough)

只要匹配到 case 就停止继续向下匹配, 因而 `break` 不是必须的, 但还是可以使用
#### [区间匹配 (Interval Matching)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Interval-Matching)

```swift
var num = 18

switch num {
    case 0:
        print("0")
    case 1..<5:
        print("<5")
    case 5..<10:
        print("<10")
    default:
        print("default")
}
```
#### [元组匹配 (Tuples)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Tuples)

```swift
let p = (1, 1)

switch p {
case (0, 0):
    print("a")
case (_, 0):
    print("b")
case (0, _):
    print("c")
case (-2...2, -2...2):
    print("d")
default:
    print("default")
}
```
#### [值绑定 (Value Bindings)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Value-Bindings)

```swift
let p = (2, 0)

switch p {
case (let x, 0):
    print(x)
case (0, let y):
    print(y)
case let (x, y):
    print(x, y)
}
```
#### [Where](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Where)

```swift
let p = (1, -1)

switch p {
case let (x, y) where x == y:
    print("a")
case let (x, y) where x == -y:
    print("b")
case let (x, y):
    print(x,y)
}
```
#### [组合 case (Compound Cases)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Compound-Cases)

🕐 非赋值情况:
```swift
let ch: Character = "e"

switch ch {
case "a", "e", "i", "o", "u":
    print("a")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
    "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("b")
default:
    print("default")
}
```

🕑 赋值情况:
```swift
let p = (9, 0)

switch p {
case (let n, 0), (0, let n):
    print(n)
default:
    print("default")
}
```
## [控制转移语句 (Control Transfer Statements)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Control-Transfer-Statements)
---
转移控制权
### [Continue](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Continue)

```swift
for i in 1...5 {
    if i < 3 {
        continue
    }
    print(i)
}
```
### [Break](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Break)
#### [在循环中使用 (Break in a Loop Statement)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Break-in-a-Loop-Statement)

终止当前循环
#### [在 switch 中使用 break (Break in a Switch Statement)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Break-in-a-Switch-Statement)

常用来忽略某个 case 的执行

```swift
var num = 18

switch num {
    case 0:
        break
    case 1..<5:
        print("<5")
    case 5..<10:
        print("<10")
    default:
        break
}
```
### [自动向下匹配 (Fallthrough)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Fallthrough)

默认一旦 case 匹配就终止执行, 使用 `fallthrough` 自动向下匹配:
```swift
let num = 5

switch num {
case 1, 3, 5:
    print("case a")
    fallthrough
case 99:
    print("case b")
default:
    print("error")
}
```
此时下一个 case 的条件将被忽略
### [带标签的语句 (Labeled Statements)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Labeled-Statements)

比如给循环语句指定标签, 从而精准控制:
```swift
let fruits = ["A", "A", "B", "A", "B", "C", "A"]
var count = 0

aLoop: while true {
    bLoop: for f in fruits {
        switch f {
            case "A":
                count += 1
                print("So far, Found \(count) A ")
                continue bLoop
            case "B":
                print("Found B")
            default:
                break
        }
        if f == "C" {
            print("Got C, work done.")
            break aLoop
        }
    }
}
```
## [提前退出 (Early Exit)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Early-Exit)
---
`guard` 中条件为真时往下执行, 否则执行 `else`, else 中必须做好控制转移:
```swift
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }

    print("Hello \(name)!") // 条件语句中的变量会保留

    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }
	
    print("I hope the weather is nice in \(location).")
}

greet(person: ["name": "John"])
greet(person: ["name": "Jane", "location": "Cupertino"])
```
这里使用 `return` 提前终止函数的执行, 当然也可以用 `throw`
## [推迟行动 (Deferred Actions)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Deferred-Actions)
---
在逻辑块退出之前, 按照逆序执行之前的所有被推迟的行动:
```swift
var score = 1

if score < 10 {
    defer {
        print(score)
    }
    defer {
        print("The score is:")
    }
    score += 5
}
```
实际上 `defer` 语句已经被计算了, 只是行动被推迟了
## [检查 API 可用性 (Checking API Availability)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/#Checking-API-Availability)
---
即检查 API 的版本兼容性. 这里先了解就行, 日后用到再作深入了解

🕐 用于条件语句:
```swift
if #available(iOS 10, macOS 10.12, *) {
    // Use iOS 10 APIs on iOS, and use macOS 10.12 APIs on macOS
} else {
    // Fall back to earlier iOS and macOS APIs
}
```

🕑 用于类型:
```swift
@available(macOS 10.12, *)
struct ColorPreference {
    var bestColor = "blue"
}


func chooseBestColor() -> String {
    guard #available(macOS 10.12, *) else {
       return "gray"
    }
    let colors = ColorPreference()
    return colors.bestColor
}
```

🕒 使用 `unavailable` 判断不可用, 以下两种是等价的 
```swift
if #available(iOS 10, *) {
	...
} else {
    // Fallback code
}
```
等价于:
```swift
if #unavailable(iOS 10) {
    // Fallback code
}
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->