#start developing ios apps

https://developer.apple.com/library/content/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Lesson1.html#//apple_ref/doc/uid/TP40015214-CH3-SW1

根据apple官方指南，笔记如下

------

## Swift
### Basic types

```
var myVariable = 42
myVariable = 50
let myConstant = 42
```

**type inference:**

Every constant and variable in Swift has a type, but you don’t always have to write the type explicitly. Providing a value when you create a constant or variable lets the compiler infer its type. In the example above, the compiler infers that myVariable is an integer because its initial value is an integer. This is called type inference.

Specify the type by writing it after the variable, separated by a colon.

```
let implicitDouble = 70.0
let explicitDouble: Double = 70
```
>In Xcode, Option-click the name of a constant or variable to see its inferred type.

强制类型转换：

```
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```
**string interpolation: **
Write the value in parentheses, and write a backslash (\) before the parentheses.

```
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```
Use optionals to work with values that might be missing. An **optional value** either contains a value or contains nil (no value) to indicate that a value is missing. Write a question mark (?) after the type of a value to mark the value as optional.

```
let optionalInt: Int? = 9
```
To get the underlying type from an optional, you unwrap it. You’ll learn unwrapping optionals later, but the most straightforward way to do it involves the *force unwrap operator* (!). Only use the unwrap operator if you’re sure the underlying value isn’t nil.

```
let actualInt: Int = optionalInt!
```
Optionals are especially useful for attempted type conversions.

```
var myString = "7"
var possibleInt = Int(myString)
print(possibleInt)
```
**Array**

```
var ratingList = ["Poor", "Fine", "Good", "Excellent"]
ratingList[1] = "OK"
ratingList

// Creates an empty array.
let emptyArray = [String]() // Initializer
```
