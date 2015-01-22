# Swift Style Guide

This is a working document that proposes a style guide for Apple's recently-announced [Swift](https://developer.apple.com/swift/) language. Feel free to open [issues](https://github.com/jamieforrest/swift-style-guide/issues), or [pull requests](https://github.com/jamieforrest/swift-style-guide/pulls).

## Sources

The style guide is based on the [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/index.html#//apple_ref/doc/uid/TP40014097) book, as well as the *Introduction to Swift*, *Intermediate Swift*, and *Advanced Swift* sessions from [WWDC 2014](https://developer.apple.com/videos/wwdc/2014/)

We also took inspiration from the [NY Times Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide), Ray Wenderlich’s [Swift Style Guide](https://github.com/raywenderlich/swift-style-guide), and GitHub’s [Swift Style Guide](https://github.com/github/swift-style-guide)

## Table of Contents

* [Constants and Variables](#constants-and-variables)
* [Naming](#naming)
* [Type Inference](#type-inference)
* [Spacing](#spacing)
* [Closures](#closures)
* [Booleans](#booleans)
* [Protocols and Extensions](#protocols-and-extensions)

## Constants and Variables
### Avoid Mutable State
Use `let` over `var` where possible to avoid mutable state where it isn't necessary.

### Avoid Force-Unwrapping of Optionals
Force-unwrapping of optionals, e.g., `myVariable!` is dangerous and can cause a runtime exception if the underlying object is `nil`. Instead, use the `if-let` syntax:

```swift
if let foo = foo {
    // Do something with foo
} else {
    // Handle the nil, if applicable
}
```

You can also use optional-chaining, as follows, but see the section below on Optional Chaining for some caveats.

```swift
foo?.doSomething()
```
### Avoid Implicitly Unwrapped Optionals

Implicitly-unwrapped optionals are also dangerous. An implicitly unwrapped optional is declared like

```swift
var foo: String!
```

If `foo` is accessed when it is `nil`, the app will crash. It is better to declare `foo` as `String?`, and use one of the optional unwrapping methods above.

### Avoid Chaining Optionals More Than One Level Deep

Swift allows you to chain optionals to avoid many nested levels of `if-let` clauses. For example, if you have a `Person` class, with an optional `Residence?`, which itself has an optional `var address: String?` field, you could print out a person’s address with the following code:

```swift
println(“\(person.residence?.address?)”)
```

However, doing so is a code smell and usually violates the [Law of Demeter](http://en.wikipedia.org/wiki/Law_of_Demeter). A better way to handle this is to create a computed property called `address()` on the `Person` class that returns the optional address:

```swift
class Person {
	…
	var address: String? {
		return residence?.address?
	}
}

println(“\(person.address?)”)
```

### Naming

Use camelCased variable, method, and function names. Long, descriptive names are good. You can use emoji in names, but if you do, you are crazy. However, other unicode characters in variable names might be sensible. For example, using π to represent the constant pi.

```swift 
let π = 3.14159
```

### Use Implicit Getters on Computed Properties

Prefer this:
```swift
var address: String? {
	return residence?.address?
}
```

Over this:
```swift
var address: String? {
	get {
		return residence?.address?
	}
}
```

## Type Inference

Prefer type inference where possible over explicit type declarations. Type declarations should only be used when the compiler demands it, or in rare cases to make the code more readable.

## Spacing

* Indent using 4 spaces. Never indent with tabs. Be sure to set this preference in Xcode.
* Braces for `func`/`if`/`else`/`switch`/`while` etc. should always open on the same line as the statement but close on a new line.

```swift 
func sayHello() {
    println("Hello!")
}
```

* There should be exactly one blank line between methods to aid in visual clarity and organization.

## Closures

* Trailing closures should be written outside of the parenthesis of the function to which they are being passed

```swift 
sort(names) { $0 > $1 }
```

* If a function takes only one argument, and it's a closure, omit the parens

```swift 
names.map { $0.upperCaseString }
```

## Booleans

Parentheses in boolean expressions are optional in Swift. Omit them where possible.

**For example**
```swift 
if numberOfItems > 2 {
    doSomething()
}
```

## Protocols and Extensions

Protocols should follow the [Single Responsibility Principle](http://en.wikipedia.org/wiki/Single_responsibility_principle) and only define one small piece of functionality. Protocol implementations should be confined to a class extension.

**For example**
```swift 
protocol TextRepresentable {
    func asText() -> String
}

extension Dice: TextRepresentable {
    func asText() -> String {
        return "A \(sides)-sided dice"
    }
}
```
