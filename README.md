# Tuples

![Drawing](http://i.imgur.com/gMMSTqF.jpg?1)

> A day without sunshine is like, you know, night. -Steve Martin 

## Learning Objectives 

* Explain what a tuple is, how to create it, use it, break down its members.
* Understand clearly the problem addressed below and how using a tuple solves it.
* Create their own tuple in code.
* Feel comfortable creating a function with the return type being a tuple.

## The Point of Tuples

Consider a relatively simple data structure: A point in 2D space. You probably remember from geometry that such a point consists of two coordinates _(x,y)_ which together tell you where a point lies in a graph. Each individual value—_x_ and _y_—are important, but when you think of a point, you really think of these values together as _one unit_. An _x_ alone alone won't describe the location of a point. Nor will a _y_ value alone. You need both—together—to know where a point lies.

What data structure would you use?

You could use an array like you learned about in a previous unit, but an array doesn't really capture the _spirit_ of a 2D point. An array is more like a _list of things_. A 2D point is something special...it consists of multiple values, but those values are tied inextricably tied together and treated as a single unit.

You could instead use another Swift data structure to represent a 2D point: a _tuple_.

## Much Ado About Tuples

Geometrical points are pretty abstract, so let's take a look at a more practical example. Say you were tasked with writing a function called `downloadImage(atURL:)` that will download an image at a given URL, and return `true` if the image was downloaded. Your function might look something like this:

```swift
func downloadImage(atURL url: String) -> Bool {
    // TODO: Download image
    return true
}
```

Great! We can fill in the guts of that function later (much later, since actually downloading the image isn't terribly relevant to this lesson). Of course, you also have to deal with the case in which the image could _not_ be downloaded due to an error: No wireless network, invalid URL, or aliens are destroying Earth. Assume that the code you use to actually download the image gives you back an error in the form of a string detailing why the image failed to download. `downloadImage(atURL:)` will probably look something like this:

```swift
func downloadImage(atURL url: String) -> Bool {
    // TODO: Download image
    // if no error, return true
    // otherwise, get error string and return false
    return false
}
```

Great! One little snag, though: That error message might be really useful to the code that called `downloadImage(atURL:)`, but right now it has disappeared, lost forever in the bowels of `downloadImage(atURL:)`. It'd be nice to return the error message string if the download fails, wouldn't it?

Well, that's easy enough to do! Just return the string, right?

```swift
func downloadImage(atURL url: String) -> Bool {
    // TODO: Download image
    // if no error, return true
    // otherwise, get error string and return false
    let error = "Image no longer exists"
    return error
}
```

Great! Err...not so great, actually. The function is supposed to return a `Bool`, but now it is returning a `String`, and that's not possible in Swift. That code won't even compile! And even if it could, you'd still like to also return `false` if the image download fails. Really, you need to be able to return two _values_ from a function: One of type `Bool`, indicating success or failure of the function, and one of type `String`, with a message indicating why the function failed (and some other positive affirmation if the function succeeds).

But how can you do that?

When you think about it, what you're trying to do is a little bit like representing a 2D point: You want to have _two_ values that are treated as _one_ unit (since a function can only return _one_ thing).

You want to return a tuple.

In Swift, a tuple is a funny word (seriously, it doesn't exactly [roll off the tongue](https://www.youtube.com/watch?v=7fTVCQRQYXk)) that describes a structure in which multiple values are grouped together as one. Like a 2D point! Or like returning a boolean and an error message as one unit.

The type of a Swift tuple is described by putting the type of each of its parts in parentheses, separated by commas. For example, a 2D point consists of two `Int`s grouped together, and would look like this in Swift:

```swift
let p1: (Int, Int) = (1, 2)
```

Take special note of the `(Int, Int)` part. In plain English, that means, "a tuple consisting of two `Int`s."

On the other hand, a tuple consisting of a boolean and a string would look like this:

```swift
let x: (Bool, String) = (false, "Image no longer exists at URL")
```

Again, the relevant bit here is `(Bool, String)`, which means "a tuple consisting of a `Bool` and a `String`.

Knowing that, let's rewrite `downloadImage(atURL:)` so it returns a tuple instead of just a `Bool`. Here's what your rewritten function would look like (without all the cool downloading code written yet):

```swift
func downloadImage(atURL url: String) -> (Bool, String) {
    // TODO: Download image
    // if no error, return true
    // otherwise, get error string and return false
    let error = "Image no longer exists"
    return (false, error)
}
```

Take particular notice of the return type. It changed from `Bool` to `(Bool, String)`. That kind of looks almost like a function argument list, doesn't it? Well, looks can be deceiving. A tuple doesn't really have anything to do with a function argument list; it just shares a similar syntax. It's a type unto itself, just like `Bool` and `String` and `Int` are types.

Notice, too, how the `return` statement changed. It says `return (false, error)` now. That's how you create a tuple: By putting all of its values in parentheses, separated by commas. Pretty easy, right? In fact, it doesn't look that much different than the way you wrote out 2D points in geometry class—because it's not really that different at all!

## Accessing Elements of a Tuple

Okay, so you have a tuple. How do you access its individual elements?

Say you wrote some code to call your `downloadImage(atURL:)` function and saved it in a variable:

```swift
let result = downloadImage(atURL: "http://example.com/image.png")
```

How would you get the first component—the `Bool` that tells you if the image was downloaded or not?

It's pretty easy. You type the constant's or variable's name, followed by a dot (`.`), and then a number representing the _position_ of the individual value you want. You can see this pretty clearly if you type `result.` and let Xcode do the autocompletion for you:

![Tuple autocomplete](http://i.imgur.com/YdlVEbS.png)

Fields in a tuple are numbered starting at 0, so `0` is the first field, `1` is the second, and so forth.

This code will grab the result of `downloadImage(atURL:)`, then print "Success? false" and the error message to the console:

```swift
let result = downloadImage(atURL: "http://example.com/image.png")
print("Success? \(result.0)")
// prints "Success? false"
print("Message: \(result.1)")
// prints "Message: Image no longer exists"
```

### Naming Elements

`result.0` and `result.1` doesn't tell you much about the elements of the tuple, does it? It might be hard to remember which value is in which position. The elements of a tuple can also be named. You give them names when you create the tuple:

```
let person = (name: "Jim", age: 30)
```

You can now access the individual parts of the tuple by their names (`name` and `age`) instead of using numbered fields. Again, Xcode's autocomplete will help you out here:

![Tuple autocomplete with named fields](http://i.imgur.com/tpeouX1.png)

Now you can access individual parts of the tuple in a much more readable way:

```swift
let person = (name: "Jim", age: 30)
print("\(person.name)'s age is \(person.age)")
// prints "Jim's age is 30"
```

Notice, too, that Xcode's autocomplete also lets you know the _type_ of each field: `name` is a `String` and `age` is an `Int`. This information can be very useful when working with tuples.

### Changing Values

Say you created this tuple:

```swift
let person = (name: "Jim", age: 30)
```

You then realize that Jim is actually 32 (he's been lying about his age all along). You want to update that information. How would you do that? Would the following code work?

```swift
let person = (name: "Jim", age: 30)
person.age = 32
```

_Should_ it work? Think back to what you know about constants and variables. `person` was declared as a constant (using the `let` keyword). If you tried this code out in a playground (you should!), you'll probably notice that the playground won't let you change the value of `person.age`—it tells you that `person` is a "let" constant.

Which makes sense, right? Constants can't change, and when you create a constant tuple, the individual parts of the tuple are considered to be constants, too. How could you fix this so that you _can_ change the individual elements?

If you guessed "declare it to be a _variable_," you're right. When a constant is declared as a _variable_ (using the `var` keyword), its individual parts are variables, too, and you can change them. This code will work:

```swift
var person2 = (name: "Jim", age: 30)
print("\(person2.name)'s age is \(person2.age)")
// prints "Jim's age is 30"
person2.age = 32
print("\(person2.name)'s age is \(person2.age)")
// prints "Jim's age is 32"
```

Often times, tuples are constant. They're basically just containers for data, and that data doesn't generally change once a tuple has been created. But now you know that you _can_ change the elements if you want to.

## A Final Note

Tuples are a fairly simple data structure, but you won't see them a whole lot in Swift programming. Usually if you want to group multiple values together, there are better data structures to use (such as classes, which you will learn about soon). They are occasionally used in functions like `downloadImage(atURL:)` to both return a boolean indicating success or failure _and_ another value. Swift's standard library uses them from time to time, but not often. They're important to know about, but you'll soon learn about better ways to handle the problem addressed by tuples.

They _are_ often used when iterating over dictionaries. Dictionaries associate a _key_ with a _value_, and when iterating over a dictionary, you get back a tuple describing this key/value pair. You'll learn about dictionaries in a future lesson, and you may find it useful to refer back to this lesson when working with a dictionary's key/value tuples.

<a href='https://learn.co/lessons/Tuples' data-visibility='hidden'>View this lesson on Learn.co</a>
