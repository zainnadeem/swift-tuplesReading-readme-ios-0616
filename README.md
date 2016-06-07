# Tuples

<img src="http://i.imgur.com/gMMSTqF.jpg?1" alt="Drawing" style="width: 200px;"/>  


> A day without sunshine is like, you know, night. 

## Learning Objectives - The student should be able to..

* Blah blah blah\\\\\

## What the student can do at this point 

* More stuff

## Outline / Notes

*  What if we wanted to group multiple values into a single compound value. What does that even mean?
* When programming, there are times when you're creating a function where you want to return multiple values. For instance, if we were creating a function like this:

```swift
func downloadImageAtURL(url: String) -> Bool {
    
    // downloading image..
    
    // image download was a success
    
    return true
}
```

* Easy enough, considering that instead of comments we have actual code that would go up to a server and download our image, but what if... there was a problem downloading this image and we want to return false if there was an issue. Well, that's easy enough:

```swift
func downloadImageAtURL(url: String) -> Bool {
    
    // downloading image..
    
    // ERROR!. Error Message: "Image no longer exists at that URL".
    
    // if an error, we will return false, else we will return true
    
    return false
}
```

* But we have a problem..

![Baby Problem](https://media.giphy.com/media/9TtwPvGwQB8QM/giphy.gif)

* That error message is useful to us! We want to know why the image failed to download. We might want to display this information to the user of our app... telling them "Hey! This image didn't download for this specific reason" then supply them with the reason. Or.. we might have a button that allows the user to try downloading the image if there was a problem. But... with an error message like "This image doesn't exist at this location, we might then disable the button which will not allow the user to make an attempt to download the image.

* So we're in a position where we want to send multiple values back in this function. If there was an error downloading the image, we would like to send back two values. One of type `Bool` indicating the success or failure of the download and one of type `String` which represents the error message.

* How you solve that problem in Swift is with `Tuple`'s. A funny word no doubt. I suggest watching this [Video](https://www.youtube.com/watch?v=7fTVCQRQYXk) to see how you pronounce it.

![Huh](https://media.giphy.com/media/gKsJUddjnpPG0/giphy.gif)

```swift
func downloadImageAtURL(url: String) -> (success: Bool, errorMessage: String) {
    
    // downloading image..
    
    // ERROR!. Error Message: "Image no longer exists at that URL".
    
    return (false, "Image no longer exists at that URL")
}
```

* We just created our first `Tuple`.
* Notice the difference in the return type. It now looks almost identical to a function you made that takes in multiple arguments, except without the keyword `func` and the name of your function. `(success: Bool, errorMessage: String)` is **NOT** a function though, this is a `Tuple` and it's just like any other type you've worked with so far.
* You can think of a tuple as being a container of other types except it represents one value that could be stored inside of a variable. Well what does that mean?

![Tuple](http://i.imgur.com/aUkUJnF.png?1)

* Here we declared a constant named 'person' to be of type (`String`, `Int`) which is a tuple. The `person` variable is storing two values, it has two pieces of information in it, a name (of type `String`) and an age (of type `Int`). How do we access that info?

* If you were to open a playground file and include that code above creating the person variable you would see the following. On the line(s) below where you declared the `person` variable, if you were to type out `person` followed by a `.` you would see the following two options (which would auto-complete for you if selected). 

![TupleMembers](http://i.imgur.com/4r9FimF.png?1)

* We know by reading this, that by accessing age in this manner, a value of type `Int` will be returned to us (which we could store in another variable or just print to the console).

* Lets try this out:

```swift
let ageOfPerson = person.age   // 30
let nameOfPerson = person.name // "Jim"

print("My name is \(nameOfPerson) and I am \(ageOfPerson) years old.")
// prints "My name is Jim and I am 30 years old."

print(person)
// prints "("Jim", 30)"
```

* You're starting to understand tuples.

![Jake](https://media.giphy.com/media/daUOBsa1OztxC/giphy.gif)

* **BUT** what if we wanted to change one of the two values in that `person` tuple we made above? Is this possible?

```swift
person.name = "Bran"
```

* Now, the name of person should be "Bran". Right? Think about this, should the complier **ALLOW** us to do this? What would disallow something like this to occur, considering we're about to **change** the value of this `person` constant to another value.
* If you recognized the problem being that we declared our `person` constant with `let` thus making it a constant, kudos! Let's create another tuple, but this time declaring it as a variable so we can change one of the values within it.

```swift
var friends = (best: "Bubblegum Princcess", worst: "Jake")
```

* But what if Finn has now become my new best friend.

```swift
friends.best = "Finn"

print("My best friend is \(friends.best) and my worst friend is \(friends.worst).")
// prints "My best friend is Finn and my worst friend is Jake."
```

*

<a href='https://learn.co/lessons/Tuples' data-visibility='hidden'>View this lesson on Learn.co</a>
