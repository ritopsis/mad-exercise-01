# MAD - Exercise 01
## Tasks
* Watch the Kotlin Crashcourse Video in Moodle or complete the tutorials **[Introduction to programming in Kotlin](https://developer.android.com/courses/pathways/android-basics-compose-unit-1-pathway-1)** and **[Kotlin fundamentals](https://developer.android.com/courses/pathways/android-basics-compose-unit-2-pathway-1
)**.
* Answer the questions inside this Readme.md file and push it to your repository.
* Submit your coding solution of the Number Guessing Game inside the repository.
* Submit the link to your repository in Moodle.

## Questions
### Describe how Kotlin handles null safety. What are nullable types and non-null types in Kotlin? (0,5 points)

<span style="color:blue">Provide your answer here! </span>
> Describe how Kotlin handles null safety:
Kotlin uses syntactic rules to achieve null safety, so no accidental calls are made on potentially null variables.
Accessing a member of a null variable during an app’s runtime can cause the app to crash (runtime error).
Kotlin compiler forces a null check, a process of checking whether a variable could be null before it's accessed, for nullable types.
So In order to use a nullable value as its non-nullable type, you need to perform a null check explicitly.
The ?. operator in Kotlin prevents NullPointerException by returning null if a variable is null instead of accessing its member.
Also the == or != comparison operator in if/else statements can be used for null checks.
Another possibility is to provide a default value for when a nullable variable is null -> with the if/else expression or the ?: Elvis operator.
The ?: Elvis operator executes the expression before ?: if the variable isn't null or after ?: if it is null.
There is also the !! not-null operator which should only be used when you can be sure that the nullable variable will not be null else it may result in a NullPointerException.
> What are nullable types and non-null types in Kotlin?
In Kotlin, you can use null to indicate that there's no value associated with the variable.
Nullable types are variables that can be assigned null.
Non-null types are variables that can't be assigned null.
To declare nullable variables in Kotlin, you need to add a ? operator to the end of the type:
```kotlin 
// example code snippet
// following code will not work because favoriteActor is a non-null type String and therefore can't hold null!
var favoriteActor: String = "Sandra Oh"
favoriteActor = null // <- big no!!!
// to make favoriteActor a nullable type String, we have to add ? after String:
var favoriteActor: String? = "Sandra Oh"
favoriteActor = null // working :)
// safe call
fun main() {
    var favoriteActor: String? = null
    println(favoriteActor?.length) // output: null
}
// example for if/else check
var favoriteActor: String? = null
if(favoriteActor != null) { // if favoriteActor is not null than we can safely do favoriteActor.length!
    println("The number of characters in your favorite actor's name is ${favoriteActor.length}.")
} else { // else if it is null and we access favoriteActor.length -> NullPointerException so therefore:
    println("You didn't input a name.")
}
// example for elvis (add a default value if favoriteActor is null)
val lengthOfName = favoriteActor?.length ?: 0 // default value would be here 0.

```
>Source: https://developer.android.com/codelabs/basic-android-kotlin-compose-nullability#0

### What are lambda expressions and higher order functions in Kotlin? Why would you store a function inside a variable? (0,5 points)

<span style="color:blue">Provide your answer here!</span>

>In Kotlin lambda expressions are functions that can be created without having to declare them. 
They are useful for creating quick functions that can also be used in higher-order functions. 
Higher-order functions are functions that take other functions as parameters or return a function.
The main reason to store functions in variables is for flexibility, which allows changing behavior at runtime. 
This allows you to write more general code that can handle a variety of situations. 
It also enables you to pass around behavior in your program, making your code more flexible and reusable.
For example the code below:
In this case the behavior of the calculate function changes depending on whether the sum or multiplication lambda is passed to it.
```kotlin 
// example code snippet
// Simple Lambda-Expression
val sum: (Int, Int) -> Int = { a, b -> a + b }
val multiplication: (Int, Int) -> Int = { a, b -> a * b }
// Higher-order functions
fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int { return operation(a, b) }
```
>Source: https://developer.android.com/codelabs/basic-android-kotlin-compose-function-types-and-lambda#0

### Provide a solution for the following number guessing game inside `App.kt`. (3 points)

## Number Guessing Game in Kotlin
The game is a simple number guessing game. The task is to generate a random, max 9-digit, number. The number must **not contain repeating digits**. Valid digits are 1-9.
Ask the user to guess the max 9-digit number. The game is finished when the user guesses the correct digits in the correct order.
In each round, the user gets feedback about the number of correct digits and the number of correct digits in the correct position.
The output should be in the format "n:m", where "n" is the number of digits guessed correctly regardless of their position, 
and "m" is the number of digits guessed correctly at their correct position. Here are some examples:

This example shows the game flow with 4-digits to guess (the default argument)

Generated number: 8576
-	User input: 1234, Output: 0:0
-	User input: 5678, Output: 4:1
-	User input: 5555, Output: 1:1
-	User input: 3586, Output: 3:2
-	User input: 8576, Output: 4:4 -> user wins

Take a look into the provided code structure in `src/main/kotlin/App.kt`. Implement the following methods (lambda expressions):
- _playNumberGame(digitsToGuess: Int = 4)_ (1 point): The main game loop that handles user input and game state. Make use of _generateRandomNonRepeatingNumber_ and _checkUserInputAgainstGeneratedNumber_ here. This function also utilizes a default argument 
- _generateRandomNonRepeatingNumber_ (1 point): A lambda expression that generates a random number with non-repeating digits of a specified length.
- _checkUserInputAgainstGeneratedNumber_ (1 point): A lambda expression that compares the user's input against the generated number and provides feedback.

``CompareResult.kt`` This class is a data structure which helps with bundling the result of the comparison of the user input and the generated number. Look at the toSting() and use it in your output.

Run the project with `./gradlew run` and test your implementation with the provided tests in `src/test/kotlin/AppTest.kt` with `./gradlew test`.

# Project Structure
The project is structured into two main Kotlin files:

**App.kt**: Contains the main game logic and functions.

**AppTest.kt**: Contains unit tests for the various functions in App.kt.

