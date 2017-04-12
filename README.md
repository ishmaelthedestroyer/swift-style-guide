This is my guide to writing iOS applications in Swift. Projects lead by myself should conform to these conventions.

## Table of Contents
- General
- Naming
- Code Organization
- Inspirations

## General

- Clarity and understanding is the most important goal. While brevity and cleanliness are important, prefer clarity when decision-making.
- No semicolons, unless they are required.
- No parantheses, unless they are required.
- Each variable or constant must be declared on a separate line.
- `let` is preferred over `var`. `var` should only be used when mutability is strictly required.
- Always use named parameters.
- **2 spaces** should be used for indentation. No more, no less, no tabs.

## Naming

- There is no need for Objective-C style prefixing in Swift (e.g. use just `MyClass` instead of `LIMyClass`.
- Use `PascalCase` for type names (e.g. `struct`, `enum`, `class`, `typedef`, `associatedtype`, etc.)
- Use `camelCase` (initial lowercase letter) for function, method, property, constant, variable, argument names, enum cases, etc.
- When dealing with an acronym or other name that is usually written in all capps, actually use all caps in any names that use this in code. The exception is if this word is at the start of a name that needs tos tart with lowercase - in this case, use all lowercase for the acronym.

```
// "HTML" is at the start of a constant name, so we use lowercase "html"
let htmlBodyContent: String = "<p>Hello, World</p>"

// prefer using ID to Id
let profileID: Int = 1

// prefer URLFinder to UrlFinder
class URLFinder {
  /* ... */
}
```

- All constants other than singletons that are instance-independent should be static. All such static constants should be placed in a container enum type as per rule 3.1.16. The naming of this container should be singular (e.g. Constant and not Constants) and it should be named such that it is relatively obvious that it is a constant container. If this is not obvious, you can add a Constant suffix to the name. You should use these containers to group constants that have similar or the same prefixes, suffixes and/or use cases.

```
class MyClassName {
    // PREFERRED
    enum AccessibilityIdentifier {
        static let pirateButton = "pirate_button"
    }

    enum SillyMathConstant {
        static let indianaPi = 3
    }

    static let shared = MyClassName()

    // NOT PREFERRED
    static let kPirateButtonAccessibilityIdentifier = "pirate_button"

    enum SillyMath {
        static let indianaPi = 3
    }

    enum Singleton {
        static let shared = MyClassName()
    }
}
```

- For generics and associated types, use either a single capital letter or a PascalCase word that describes the generic. If this word clashes with a protocol that it conforms to or a superclass that it subclasses, you can append a Type suffix to the associated type or generic name.

```
class SomeClass<T> { /* ... */ }
class SomeClass<Model> { /* ... */ }

protocol Modelable {
    associatedtype Model
}

protocol Sequence {
    associatedtype IteratorType: Iterator
}
```

- Names should be descriptive and unambiguous.

```
// PREFERRED
class RoundAnimatingButton: UIButton { /* ... */ }

// NOT PREFERRED
class CustomButton: UIButton { /* ... */ }
```

- Do not abbreviate, use shortened names, or single letter names.

```
// PREFERRED
class RoundAnimatingButton: UIButton {
    let animationDuration: NSTimeInterval

    func startAnimating() {
        let firstSubview = subviews.first
    }

}

// NOT PREFERRED
class RoundAnimating: UIButton {
    let aniDur: NSTimeInterval

    func srtAnmating() {
        let v = subviews.first
    }
}
```

- Include type information in constant or variable names when it is not obvious otherwise.

```
// PREFERRED
class ConnectionTableViewCell: UITableViewCell {
    let personImageView: UIImageView

    let animationDuration: TimeInterval

    // it is ok not to include string in the ivar name here because it's obvious
    // that it's a string from the property name
    let firstName: String

    // though not preferred, it is OK to use `Controller` instead of `ViewController`
    let popupController: UIViewController
    let popupViewController: UIViewController

    // when working with a subclass of `UIViewController` such as a table view
    // controller, collection view controller, split view controller, etc.,
    // fully indicate the type in the name.
    let popupTableViewController: UITableViewController

    // when working with outlets, make sure to specify the outlet type in the
    // property name.
    @IBOutlet weak var submitButton: UIButton!
    @IBOutlet weak var emailTextField: UITextField!
    @IBOutlet weak var nameLabel: UILabel!

}

// NOT PREFERRED
class ConnectionTableViewCell: UITableViewCell {
    // this isn't a `UIImage`, so shouldn't be called image
    // use personImageView instead
    let personImage: UIImageView

    // this isn't a `String`, so it should be `textLabel`
    let text: UILabel

    // `animation` is not clearly a time interval
    // use `animationDuration` or `animationTimeInterval` instead
    let animation: TimeInterval

    // this is not obviously a `String`
    // use `transitionText` or `transitionString` instead
    let transition: String

    // this is a view controller - not a view
    let popupView: UIViewController

    // as mentioned previously, we don't want to use abbreviations, so don't use
    // `VC` instead of `ViewController`
    let popupVC: UIViewController

    // even though this is still technically a `UIViewController`, this property
    // should indicate that we are working with a *Table* View Controller
    let popupViewController: UITableViewController

    // for the sake of consistency, we should put the type name at the end of the
    // property name and not at the start
    @IBOutlet weak var btnSubmit: UIButton!
    @IBOutlet weak var buttonSubmit: UIButton!

    // we should always have a type in the property name when dealing with outlets
    // for example, here, we should have `firstNameLabel` instead
    @IBOutlet weak var firstName: UILabel!
}
```

- As per Apple's API Design Guidelines, a protocol should be named as nouns if they describe what something is doing (e.g. Collection) and using the suffixes able, ible, or ing if it describes a capability (e.g. Equatable, ProgressReporting). If neither of those options makes sense for your use case, you can add a Protocol suffix to the protocol's name as well. Some example protocols are below.

- When naming function arguments, make sure that the function can be read easily to understand the purpose of each argument.
-


## Inspirations

- https://swift.org/documentation/api-design-guidelines/
- https://github.com/linkedin/swift-style-guide
- https://github.com/github/swift-style-guide
- https://github.com/raywenderlich/swift-style-guide
- https://github.com/coursera/swift-style-guide
