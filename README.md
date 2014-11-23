# Looping and Conditionals

## Conditionals

Everything you have learned until now can *say* different things. For example with variables we can have the code:

```objc
NSString *studentName = @"James";
NSLog(@"His name is %@",studentName);
```

and this would print out a different greeting depending on what we put in the `studentName` variable. The problem with this is we can't *do* something different depending on that variable. This code would be a bit weird of the `studentName` was `@"Sally"`. If it's a woman's name then we should log out `@"Her name is Sally"`. Conditionals allow us to *do* something depending on some sort of comparison. So let's take a look at what types of conditions and comparisons we can do in Objective-C

### Comparisons and Conditions

In Objective-C there are two outcomes of type `BOOL` whenever you run a condition: `YES` or `NO`. It can't be both! When we log out these values, they get converted into `NSInteger` objects and will be logged as `1` for `YES` and `0` for `NO`.Let's take a look at a few comparisons, we are using the placeholder `%i` because we are logging the `NSInteger` value.

```objc
NSLog(@"%i", YES); // Logs 1
NSLog(@"%i",NO); // Logs 0
NSLog(@"%i", 5 < 8); // Logs 1
NSLog(@"%i", 4>=5); // Logs 0
NSLog(@"%i", 10 == 10) // Logs 1
```

As you can see, comparing `NSInteger` values is pretty simple. When we are comparing proper Objective-C objects (those with the `*`) we have to use a method though. The `==` sign will only compare if they are the *exact same object*, not just the same content. To compare `NSString` objects we use the `isEqualToString:` method, for other data types you can use the `isEqual` method. Let's take a look at that:

```objc
NSLog(@"%i", [@"joe" isEqualToString:@"joe"]); // Logs 1
NSLog(@"%i", [@"james" isEqualToString:@"James"]); //Logs 0
NSLog(@"%i", [@4 isEqual:@91]); //Logs 0
```

We can also combine multiple conditions. You combine conditions with either an "and" (`&&`) or and "or" (`||`). You use `&&` of you need both conditions to return `YES`. An `||` is used if you are ok with only one of the conditions returning `YES`. Let's say we wanted to check to see if a number was between 5 and 8. We can do that like this:

```objc
NSLog(@"%i", num >5 && num <8); // logs 1
```

But we can also check to see if a number is either less then 5 or greater that 30 like this:

```objc
NSLog(@"%i",num<5 || num>30); // logs 1

## Doing Something With Conditions


