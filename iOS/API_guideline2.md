# [3] Conventions
## (1) General conventions
#### computed property의 복잡도가 O(1)이 아니라면 복잡도를 주석으로 남겨주세요.
```swift
import Founcation

/// Time Complexity: O(n^2)
class Company {
    var numberOfEmployees: Int {
        var result: Int = 0

        (0...n).forEach {
            (0...n).forEach{
                (0...n).forEach{
                    result += 1
                }
            }
        }
        return result
    }
}
```

#### 전역 함수 대신에 method와 property를 사용하세요.

 전역 함수는 아래와 같이 특수한 경우에만 사용됩니다.
```swift
// 명확한 self 가 없는경우
min(x, y, z)  

//function이 generic으로 제약조건이 걸려있지 않을 때
print(x) 

//function 구문이 해당 도메인의 표기법인 경우
sin(x) 
```

#### 대소문자 컨벤션을 따르세요.
type, protocol의 이름은 `UpperCamelCase`, 나머지는 `lowerCamelCase`를 따릅니다.

```swift
    var utf8Bytes: [UTF8] = []
    var webstieURL: URL?
    var urlString: String?

```

#### 기본 뜻이 같거나 구별되는 서로 구별되는 도메인에서 작동하는 Method는 base name을 동일하게 사용할 수 있습니다.

###### 👍 [좋은 예시 1]
기본적으로 `같은 동작`을 하는 메소드들의 나열
```swift
struct Shape {
    func contains(_ otehr: Point) -> Bool {}
    func contains(_ other: Shape) -> Bool {}
}

let shape = Shape()
shape.contains(Point())
shape.contains(Shape())

```

###### 👍 [좋은 예시 2]
위의 Shape 와 collection type은 구별된 도메인이기 때문에, 같은 프로그램 안에서 다음과 같이 사용할 수 있습니다.
``` swift
struct Shape {
    func contains(_ otehr: Point) -> Bool {}
    func contains(_ other: Shape) -> Bool {}
}

extension Collection where Element : Equatable {
  func contains(_ sought: Element) -> Bool { ... }
}
```

###### 👎 [나쁜 예시 1]
아래의 index method는 `다른 의미`를 갖고 있기 때문에, `다르게 네이밍` 되어야 합니다.
```swift
extension Database {
  /// Rebuilds the database's search index
  func index() { ... }

  /// Returns the `n`th row in the given table.
  func index(_ n: Int, inTable: TableID) -> TableRow { ... }
}

```

###### 👎 [나쁜 예시 2]
`"overloading on return type"(리턴 값을 오버로딩 하는 경우)`은 타입 추론의 유무에 따라 모호한 경우가 있어서 권장되지 않습니다.
``` swift
struct Box {
    private let rawValue: Int

    init(_ rawValue: Int) {
        self.rawValue = rawValue
    }

    func value() -> Int? {
        rawValue
    }

    func value() -> String {
        "\(rawValue)"
    }
}

let myBox = Box(100)
myBox.value() as Int?
myBox.value() as String?

let intBoxValue: Int? = myBox.value()
```

<br/>

## (2) Parameters
#### 주석을 읽기 쉽게 만들어주는 파라미터 이름을 선택하세요.
###### 👍 [좋은 예시]

```swift
    /// Return an `Array` containing the elements of `self`
    /// that satisfy `predicate`.
    func filter(_ predicate: (Element) -> Bool) -> [Generator.Element]

    /// Replace the given `subRange` of elements with `newElements`.
    mutating func replaceRange(_ subRange: Range, with newElements: [E])

    func move(from start: Point, to end: Point){}

```
###### 👎 [나쁜 예시]
```swift
    /// Return an `Array` containing the elements of `self`
    /// that satisfy `includedInResult`.
    func filter(_ includedInResult: (Element) -> Bool) -> [Generator.Element]

    /// Replace the range of elements indicated by `r` with
    /// the contents of `with`.
    mutating func replaceRange(_ r: Range, with: [E])
    
```

#### 일반적인 사용을 단순화 할 수 있다면, `Defaulted Parameters`를 사용하세요
###### 👍 [좋은 예시]

```swift
// #1
let order = lastName
            .compare(royalFamilyName, options: [], range: nil, locale: nil)
let order = lastName.compare(royalFamilyName)

// #2
extension String {
  /// ...description...
  public func compare(
     _ other: String, options: CompareOptions = [],
     range: Range? = nil, locale: Locale? = nil
  ) -> Ordering
}
```
###### 👎 [나쁜 예시]
```swift
extension String {
  /// ...description 1...
  public func compare(_ other: String) -> Ordering
  /// ...description 2...
  public func compare(_ other: String, options: CompareOptions) -> Ordering
  /// ...description 3...
  public func compare(
     _ other: String, options: CompareOptions, range: Range) -> Ordering
  /// ...description 4...
  public func compare(
     _ other: String, options: StringCompareOptions,
     range: Range, locale: Locale) -> Ordering
}
    
```
#### Default parameter를 parameter list `끝 부분`에 두는 것을 선호합니다
```swift
//Default Parameter를 끝부분에 두었을 경우의 호출문
compare("A")
compare("B", locale: nil)
compare("B", options:[], locale: nil)
compare("B", options:[], range: nil, locale: nil)


//Default Parameter를 끝부분에 두지 않았을 경우의 호출문
compare("A")
compare(locale: nil, "B")
compare(options:[], locale: nil, "B")
compare(options:[], range: nil, locale: nil, "B")
```

<br/>

## (3) Argument Labels
```swift
// from과 to가 arugument label
func move(from start: Point, to end: Point)
x.move(from: x, to: y) 
```

#### label을 써도 유용하게 구분이 되지 않는다면 모든 label을 생략하세요
```swift
min(number1, number2)
zip(sequence1, sequence2)
```


#### 값을 유지하면서 타입 변환을 해주는 initializer에서, 첫번째 argument label을 생략하세요.
```swift
Int64(someUInt32) // UInt32에서 Int64로 확장되므로
```
<br/>
첫번째 argument는 항상 source of conversion 이어야 한다.

```swift
extension String {
// Convert `x` into its textual representation in the given radix
init(_ x: BigInt, radix: Int = 10)   ← Note the initial underscore
}

text = "The value is: "
text += String(veryLargeNumber)
text += " and in hexadecimal, it's"
text += String(veryLargeNumber, radix: 16)
```


값의 범위가 좁혀지는 타입 변환의 경우, label을 붙여서 설명하는 것을 추천합니다
```swift
extension UInt32 {
/// Creates an instance having the specified `value`.
init(_ value: Int16)            ← Widening, so no label

/// Creates an instance having the lowest 32 bits of `source`.
// 값이 줄여지므로 truncating 붙어야 한다.
init(truncating source: UInt64)

/// Creates an instance having the nearest representable
/// approximation of `valueToApproximate`.
init(saturating valueToApproximate: UInt64)
}
```

#### 첫 번째 argument가 전치사구의 일부일 때, argument label로 지정합니다
argument label은 보통 전치사로 시작합니다. 
```swift
func removeBoxes(havingLength length: Int) {}

x.removeBoxes(havingLength: 12)
```

처음에 나오는 2개의 argument들이 단일 추상화를 표현하는 경우는 예외입니다.
```swift
// 👍 좋은 예시 
a.moveTo(x: b, y: c)
a.fadeFrom(red: b, green: c, blue: d)

// 👎 나쁜 예시
a.move(toX: b, y: c)
a.fade(fromRed: b, green: c, blue: d)
```

#### 만약 첫번째 argument가 문법적 구절을 만든다면 label은 제거하고, 함수 이름에 base name을 추가합니다.
```swift
x.addSubview(y)
```
첫번째 argument가 문법적으로 구절을 만들지 않는다면, label을 둬야한다는 것을 암시합니다.

```swift
// 👍 좋은 예시 
view.dismiss(animated: false)
let text = words.split(maxSplits: 12)
let studentsByName = students.sorted(isOrderedBefore: Student.namePrecedes)

// 👎 나쁜 예시
view.dismiss(false)   Don't dismiss? Dismiss a Bool?
words.split(12)       Split the number 12?
```

default value를 가진 argument는 생략될 수 있으며, 이 경우 문법 구문의 일부를 형성하지 않으므로 항상 레이블이 있어야 합니다.
```swift
extension String {
  /// ...description...
  public func compare(
     _ other: String, options: CompareOptions = [],
     from range: Range? = nil, with locale: Locale? = nil
  ) -> Ordering
}
```

#### 나머지 모든 경우, argument들은 Label을 붙여야 합니다

<br/>

# [4] Special Instructions
#### tuple members와 closure parameters에 Label을 붙이세요.
```swift
struct Storage {
    func doSomething() -> (reallocated: Bool, capacityChanged: Bool) {
        return (true, false)
    }
}

let storage = Storage()
let result = storage.doSomething()

result.reallocated // true
result.capacityChanged //false

```

#### overload set에서의 모호함을 피하기 위해, 제약 없는 다형성에 각별히 주의하세요.

###### 👍 좋은 예시 
```swift
struct Array {
  /// Inserts `newElement` at `self.endIndex`.
  public mutating func append(_ newElement: Element)

  /// Inserts the contents of `newElements`, in order, at
  /// `self.endIndex`.
  public mutating func append(contentsOf newElements: S)
    where S.Generator.Element == Element
}

var values: [Any] = [1, "a"]
values.append(contentsOf:[2, 3, 4]) //[1,"a", 2, 3, 4]

```


###### 👎 나쁜 예시
```swift
struct Array {
  /// Inserts `newElement` at `self.endIndex`.
  public mutating func append(_ newElement: Element)

  /// Inserts the contents of `newElements`, in order, at
  /// `self.endIndex`.
  public mutating func append(_ newElements: S)
    where S.Generator.Element == Element
}

var values: [Any] = [1, "a"]
values.append([2, 3, 4]) // [1, "a", [2, 3, 4]] or [1, "a", 2, 3, 4]?
```

<br/>

# 참고
- 공식 문서: https://www.swift.org/documentation/api-design-guidelines/
- 번역본: https://cozzin.gitbook.io/swift-api-design-guidelines/naming/strive-for-fluent-usage


