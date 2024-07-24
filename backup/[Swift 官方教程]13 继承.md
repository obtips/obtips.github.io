[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

## [定义基类 (Defining a Base Class)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Defining-a-Base-Class)
---
```swift
class Pet {
    var name: String = "Pet"
    var age = 0.0
    var description: String {
        return "My name is \(name), I'm \(age) years old."
    }
    
    func eat() {
    }
}
```
## [子类 (Subclassing)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Subclassing)
---
```swift
class Cat: Pet {
    var value = 18.4
}
```

```swift
let cat = Cat()
cat.name = "mimi"
cat.age = 2.3
print(cat.description)
```
## [重写 (Overriding)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Overriding)
---
使用 `override`
### [访问超类的方法, 属性和下标 (Accessing Superclass Methods, Properties, and Subscripts)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Accessing-Superclass-Methods-Properties-and-Subscripts)

使用 `super`:
- 方法: `super.method()`
- 属性: `super.properties`
- 下标: `super[index]`
### [重写方法 (Overriding Methods)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Overriding-Methods)

```swift
class Dog: Pet {
    override func eat() {
        print("I like bones.")
    }
}
let dog = Dog()
dog.eat()
```
### [重写属性 (Overriding Properties)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Overriding-Properties)
#### [重写属性的 Getters 和 Setters (Overriding Property Getters and Setters)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Overriding-Property-Getters-and-Setters)

判断是否属于重写的依据是属性名和其类型:
```swift
class Rabbit: Pet {
    var color = "white"
    override var description: String {
        return super.description + "My color is \(color)"
    }
}

let rabbit = Rabbit()
rabbit.name = "Nity"
rabbit.age = 1.5
print(rabbit.description)
```
#### [重写属性观察器 (Overriding Property Observers)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Overriding-Property-Observers)

```swift
class Pig: Pet {
    var weight = 1.8
    override var age: Double {
        didSet {
            weight = weight * age
        }
    }
}

let pig = Pig()
pig.age = 10
print(pig.weight)
```
## [防止被重写 (Preventing Overrides)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/inheritance#Preventing-Overrides)

使用 `final`


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->