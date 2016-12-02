# Swift style guidelines
A set of Swift syntax guidelines for Swift projects.
Feel free to fork and contribute with your own guidelines.

- [Variable and constants](#features)

## Variable and constants
### Define constants and, if needed, variables
Always declare the property as a constant (`let`) and, only if needed, switch to a variable (`var`)
This is valid for any type properties that supported stored properties (`struct`, `class`) and in global scope or method/closure scope

```swift
// Struct example
struct MyStruct {
    let property: Any
}

// Class example
class MyClass {
    let property: Any
}

// Method/closure example
func doSomething() {
    let data = Manager.data
    // do something with data 
}
```

### Private/fileprivate is always preferred
Always declare your property as `private/fileprivate` first. If needed, change the declaration to a public one.
Every time a property is `private/fileprivate`, it has to be marked with an `_` (underscore) in the name

```swift
// Normal private constant
private let _viewModel = ViewModel()

// Private outlet
@IBOutlet private weak var _tableView: UITableView!

// Public constant
var state: ViewState = .default

// Get-only public variable
private(set) var state: ViewState = .default
```

### Type inference
Always declare the property type where it's not implicit inferred by the compiler.

```swift
// Correct version
let viewState: ViewState = .default

// Wrong version
let viewState = ViewState.default
```

```swift
// Correct version
let arrayOfIntegers: [Int] = []

// Wrong version
let arrayOfIntegers = [Int]()
```

### Initial value
Try to keep the property not-optional as possible.
An example could be an array of items that has to be displayed in a tableView.

```swift
// Correct version
var dataSource: [Item] = []

// Wrong version
var dataSource: [Item]? = nil
```

The second implementation doesn't make sense since the tableView has, anyway, nothing to render.
This is a preferred style, but, if needed, the `Optional` type can be used.

### Colon position
Always type the colon next to the identifer

```swift
// Correct version
let number: Int = 0

// Wrong version
let number :Int = 0
```


