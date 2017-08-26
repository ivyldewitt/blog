---
disqusIdentifier: ivApCQ1Kop
title: "An Intro To Types In Go Part 1"
date: 2017-08-23T20:57:45-04:00
categories:
- lifeintech
tags:
- codenewbies
- golang
- javascript
- programmingconcepts
keywords:
- tech
- golang
- programmingconcepts
thumbnailImagePosition: left
thumbnailImage: https://firesidetech.files.wordpress.com/2017/08/leo-fosdal-113874.jpg
coverImage: https://firesidetech.files.wordpress.com/2017/08/leo-fosdal-113874.jpg
metaAlignment: center
---

Before Go, I had primarily programmed in JavaScript and Python which had the fun distinction of being dynamically typed languages. When I moved to Go, I hit two specific roadblocks: 1) not fully understanding the difference between dynamic vs static languages and 2) and honestly, why should I be concerned about the difference? So naturally, I decided to create a blog post about static vs dynamic languages, and what that means for Go newbies. 

<!--more-->

{{< figure src="https://firesidetech.files.wordpress.com/2017/08/chris-barbalis-177813.jpg" title="Building on your knowledge of programming fundamentals sometimes seems like building a skyscraper." >}}

## What is a type?

To start off, it’s useful to have a more comprehensive picture of what types actually are. For fun (well maybe my definition of fun), here’s the definition of types from Wikipedia:

>"“In computer science and computer programming, a data type or simply type is a classification of data which tells the compiler or interpreter how the programmer intends to use the data. Most programming languages support various types of data, for example: real, integer or Boolean. A Data type provides a set of values from which an expression (i.e. variable, function ...) may take its values. The type defines the operations that can be done on the data, the meaning of the data, and the way values of that type can be stored.“

[Source - Wikipedia](https://en.wikipedia.org/wiki/Data_type)

Breaking this down, I recommend thinking about types as containers, all holding a different category of data. I.e. in one category I can put strings, in another Booleans, and in a third arrays. A data type, either in a static or dynamic language simply states what segment/category this piece of data belongs to.
We’ll be covering the most common types in this section, including the following:

* **Primitive Types:** These are your building-block types as I like to call them. Most languages have some iteration of Booleans, integers, floats, and strings, though there may be some variation on the naming conventions and expanding on the numeric types especially.
* **Composite Types:** These are types that are composed of more than one data type. While again the terminology changes, the most common types are arrays, objects, etc.

As I mentioned before, some languages provide a wide variety of primitive and composite types. For example, along with bool, string, int, and float64, Go provides bytes and runes, which provide another set of useful tools for coding.
Now that you’ve gotten a decent overview of what types are, let’s take a look at the core differences of static vs dynamic typing.

## What is dynamic vs static typing?

The difference between static vs dynamic typing ultimate refers to at what point in the program are we verifying the logic of the types – also known as type checking.

To elaborate, Type Checking is the process of verifying and placing constraints on types in a program.  This can occur either at compile time (static typing) or runtime (dynamic checking). The purpose of type checking is to reduce the amount of type-related errors as much as possible, and in other words, ensure that if you’re program isn’t running as expected it’s not due to a type error.

One the reasons why statically typed languages are popular is that type checking at compile time allows for more swiftly executing code, as a result of the compiler knowing the specific data types being used and overall reduces the need to repeat type checks every time the program is executed.

In contrast, dynamic typing will cause a program to report type errors at runtime, not compile time. Dynamic typing provides a number of benefits, including [dynamic dispatch](https://en.wikipedia.org/wiki/Dynamic_dispatch) & [metaprogramming](https://en.wikipedia.org/wiki/Metaprogramming). Additionally, even many static languages have some implementation of dynamic type checking – even Go uses a form of dynamic dispatch with interfaces.

Here’s also a Quora response that gives a brief, if generalized overview of the main differences between the two:

* **Dynamic:** slower to run, faster to write, confusing to debug
* **Static:** faster to run, slower to write, less prone to bugs

[Source](https://www.quora.com/What-are-the-differences-between-a-dynamic-programming-language-and-a-static-programming-language-Which-one-is-better-or-in-other-words-has-a-better-prospect)

## What’s the difference between static/dynamic and strong/weak typed languages?

Another common source of confusion is the difference between strong/weak typed languages and static/dynamic languages. This confusion typically occurs because a lot of static languages are also strongly typed languages, and vice-versa for weakly typed-dynamic languages.

At its core, weakly typed languages do not place restrictions on how data types can be mixed, while strongly typed languages place at least one restriction on how data types are mixed.

For example, let’s say we have a function ```concatCookies()``` – where we want to add a string and an integer together to tell how many cookies we have in our basket. In JavaScript, my function would look like the following:

```javascript
function concatCookies(num, str) {
    console.log('I have ' + num + ' of ' + str + ' cookies in my basket!');
}
var basketOfCookies = 25;

var cookies = 'molasses';

concatCookies(basketOfCookies, cookies);
```

[View in JSFiddle.](https://jsfiddle.net/g442fo6c/)

I’m able to compile a string and an integer and JavaScript, being the smart language that it is can immediately determine that while basketOfCookies is a number (or int), it can coerce the type to a string in order to print the full string to the console.

Go does not afford such luxuries. If I attempt to computer the following:

```go
package main

import (
    "fmt"
)

func main() {

    cookies := "Molasses"
    basketOfCookies := 25;
    fmt.Println(concatCookies(cookies, basketOfCookies))

}

func concatCookies(c string, b int) string {
    m := "I have " + b + " of " + c + " cookies in my basket!"
    return m

}
```

[View on the Go Playground.](https://play.golang.org/p/BNbAh3OcWy)

I get the following scary looking (but surprisingly straightforward) error:

```invalid operation: "I have " + b (mismatched types string and int)``` 

Go is very specific with its typing, and to complete this successfully I’ll actually need to import and entirely different package:

```go

package main

import (
    "fmt"
    "strconv"
)

func main() {

    cookies := "Molasses"
    basketOfCookies := 25;
    fmt.Println(concatCookies(cookies, basketOfCookies))
}

func concatCookies(c string, b int) string {
    m := "I have " + strconv.Itoa(b) + " of " + c + " cookies in my basket!"
    return m

}
```

[View on the Go Playground.](https://play.golang.org/p/bLCRpI49Zx)

We'll discuss this in more detail in another section - but note a few things here:

1. We imported a new package - strconv - in order to add another function that converts an int to a string.
2. In Go, we've explicity declared the types of our paramaters ```c string, b int``` and our return value ```string```. In JS, we declared our variables without any explicit type declarations and were on our merry way.

Overall, there’s a lot of benefits to both – some like the freedom & flexibility of weakly typed languages, while others like the constraints from strongly typed languages, but strong/weak typing refers to the restrictions on how data types can be mixed, versus static/dynamic type systems which focus on when the type itself is checked.

## Which one should I use/learn?

So, after a quick look into what static and dynamic types each bring to the programming table, you’re probably wondering which one you should start to program with.

The answer….. is that it’s most likely worth your time to learn both. At some point, you’re probably going to encounter both over your programming career, and both type systems have their own benefits and downsides. Moving from one type system to another can be confusing at times, and I hope this post cleared up a bit of that haziness for you.

As always, I leave you with a programming quote:

{{< tweet 832014603391553536 >}}

## Reference Links:

[Quora: Strong vs Weakly Typed Languages](https://www.quora.com/What-are-the-differences-between-strongly-typed-and-weakly-typed-languages)

[Programming Concepts: Static vs Dynamic Checking](https://thesocietea.org/2015/11/programming-concepts-static-vs-dynamic-type-checking/)

[Golang FAQ](https://golang.org/doc/faq)

[Quora: Dynamic vs Static Languages](https://www.quora.com/What-are-the-differences-between-a-dynamic-programming-language-and-a-static-programming-language-Which-one-is-better-or-in-other-words-has-a-better-prospect)

{{% unsplashcredit link="https://unsplash.com/@fozzie?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge" title="Leo Fosdal"%}}
