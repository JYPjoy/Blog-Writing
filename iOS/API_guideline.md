
# Foundamentals
1. 사용할 때 명확하게 느끼는 것이 **가장** 중요합니다.
2. 명확한 것 > 간결한 것 
    ```swift
        let blackButton (O)
        let blackBtn (x)
    ```
3.  모든 선언에 대해 문서 주석(Documentation Comment)를 작성해 주세요
     ```swift
    /// Writes the textual representation of each  
    /// element of `items` to the standard output.
    ///                                              ← Blank line 빈줄
    /// The textual representation for each item `x` 
    /// is generated by the expression `String(x)`.
    ///
    /// - Parameter separator: text to be printed    ⎫
    ///   between items.                             ⎟
    /// - Parameter terminator: text to be printed   ⎬ Parameters section
    ///   at the end.                                ⎟
    ///                                              ⎭
    /// - Note: To print without a trailing          ⎫
    ///   newline, pass `terminator: ""`             ⎟
    ///                                              ⎬ Symbol commands
    /// - SeeAlso: `CustomDebugStringConvertible`,   ⎟
    ///   `CustomStringConvertible`, `debugPrint`.   ⎭
    public func print(_ items: Any..., separator: String = " ", terminator: String = "\n")
    ```

<br/><br/>

# Naming
## Promote Clear Usage
1. 필요한 단어들을 모두 포함해 두세요
   ```swift
    employees.remove(at: x) (👍)
    employees.remove(x) (👎)
   ```

2. 불필요한 단어를 생략하세요
   ```swift
    allViews.removeElement(cancelButton) (👍)
    allViews.remove(cancelButton) (👎)
   ```

3. 타입 대신 역할에 따라 변수(variables), 파라미터(parameters), 연관타입(associated types)을 네이밍하세요.
    ```swift
    ///Good(👍)
    var greeting = "Hello"
    protocol ViewController {
        associatedtype ContentView : View
    }
    class ProductionLine {
        func restock(from supplier: WidgetFactory)
    }

    ///Bad(👎)
    var string = "Hello"
    protocol ViewController {
        associatedtype ViewType : View
    }
    class ProductionLine {
        func restock(from widgetFactory: WidgetFactory)
    }

    ```

4. 파라미터의 역할을 명확히 하기 위해 불충분한 type 정보를 보충하세요
    ```swift
    ///Good(👍)
        final class MyNotificationCenter{
            private var observers: [String:NSObject] = [:]

            func add(_ observer: NSObject, forKeyPath keyPath: String) {
                observers[keyPath] = observer
            }
        }

        let center = MyNotificationCenter()
        center.add(self, forKeyPat: "mykey")


     ///Bad(👎)
        final class MyNotificationCenter{
            private var observers: [String:NSObject] = [:]

            func add(_ observer: NSObject, for keyPath: String) {
                observers[keyPath] = observer
            }
        }

        let center = MyNotificationCenter()
        center.add(self, for: "key")
    ```
<br/>

## Strive for Fluent Usage








## Use Terminology Well


    ```swift
    
    ```