#start developing ios apps

https://developer.apple.com/library/content/referencelibrary/GettingStarted/DevelopiOSAppsSwift/Lesson1.html#//apple_ref/doc/uid/TP40015214-CH3-SW1

根据apple官方指南，笔记如下：

------

## Swift
### Basic types

```swift
var myVariable = 42
myVariable = 50
let myConstant = 42
```

**type inference:**

Every constant and variable in Swift has a type, but you don’t always have to write the type explicitly. Providing a value when you create a constant or variable lets the compiler infer its type. In the example above, the compiler infers that myVariable is an integer because its initial value is an integer. This is called type inference.

Specify the type by writing it after the variable, separated by a colon.

```swift
let implicitDouble = 70.0
let explicitDouble: Double = 70
```
>In Xcode, Option-click the name of a constant or variable to see its inferred type.

强制类型转换：

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```
**string interpolation: **
Write the value in parentheses, and write a backslash (\) before the parentheses.

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```
Use optionals to work with values that might be missing. An **optional value** either contains a value or contains nil (no value) to indicate that a value is missing. Write a question mark (?) after the type of a value to mark the value as optional.

```swift
let optionalInt: Int? = 9
```
To get the underlying type from an optional, you unwrap it. You’ll learn unwrapping optionals later, but the most straightforward way to do it involves the *force unwrap operator* (!). Only use the unwrap operator if you’re sure the underlying value isn’t nil.

~~~swift
let actualInt: Int = optionalInt!
~~~

Optionals are especially useful for attempted type conversions.

```swift
var myString = "7"
var possibleInt = Int(myString)
print(possibleInt)
```
**Array**

```swift
var ratingList = ["Poor", "Fine", "Good", "Excellent"]
ratingList[1] = "OK"
ratingList

// Creates an empty array.
let emptyArray = [String]() // Initializer
```
### Control Flow

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
```
Use optional binding in an if statement to check whether an optional contains a value.

```swift
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```
switch-case:

```swift
let vegetable = "red pepper"
switch vegetable {
    case "celery":
        let vegetableComment = "Add some raisins and make ants on a log."
    case "cucumber", "watercress":
        let vegetableComment = "That would make a good tea sandwich."
    case let x where x.hasSuffix("pepper"):
        let vegetableComment = "Is it a spicy \(x)?"
    default:
        let vegetableComment = "Everything tastes good in soup."
}
```
You can keep an index in a loop by using a **Range**. Use the **half-open range operator** (`..<`) to make a range of indexes.

```swift
var firstForLoop = 0
for i in 0..<4 {
    firstForLoop += i
}
print(firstForLoop)
```
The half-open range operator (..<) doesn’t include the upper number, so this range goes from 0 to 3 for a total of four loop iterations. Use the closed range operator (`...`) to make a range that includes both values.

```swift
var secondForLoop = 0
for _ in 0...4 {
    secondForLoop += 1
}
print(secondForLoop)
```
The underscore (`_`) represents a **wildcard**, which you can use when you don’t need to know which iteration of the loop is currently executing.

###Functions and Methods
Use `func` to declare a function. A function declaration can include zero or more parameters, written as `name: Type`. Optionally, a function can have a return type, written after the `->`, which indicates what the function returns as its result.

```swift
func greet(name: String, day: String) -> String {
    return "Hello \(name), today is \(day)."
}
```
When you call a function, you pass in the first argument value without writing its name, and every subsequent value with its name.

```swift
greet("Anna", day: "Tuesday")
greet("Bob", day: "Friday")
greet("Charlie", day: "a nice day")
```
###Classes and Initializers
```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```
This `Shape` class is missing something important: an `initializer`. An initializer is a method that prepares an instance of a class for use, which involves setting an initial value for each property and performing any other setup. Use `init` to create one. This example defines a new class, `NamedShape`, that has an initializer which takes in a name.

```swift
class NamedShape {
    var numberOfSides = 0
    var name: String

    init(name: String) {
       self.name = name
    }

    func simpleDescription() -> String {
       return "A shape with \(numberOfSides) sides."
    }
}
```
Notice how `self` is used to distinguish the name property from the name argument to the initializer. Every property needs a value assigned—either in its declaration (as with numberOfSides) or in the initializer (as with name).

When you call an initializer, you include all arguments names along with their values.

```swift
let namedShape = NamedShape(name: "my named shape")
```
Methods on a subclass that override the superclass’s implementation are marked with `override`—overriding a method by accident, without override, is detected by the compiler as an error. The compiler also detects methods with override that don’t actually override any method in the superclass.

This example defines the `Square` class, a subclass of `NamedShape`.

```swift
class Square: NamedShape {
    var sideLength: Double

    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }

    func area() ->  Double {
        return sideLength * sideLength
    }

    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let testSquare = Square(sideLength: 5.2, name: "my test square")
testSquare.area()
testSquare.simpleDescription()

```

Sometimes, initialization of an object needs to fail, such as when the values supplied as the arguments are outside of a certain range, or when data that’s expected to be there is missing. Initializers that may fail to successfully initialize an object are called failable initializers. A failable initializer can return `nil` after initialization. Use `init?` to declare a failable initializer.

```swift
class Circle: NamedShape {
    var radius: Double

    init?(radius: Double, name: String) {
        self.radius = radius
        super.init(name: name)
        numberOfSides = 1
        if radius <= 0 {
            return nil
        }
    }

    override func simpleDescription() -> String {
        return "A circle with a radius of \(radius)."
    }
}
let successfulCircle = Circle(radius: 4.2, name: "successful circle")
let failedCircle = Circle(radius: -7, name: "failed circle")
```
###Enumerations and Structures
Enumerations define a common type for a group of related values and enable you to work with those values in a type-safe way within your code. Enumerations can have methods associated with them.

Use `enum` to create an enumeration.

```swift
enum Rank: Int {
    case Ace = 1
    case Two, Three, Four, Five, Six, Seven, Eight, Nine, Ten
    case Jack, Queen, King
    func simpleDescription() -> String {
        switch self {
            case .Ace:
                return "ace"
            case .Jack:
                return "jack"
            case .Queen:
                return "queen"
            case .King:
                return "king"
            default:
                return String(self.rawValue)
        }
    }
}
let ace = Rank.Ace
let aceRawValue = ace.rawValue
```
//后面一部分没有写（感觉没什么大用
###Protocols

A `protocol` defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol doesn’t actually provide an implementation for any of these requirements—it only describes what an implementation will look like. The protocol can then be adopted by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to conform to that protocol.

```swift
protocol ExampleProtocol {
     var simpleDescription: String { get }
     func adjust()
}
```
> Note: The `{ get }` following the simpleDescription property indicates that it is read-only, meaning that the value of the property can be viewed, but never changed.

// 关于protocols以后如果要用到的时候再学

###Swift and Cocoa Touch

> `alt`+鼠标左键点击：看到变量的基本属性，类的属性，以及一些方法

When writing iOS apps, you’ll be using more than the `Swift standard library`. One of the most frequently used frameworks in iOS app development is `UIKit`. `UIKit` contains useful classes for working with the UI (user interface) layer of your app.

```swift
import UIKit

let redSquare = UIView(frame: CGRect(x: 0, y: 0, width: 44, height: 44))
redSquare.backgroundColor = UIColor.red
```

//finally! finish!