---
layout: post
title:  "C# If Else"
date:   2023-06-09 22:08:49 +0800
categories: C# basics
---

If Else statements (also known as conditionals) have this format

if (condition1) {
  // true code
} else if (condition2) {
  // false code
} else {

}

The *conditions* are bits of code that evaluate to true or false

The code in the curly braces after the *if* is executed if the condition is true.
If we have other things to test, we can add else if
The code after the *else* is executed if everything else is false.

If you have only one line of code that needs to be executed after an if, else if or else,
then the curly braces around it are optional.  This is a shortening, for convenince,
like saying *can't* instead of *can not*.

{% highlight csharp %}
if (age >= 13) // No curly braces needed
    Console.WriteLine("You can see a P13 movie");
else { // 2 lines of code, must have curly braces
    Console.WriteLine("You can't see this movie'");
    Console.WriteLine("Quick call the parents!");
}
{% endhighlight %}

Both *else* and *else if* are **optional**

Examples:

{% highlight csharp %}
if (hasCake == true) // An if without else or else if
    Console.WriteLine("You can eat cake");

if (age >= 18) { // An if with only an else if
    Console.WriteLine("You can see any movie");
    return;
} else if (age >= 13) {
    Console.WriteLine("You can watch P13 movies");
    return;
} else 
    Console.WriteLine("You can watch U movies");

if (age >= 18) { // An if with only an else
    Console.WriteLine("You can watch any movie");
    return;
} else {
    Console.WriteLine("Please get your parents to come with you");
}
{% endhighlight %}
