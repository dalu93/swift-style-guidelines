# Swift style guidelines
A set of Swift syntax guidelines for Swift projects.
Feel free to fork and contribute with your own guidelines.

- [Variables and constants](#variables-and-constants)
- [Methods](#methods)
- [Type declaration](#type-declaration)
- [Extensions](#extensions)
- [Marks](#marks)

## Variables and constants
### Define constants or, only if needed, variables
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
Try to keep the property not-optional as possible by assigning a default value.
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

## Methods
### Method definition
Always follow the Swift API guidelines for method naming convention.
The same rule valid for public/private properties is valid for methods

```swift
// public definition
func doSomething()

// private definition
fileprivate/private func _doSomething()
```

### Brackets position
Always type the first bracket on the same line of the definition

```swift
// correct way
func doSomething() {
}

// wrong way
func doSomething()
{
}
```

Do not leave any line between the implementation and the declaration
```swift
// correct way
func doSomething() {
    print("something")
}

// wrong way
func doSomething() {

    print("something")
}
```

## Type declaration
Remember to always define, in case of `class`, the declaration as `final`. Then, if needed, switch to open/default to allow inheritance.

### Brackets position
Always type the first bracket on the same line of the declaration

```swift
final class User {
}

struct User {
}

enum UserType {
}

protocol UserType {
}

extension User {
}
```

Always leave one line from the declaration and the implementation.

```swift
final class User {

    var email: String = ""
}

protocol UserType {

    var email: String { get }
}

enum UserType {

    case facebook, twitter
}

extension User {

    func doSomething {
    }
}
```

## Extensions
### Use extension to conform to a protocol
Always use a separated extension to conform a single protocol

```swift
final class ViewController: UIViewController {
}

extension ViewController: UITableViewDataSource {

    // dataSource implementation
}
```

### Use extensions to separate the code
Always use extensions to separate different parts of the object

```swift
final class ViewController: UIViewController {

    // Here only stored-properties declarations and overrides
}

extension ViewController {

    // Here the viewModel interaction
}

extension ViewController {

    // Here the IBActions
}

extension ViewController {

    // Here the cache management
}
```

### Use private extensions
In case you need to group a set of methods/computed properties which they are all private, instead of naming them all as private, define the extension as private

```swift
private extension Object {

    // Here a set of private functions/properties
}
```

## Marks
### Use marks for each extension
By using the combination `CMD + ALT + /` on the line on top of the extension declaration, Xcode creates a mark for you in this form:

```swift
// MARK: - DESCRIPTION
```

Use the description to describe the extension scope.

### Use marks to separate different type of stored-properties and methods
```swift
// MARK: - Controller declaration
final class Controller: UIViewController {

    // MARK: - Private outlets
    @IBOutlet fileprivate weak var _titleLabel: UILabel!
    fileprivate lazy var _shadowView: UIView = self._makeShadowView()

    // MARK: - Private properties
    fileprivate var _toCheckSomething = true

    // MARK: - Public properties
    var item: Object!

    // MARK: - View lifecycle
    override func viewDidLoad() {
        super.viewDidLoad()
    }

    // MARK: - Object lifecycle
    deinit {
        print("deinitialized")
    }
}
```
