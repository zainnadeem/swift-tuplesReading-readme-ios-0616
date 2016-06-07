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

* Lets go back to to the original problem now. If we were to call on this function, we know through its return type that we're to expet back a tuple of type (`Bool`, `String`). Lets try it out:

![downloadImage](http://i.imgur.com/gatoOEI.png?1)

* Here we called on the function `downloadImageAtURL()` and received back a tuple of type (`Bool`, `String`) and stored that inside of a constant named `imageDownload`.
* So now we can access these two values within the `imageDownload` variable to see if our image succesfully downloaded and if not, then see what the problem is.

```swift
let imageDownload = downloadImageAtURL("http://www.apple.com/iPhone7")

if imageDownload.success {
    // image download was a success
    // display the new image to the user
} else {
    // image download DID NOT SUCCEED
    // display the error message to the user
    
    print(imageDownload.errorMessage)
}

// prints "Image no longer exists at that URL"
```

* In this code above, we're checking to see if the image we're attempting to download was successful by checking the `Bool` value stored in the `imageDownload` constant. If `imageDownload.success` is `true` **THEN** display the image to the user **ELSE** (if the value of `imageDownload.success` is `false`) then display the error message to the user. We're also printing the message to the console by passing in `imageDownload.errorMessage` to the `print()` function as `imageDownload.errorMessage` is of type `String`.

* As you progress through this course, you will not see tuples used that often. Tuples (according to Apple) are particularly useful as the return values of functions (as we showed you above). By returning a tuple with two distinct values, each of a different type, the function provides more useful information about its outcome than if it could only return a single value of a single type.
* You will soon learn about dictoinaries in Swift. When you iterate over a dictionary in swift, each item in the dictionary is returned as a `(key, value)` tuple which you can decompose JUST like we did above. So in your future readings about dictionaries, come back to this reading should you have any questions in how to access the various values within the tuple variable.

<a href='https://learn.co/lessons/Tuples' data-visibility='hidden'>View this lesson on Learn.co</a>
