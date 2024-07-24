[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

建议: 这部分没什么难点, 了解下各个类型的操作就行
## [集合的可变性 (Mutability of Collections)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Mutability-of-Collections)
---
是否可变取决于是 `var` 还是 `let`
## [数组 (Arrays)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Arrays)
---
同一类型值的顺序集合
### [数组类型简记法 (Array Type Shorthand Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Array-Type-Shorthand-Syntax)

数组的完整写法为: `Array<Element>`, 但通常简写为: `[Element]`
### [创建空数组 (Creating an Empty Array)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Empty-Array)

```swift
var a: [Int] = []
a.append(3)
a = []
```
### [创建有默认值的数组 (Creating an Array with a Default Value)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Array-with-a-Default-Value)

具有 3 个相同值的数组:
```swift
var a = Array(repeating: 0.0, count: 3)
```
### [合并两个数组 (Creating an Array by Adding Two Arrays Together)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Array-by-Adding-Two-Arrays-Together)

```swift
var a = Array(repeating: 0.0, count: 3)
var b = Array(repeating: 2.5, count: 4)
var c = a + b
```
### [通过数组字面量创建数组 (Creating an Array with an Array Literal)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Array-with-an-Array-Literal)

```swift
var a: [String] = ["Eggs", "Milk"]
```
### [访问和修改数组 (Accessing and Modifying an Array)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Accessing-and-Modifying-an-Array)

```swift
var a = [1, 2, 3, 4, 5]
```

🕐 获取的元素个数:
```swift
a.count
```

🕑 判断数组是否为空:
```swift
a.isEmpty
```

🕒 在"数组"末尾添加元素:
```swift
a.append(6)
```

🕓 通过索引获取和修改数组:
```swift
let e = array[0]
array[0] = "root"
array[4...6] = ["a", "b"]
```

🕔 插入或移除指定位置的元素:
```swift
a.insert(88, at: 0)
a.remove(at: 1)
```

🕕 弹出最后一位元素:
```swift
let p = a.removeLast()
```
### [遍历数组 (Iterating Over an Array)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Iterating-Over-an-Array)

🕐 遍历数组中的元素:
```swift
for v in array {
}
```

🕑 遍历数组的索引和元素:
```swift
for (i, v) in array.enumerated() {
}
```
## [集合 (Sets)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Sets)
---
同一类型的唯一值的无序集合
### [集合的哈希值 (Hash Values for Set Types)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Hash-Values-for-Set-Types)

集合类型必须是可哈希的, 因为要进行值比较
### [集合类型语法 (Set Type Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Set-Type-Syntax)

集合类型写作: `Set<Element>`
### [创建和初始化空集合 (Creating and Initializing an Empty Set)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-and-Initializing-an-Empty-Set)

```swift
var s = Set<Character>()
s.insert("a")
s = []
```
### [通过数组字面量创建集合 (Creating a Set with an Array Literal)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-a-Set-with-an-Array-Literal)

```swift
var s: Set<String> = ["Rock", "Classical", "Hip hop"]
```

可以简写为:
```swift
var s: Set = ["Rock", "Classical", "Hip hop"]
```
### [访问和修改集合 (Accessing and Modifying a Set)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Accessing-and-Modifying-a-Set)

🕐 获取个数:
```swift
s.count

```

🕑 判断否为空:
```swift
s.isEmpty
```

🕒 插入元素:
```swift
s.insert("a")

```

🕓 移除元素:
```swift
s.remove("a")
```
 
 🕓 是否包含某元素:
```
s.contains("a")
```
### [遍历集合 (Iterating Over a Set)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Iterating-Over-a-Set)

🕐 遍历集合元素:
```swift
for i in s {
}
```

🕑 排序后遍历:
```swift
for i in s.sorted() {
}
```
## [执行集合操作 (Performing Set Operations)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Performing-Set-Operations)
---
数学中的集合操作
### [基础集合操作 (Fundamental Set Operations)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Fundamental-Set-Operations)

![[Pasted image 20240107203713.png|550]]
### [集合的成员资格和等价性 (Set Membership and Equality)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Set-Membership-and-Equality)

```swift
let a: Set = ["🐶", "🐱"]
let b: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let c: Set = ["🐦", "🐭"]
```

🕐 判断集合是否相等:
```swift
a == b
```

🕑 集合操作:

```swift
a.isSubset(of: b) // 子集
a.isStrictSubset(of: b) // 严格子集
b.isSuperset(of: a) // 超集
b.isDisjoint(with: c) // 无交集
```
## [字典 (Dictionaries)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Dictionaries)
---
无序的, key 类型相同, value 类型相同
### [字典类型简记法 (Dictionary Type Shorthand Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Dictionary-Type-Shorthand-Syntax)

字典定义为: `Dictionary<Key, Value>`, 可以简写为: `[Key: Value]`
### [创建空字典 (Creating an Empty Dictionary)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-an-Empty-Dictionary)

```swift
var d: [Int: String] = [:]
```

🕐 赋值:
```swift
d[16] = "sixteen"
```
### [通过字典字面量创建字典 (Creating a Dictionary with a Dictionary Literal)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Creating-a-Dictionary-with-a-Dictionary-Literal)

```swift
var d: [String: Int] = ["a": 18, "b": 28]
```

🕐 可以简写为:
```swift
var d = ["a": 18, "b": 28]
```
### [访问和修改字典 (Accessing and Modifying a Dictionary)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Accessing-and-Modifying-a-Dictionary)

🕐 获取元素个数,
```swift
d.count
```

🕑 判断是否为空:
 ```swift
d.isEmpty
```

🕒 通过 key 添加或修改 value:
```swift
d["c"] = 19
```

🕓 更新并返回旧 value (可选类型):
```swift
var d  = ["a": 18, "b": 28]
if let v = d.updateValue(19, forKey: "a") {
    print(v)
}
```

🕔 获取 value (可选类型):
```swift
var d  = ["a": 18, "b": 28]
if let v = d["b"] {
    print(v)
}
```

🕕 通过赋值方式删除元素:
```swift
dict[key] = nil
```

🕖 通过 key 删除并返回对应的 value (可选类型):
```swift
var d  = ["a": 18, "b": 28]
if let v = d.removeValue(forKey: "a") {
    print(v)
}
```
### [遍历字典 (Iterating Over a Dictionary)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#Iterating-Over-a-Dictionary)

🕐 遍历 key 和 value:
```swift
var d  = ["a": 18, "b": 28]
for (k, v) in d {
}
```

🕑 遍历 key :
```swift
for k in d.keys {
}
```

🕒 遍历 value:
```swift
for v in d.values {
}
```

🕓 将 key 或 value 转换为数组:
```swift
var d  = ["a": 18, "b": 28]
let a = [String](d.keys)
let b = [Int](d.values)
```

🕔 原地排序 key:
```swift
d.keys.sorted()
```

🕕 原地排序 value:
```swift
d.values.sorted()
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->