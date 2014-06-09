# Swift Style Guide

This is a working document that proposes a style guide for Apple's recently-announced [Swift](https://developer.apple.com/swift/) language. Feel free to open [issues](https://github.com/jamieforrest/swift-style-guide/issues), or [pull requests](https://github.com/jamieforrest/swift-style-guide/pulls).

## Sources

The style guide is based on the [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/index.html#//apple_ref/doc/uid/TP40014097) book, as well as the *Introduction to Swift*, *Intermediate Swift*, and *Advanced Swift* sessions from [WWDC 2014](https://developer.apple.com/videos/wwdc/2014/)

We also took inspiration from the [NY Times Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)

## Table of Contents

* [Constants and Variables](#constants-and-variables)
* [Naming](#naming)
* [Type Inference](#type-inference)
* [Spacing](#spacing)
* [Closures](#closures)
* [Booleans](#booleans)

## Constants and Variables

Use `let` over `var` where possible to avoid mutable state where it isn't necessary.

## Naming

Use camelCased variable, method, and function names. Long, descriptive names are good. You can use emoji in names, but if you do, you are crazy. However, other unicode characters in variable names might be sensible. For example, using π to represent the constant pi.

```let π = 3.14159```

## Type Inference

Prefer type inference where possible over explicit type declarations. Type declarations should only be used when the compiler demands it, or in rare cases to make the code more readable.

## Spacing

* Indent using 4 spaces. Never indent with tabs. Be sure to set this preference in Xcode.
* Braces for `func`/`if`/`else`/`switch`/`while` etc. should always open on the same line as the statement but close on a new line.

```
func sayHello() {
    println("Hello!")
}
```

* There should be exactly one blank line between methods to aid in visual clarity and organization.

## Closures

* Trailing closures should be written outside of the parenthesis of the function to which they are being passed

```
sort(names) { $0 > $1 }
```

* If a function takes only one argument, and it's a closure, omit the parens

```
names.map { $0.upperCaseString }
```

## Booleans

Parentheses in boolean expressions are optional in Swift. Omit them where possible.

**For example**
```
if numberOfItems > 2 {
    doSomething()
}
```
