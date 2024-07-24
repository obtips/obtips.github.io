[Swift官方文档同步的中文快速入门教程](https://github.com/YugenFring/swift-tutorial-quickstart/wiki)

## [下标语法 (Subscript Syntax)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts#Subscript-Syntax)

🕐 使用 `subscript` 自定义下标查询逻辑:
```swift
struct MyStruct {
    let multi: Int
    subscript(num: Int) -> Int {
        return multi * num
    }
}
```

🕑 通过方括号对实例进行查询:
```swift
let s = MyStruct(multi: 3)
print(s[6]) // 18
```
## [下标使用场景  (Subscript Usage)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts#Subscript-Usage)

取决于你自己
## [下标操作 (Subscript Options)](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/subscripts#Subscript-Options)

🕐 可以像函数一样使用 `subscript`, 只是不能使用 `in-out` 参数. 可以在类型中定义多个 `subscript` 实现, 调用时会根据参数自动匹配

🕑 下面是自定义二维矩阵的实现:
```swift
struct Matrix {
    let rows: Int, columns: Int
    var grid: [Double]
    init(rows: Int, columns: Int) {
        self.rows = rows
        self.columns = columns
        grid = Array(repeating: 0.0, count: rows * columns)
    }
    func indexIsValid(row: Int, column: Int) -> Bool {
        return row >= 0 && row < rows && column >= 0 && column < columns
    }
    subscript(row: Int, column: Int) -> Double {
        get {
            assert(indexIsValid(row: row, column: column), "Index out of range")
            return grid[(row * columns) + column]
        }
        set {
            assert(indexIsValid(row: row, column: column), "Index out of range")
            grid[(row * columns) + column] = newValue
        }
    }
}

var matrix = Matrix(rows: 2, columns: 2)
matrix[0, 1] = 1.5
matrix[1, 0] = 3.2

let someValue = matrix[2, 2] // 报错
```


<!-- ##{"script":"<script src='https://blog.meekdai.com/assets/GmeekTOC.js'></script>"}## -->