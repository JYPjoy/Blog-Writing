# Array
```swift
array.count
array.isEmpty
array.contains(5)
array.randomElement()

array[인덱스]
array.first
array.last

array.startIndex
array.endIndex

array.firstIndex(of:요소)
array.lastIndex(of:요소)

array.insert(요소, at: 인덱스)
array.insert(contentsOf:[요소], at:인덱스)
array[인덱스] = 요소
array.replaceSubrange(인덱스, with:[요소])
array.replaceSubrange(인덱스범위, with:[요소])

array += [요소]
array.append(요소)
array.append(contentsOf:요소)

array[0...3] = []
array.remove(at: 인덱스)
array.removeSubrange(0...1)

array.removeFirst(갯수)
array.removeLast(갯수)
array.removeAll()
array.removeAll(keepingCapacity: true)

array.sort()
array.sorted()

array.reverse()
array.reversed()
```
<br/>

# Dictionary
```swift
dic.count
dic.isEmpty
dic.randomElement()

dic["A"] => 값 얻기

dic.keys
dic.values

dic.keys.sorted()
dic.values.sorted()

dic["A"] = "Apple"
dic.updateValue("City", forKey: "C")

dic["B"] = nil
dic.removeValue(forKey: "A")
dic.removeAll()
```

<br/>

# Set
```swift
set.count
set.isEmpty
set.contains(5)
set.randomElement()

set.update(with: 3)
set.remove("Swift")
set.removeAll()

b.isSubset(of:a)
b.isStrictSubset(of:a)

a.isSuperset(of:b)
b.isStrictSuperset(of:a)

d.isDisjoint(with:c)

a.union(b)
a.formUnion(b)

a.intersection(b)
a.formIntersection(b)

a.substracting(b)
a.substract(b)

b.symmetrictDifference(c)
b.formSymmetricDifference(c)
```
<br/>

# 고차함수
```swift
배열.map{클로저}
배열.filter{클로저}

배열.reduce(0){$0 + $1}
배열.reduce(0, +)

배열.forEach{클로저}
배열.compactMap{클로저}
배열.flatMap{클로저}
```

<br/>

# 문자열
```swift
string.lowercased()
string.uppercased()
string.capitalized
== / !=

string.count
string.isEmpty
string.contains("Swift")
string.randomElement()

string.shuffled() //배열로 리턴

string[인덱스]

string.startIndex
string.endIndex

string.index(string.startIndex, offsetBy:2)
string.index(after:)
string.index(before:)
string.firstIndex(of:요소)
string.lastIndex(of:요소)
string.range(of: "Swift")

string.insert(문자, at:인덱스)
string.insert(contentsOf:문자열, at:인덱스)

string.replaceSubrange(범위, with:문자열)
string.replacingOccurences(of:문자열, with:문자열)
string.replacingOccurences(of:with:options:range:)

string.append(문자)
string.append(문자열)

string.remove(at:인덱스)
string.removeSubrange(범위)

string.removeFirst(갯수)
string.removeLast(갯수)

string.removeAll()
string.removeAll(keepingCapacity:true)

string.caseInsensitiveCompare(문자열)
string.compare(문자열)
string.compare(_:options:range:locale:)

//위의 compare메소드의 options 종류
.caseInsensitive, .diacriticInsensitive, .widthInsensitive, .forcedOrdering, .literal, 
.numeric, .anchored, .backwards, .regularExpression

string.contains(문자/문자열)
string.hasPrefix(문자열)
string.hasSuffix(문자열)

string.prefix(갯수)
string.suffix(갯수)
string.commonPrefix(with:문자열)

string.dropFirst(갯수)
string.dropLast(갯수)
```

