---
layout: post
title:  "Anatomy of a C# class"
date:   2023-06-11 22:08:49 +0800
categories: C# basics
---
C# is an object oriented language. This means that everything is an object.
An object is defined in a class. C# allows multiple classes in one file, but
generally, the file has the same name as the class it contains.

So a basic C# class, in a file looks like this. The file would be saved as Hello.cs

{% highlight csharp %}
public class Hello
{
  ...
}
{% endhighlight %}


Once we have the class, we can add its fields. Fields can also be called class variables.
Fields are the data that a class needs o do its jobs. Fields are declared just like any other variable.
The difference is that they are **WITHIN** the curly braces of the class but **OUTSIDE** any methods.
Class variables are accessible within the methods of the class.

Remember that variables are declared as

  <type> <name> <optional assignment>;

See the following examples:
{% highlight csharp %}
public class Square
{
  int sideLength;
}

public class Rectangle
{
  int width;
  int height
}

public class Player
{
  int hitPoints = 10;
  int xPosition = 0;
  int yPosition = 0;
}
{% endhighlight %}


A class can have many methods, but there are a few special types of methods.
One of these is the Main method. When a class has a main method, it can be run
as a command line application. Command line applications can write and read
basic text. When a command line application is run, it's Main method is called.
So any code in the Main method is executed

{% highlight csharp %}
public class Hello
{
    public static void Main()
    {
        System.Console.WriteLine("Goodbye, World!");
    }
}
{% endhighlight %}

