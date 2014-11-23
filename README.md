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
```

## Doing Something With Conditions

So now we know how to compare values, how do we use these comparisons do actually *do* something? The answer is with an `if` statement! Let's look at this code:

```objc
if (num < 5)
{
  NSLog(@"It's less than five");
}
```

You can read this code as "if num is less than 5, then log I's less than five". See how that is sorta english-y? As it is right now, if `num` isn't less than 5 then we just skip over the `NSLog` and move on with the code. What if we want to do something else if the `num` is greater then 5? Well, that sounds like an `else` statement!

```objc
if (num <5)
{
  NSLog(@"It's less than five");
} else
{
  NSLog(@"It's greater then or equal to five");
}
```

An `else` statement must be paired with an `if` statement, but it is the code that is run if the condition returns `NO`. These are a convenient "catch-all", but what if we want a bit more granularity in our statements? What if we want to do different things as a sort of waterfall of decisions. So if a number is less than 5 log "It's less than five", else if it's less than 10 log "It's greater than 5, but less than 10", if none of these are true then print "It's greater than 10". This is what that looks like expressed in code:

```objc
if (num < 5)
{
  NSLog(@"It's less than five");
} else if (num < 10)
{
  NSLog(@"It's greater than 5, but less than 5");  
} else 
{
  NSLog(@"It's greater than 10");
}
```

You can even have as many `else if` statements as you'd like, but you can only have one `else` statement per `if` chain.

## Looping

So now we can choose what we want to do based on some conditions. Now let's choose how many times we want do it. Humans stink at doing the exact same thing over and over, thankfully computers are really incredibly good at it. Loops usually take the form of a what's called a `for` loop. For loops have three different sections. These sections describe how the loop should behave. Let's look at a `for` loop that will print out a line from Edgar Allen's Poem ["Bells"](http://www.poets.org/poetsorg/poem/bells): "From the bells, bells, bells, bells, Bells, bells, bells".

```objc
NSLog(@"From the");
for (NSInteger i=0;i<7;i++)
{
  NSLog(@"bells,");
}
```

The three sections in the `for` line explain three different facets of the loop. The first section (`NSInteger i=0`) creates a variable named `i` that starts at 0. This will be our "counter". The second section (`i<7`) is checked before every iteration of the loop, as long as that condition returns `YES`, the loop will begin again. The third section (`i++`) is shorthand for `i=i+1`. This means at the *end* of each loop iteration it increases the `i` variable by one. If we look at the line of text we are trying to write, we want the fifth "bells" to be capitalized. How would we do that in code? We can just look at our counter variable and see which iteration we are on!

```objc
NSLog(@"From the");
for (NSInteger i=0;i<7;i++)
{
  if (i==4)
  {
    NSLog (@"Bells, ");
  }else
  {
    NSLog(@"bells, ");
  }
}
```

Why did I check at 4? Well we started counting at 0 so 0,1,2,3,4. 4 is the fifth time running through this code. There are two other types of loops, [while](http://www.techotopia.com/index.php/Objective-C_Looping_with_do_and_while_Statements#The_Objective-C_while_Loop) and [do-while](http://www.techotopia.com/index.php/Objective-C_Looping_with_do_and_while_Statements#Objective-C_do_..._while_loops) loops but they aren't used very often. That's really all there is to loops!
