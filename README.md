# Conditionals

## Objectives

1. Learn how `BOOL`s are used in `if()` statements.
2. See how a switch block is built with `if()`, `else if()`, and `else` statements.
3. Learn about using `!` ("the negation operator").

#### Advanced

4. Learn the use of the logical operators `&&` ("AND") and `||` ("OR").

## Conditionals

Computers, at their heart, are logic machines. Binary arithmetic is accomplished using various arrangements of logic gates to perform calculations. 

**Shameless plug:** *Read [Mark's blog post](https://medium.com/@MarkEdwardMurray/binary-operations-and-xor-you-9417a5dc275d) for an introduction to how logic gates are employed in computer operations.* 

In programming Objective-C, the primary way that customized logic gates are utilized is through the use of `if()`, `else if()`, and `else` statements.

## The `if()`-statement

An `if()` statement is exactly that: a function which runs a designated block of code **only if** a condition (or set of conditions) is met. All `if()`-statements evaluate the contents of their parentheticals ***as a boolean***. As we know from the previous reading, a `BOOL` can be either true or false, represented as `YES` or `NO` in Objective-C.

An `if`-statement is structured like this:

```objc
if (someConditionIsTrue) {
    // then run this code
}
```

Implementing one can look like:

```objc
if (3 > 2) {
    NSLog(@"Three is greater than two.");
}
```
They're pretty straight-forward.

### The `else`-statement

An `else`-statement may (and may *only*) follow an `if()`-statement and will only run if the `if()`-statement evaluates as false (`NO`). This is a quick way of creating an either-or behavior.

A common use example of this is in validating a password:

```objc
NSString *savedPassword   = @"p@ssw0rd";
NSString *enteredPassword = @"password";

if ([enteredPassword isEqualToString:savedPassword]) {
    NSLog(@"Welcome! You've got mail!");
} else {
    NSLog(@"Incorrect password.");
}
```
This will print: `Incorrect password.`.

The `else`-statement can be considered the "**default**" behavior, since it will run for any case **not** detected by a preceding `if()`- or `else if()`-statement.

### The `else if()`-statement

If you wish to present any additional cases separate from the first case, but not the default case, then the `else if()`-statement can be employed. An `else if()`-statement will only get checked if **all** of the conditionals before it fail, **and** its own conditional statement passes. A series of `else if()`-statements essentially builds a switch case.

```objc
NSInteger selection = 3;

if (selection == 1) {
    NSLog(@"You have selected option 1.");
} else if (selection == 2) {
    NSLog(@"You have selected option 2.");
} else if (selection == 3) {
    NSLog(@"You have selected option 3.");
} else {
    NSLog(@"Please select a valid option.");
}
```

**Note:** *There is a* `switch` *case function that Objective-C inherits as a C language function. You should avoid using it within the scope of this course.*

### Avoid Direct Comparisons to `YES`

You may have wondered, if an `if()`-statement's conditional takes a `BOOL` value, then how are the provided examples able to pass in variables of other types without getting errors? The answer is because `BOOL` evaluates anything that is **not zero or `nil`** to `YES`, and `YES` is equivalent to the integer value `1`. However, a variable which is evaluated as `BOOL` can result to `YES` without actually equalling `YES`. 

```objc
// bad example

NSInteger answer = 42;

if (answer == YES) {
    NSLog(@"The answer to the ultimate question");
    NSLog(@"of life, the universe, and everything");
    NSLog(@"is %li.", answer);
}
```
This, counter-intuitively, will not print anything at all. Don't panic! Instead, simply submit the variable itself into the `if()`-statement's conditional:

```objc 
// good example

NSInteger answer = 42

if (answer) {
    NSLog(@"The answer to the ultimate question");
    NSLog(@"of life, the universe, and everything");
    NSLog(@"is %li.", answer);
}
```
This will print: 

```
The answer to the ultimate question 
of life, the universe, and everything 
is 42.
```

### Check For Existence

Similar to the example above, you may see:

```objc
if (username) {
    NSLog(@"Welcome, %@. You've got mail!", username);
}
```
This `if()`-statement is set up to only print its customized welcome message if a variable named `username` has been previously created. If `NSString *username = @"Mark";` has been declared and defined already, then this check will print: `Welcome, Mark. You've got mail!`.

### The Negation Operator (`!`)

No, it's not an exclamation point—that's just the name of the typed character. This symbol in our current context is called "the negation operator". It acts to invert a `BOOL`, making a `YES` into a `NO`, or a `NO` into a `YES`.

```objc
BOOL gonnaGiveYouUp = NO;

if (!gonnaGiveYouUp) {
   NSLog(@"We're no strangers to love.");
}
```
This code snippet just Rick-Rolled you.

Just as in checking whether an object exists, we can check if an object *doesn't* exist:

```objc
if (!username) {
   NSLog(@"Please log in.");
}
```
This will check if our user has logged in before, and if not, it will print `Please log in.`.

## Advanced

### Combining Conditionals

When processing logic, there are several ways that multiple conditions can be handled together by using the keywords `AND`, `OR`, and `NOT`. In Objective-C, these logical operators are represented by `&&` ("double-ampersand"), `||` ("double-pipe"), and `!` ("the negation operator") respectively.

**Note:** *On the QWERTY keyboard layout, the* `|` *("pipe") symbol is the* `shift` *case on the backslash* `\` *key.*

| Symbol | Operation | Description |
|:------:|:---------:|:------------|
| `&&`   |  AND      | Passes only if **both** conditionals are true. |
| `||`   |  OR       | Passes if **either** conditional is true. |
| `!`    |  NOT      | Passes if the **inverse** of the conditional is true (if the conditional is false). |

**Note:** *The single-ampersand* `&` *and single-pipe* `|` *are "bitwise operators" inherited from C. Don't use them—they'll behave in ways you don't expect.*

Any `BOOL` can be defined as the result of evaluating combined conditionals:

| Condition A | Condition B | = | AND Result | OR Result |
|:-----------:|:-----------:|:-:|:----------:|:---------:|
| `NO`        | `NO`        | = | `NO`       | `NO`      |
| `NO`        | `YES`       | = | `NO`       | `YES`     |
| `YES`       | `NO`        | = | `NO`       | `YES`     |
| `YES`       | `YES`       | = | `YES`      | `YES`     |

In code, these can look like:

```objc
BOOL isTrue = YES;
BOOL isFalse = NO;

if (isFalse && isTrue) {
    // will not run.
}
if (isTrue && isTrue) {
    // will run.
}

if (isFalse || isTrue) {
    // will run.
}
if (isFalse || isFalse) {
    // will not run.
}
```

The usage of these logical operators primarily serves to reduce nested conditionals:

```objc
if (isTrue) {
    if (isAlsoTrue) {
        if (mayBeFalse) {
            // action A
        } else if (mayAlsoBeFalse) {
            // action A
        } else {
            // action B
        }
    }
}
```
Notice that arrowhead shape? It's considered bad practice to nest code any more than three indentations deep. That's because it gets difficult to read. However, we can actually represent this same logical structure in a simpler manner:

```objc
if (isTrue && isAlsoTrue) {
    if (mayBeFalse || mayAlsoBeFalse) {
        // action A
    } else {
        // action B
    }
}
```

For a complete list of all the operators in Objective-C, take a look at [Tutorial Point's](http://www.tutorialspoint.com/objective_c/objective_c_operators.htm) page on Objective-C operators.
