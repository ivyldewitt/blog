---
#disqusIdentifier: ivApCQ1Kop
title: "Ten Minutes Of Go"
date: 2017-07-30T19:11:03-04:00
categories:
- lifeintech
tags:
- codenewbies
- golang
- codechronicles
keywords:
- tech
thumbnailImagePosition: left
thumbnailImage: https://res.cloudinary.com/dgyz97es2/image/upload/v1501456688/mpho-mojapelo-109897_hxcqfj.jpg
coverImage: https://res.cloudinary.com/dgyz97es2/image/upload/v1501456688/mpho-mojapelo-109897_hxcqfj.jpg
metaAlignment: center
---

It's probably no secret by now that I am a big fan of Go (also known as Golang), an open source programming language that is known for its speed and efficiency. As we move towards [Go 2](https://blog.golang.org/toward-go2) and the eventual nuances and challenges that will come with its newest iteration, I want to take a few minutes to talk about what I think makes Go so special.

<!--more-->

{{< figure src="https://res.cloudinary.com/dgyz97es2/image/upload/v1501537076/gophercolor_p2yfmh.png" title="The Go Gopher: Courtesy of Renee French" >}}

# Origins of Go

Go gained traction partly because it's credentials. It was created by Google, and more specifically by three well-known programers:

* **Rob Pike:** Known for his work on Unix at Bell Labs, and his assistance with creating Plan 9, the Limbo programming language, and a *minor, little known* encoding system called UTF-8.
* **Robert Griesemer:** Studied under the creator of the Pascal programming language, which Go takes [some inspiration](https://golang.org/doc/faq#ancestors) from.
* **Ken Thompson:** Another Bell Labs alum, who was responsible for designing the original Unix operating system. Additionally, he invented the B programming language which was - you guessed it - the predecessor to the gargantuan language known as C.



{{< youtube rKnDgT73v8s >}}



#### Above: The Original Intro to Go from Google Tech Talks on 11/11/09.

The language debuted on November 10, 2009, with the intention of solving some of the following issues:

* Systems programming with existing languages had become confusing and difficult - partly due to the number of languages to choose from, and also partly due to the issues with the languages themselves.
* There were constant tradeoffs between efficient compilation, efficient execution, or ease of programming.
* Cores cores cores! As technology has evolved, we now have multicore computers. Due to how recent this development is, most modern languages aren't designed with multicore computing in mind.


# So what is it that makes Go so special?

In the Go FAQ, the developers have the following to say about why they thought it was worth creating an entirely new language in Go:

>"Go is an attempt to combine the ease of programming of an interpreted, dynamically typed language with the efficiency and safety of a statically typed, compiled language. It also aims to be modern, with support for networked and multicore computing. Finally, working with Go is intended to be fast: it should take at most a few seconds to build a large executable on a single computer. To meet these goals required addressing a number of linguistic issues: an expressive but lightweight type system; concurrency and garbage collection; rigid dependency specification; and so on. These cannot be addressed well by libraries or tools; a new language was called for."

From someone coming from a mostly JavaScript heavy background with a bit of Python, Go definitely felt like taking a cross-country trip - lots of new sights, new landmarks, and tons of new mistakes to make. Now that I've been working with Go for a few months, here's what I summarize as the core benefits of Go:

#### Compiled language

Go is a [complied language](https://en.wikipedia.org/wiki/Compiled_language) along the likes of C, Java, Pascal and more modern languages like Rust. Compiled languages are converted directly to machine code that can be read directly by the computer, instead of an interpreted language such as JavaScript. Go's compiler leads to it being a very fast, performant language.

#### Error Checking

While this could technically go under the compiled section, I think it's worth it's own shout-out. That said, error checking in Go is neat, pristine, and arguably does wonders to improve your own debugging skills in my opinion. As one of my favorite Go teachers, [Todd McLeod](https://twitter.com/Todd_McLeod) says:

>"Go suffers no fools"

I warn you, that is not a joke at all. Go will tell you if you declared a variable and didn't use it, if you're mismatching types (coming from JavaScript this was especially painful to learn) and subtly hint that you added but didn't use a package. Go rarely allows for sloppy code, and while it can be difficult at times it does force you to be a more attentive programmer.


#### Concurrency

In some respects, you could argue that concurrency is the core of what makes Go so successful. With modern computing, concurrency is crucial to using multicore machines running web servers with multiple clients. Due to how often that type of computing environment is used at Google, it's no wonder why Go was made to handle it.

I won't explain the full details of concurrency here, but in short it is the expression of  multiple copies of a program being run at the same time, and during execution the copies of the program are communicating with each other. Think of it as a baton pass - two runners are moving alongside each other, and doing handoffs at specific intervals. Go utilizes concurrency through channels and go routines, which allow for simple and easy communication between running tasks.


#### Simplicity

With everything I've added so far, you might be thinking: *Go seems unreasonably difficult to learn.*

I want to be sincere in saying that **Go is simple**. Deceptively so, even. In my opinion, one of the nice things about Go's error checking is that it allows for very clean, readable code. Go has a robust standard library, and is overall very simple to learn. One of the neat things about Go is that it has many of the features within its standard library that other languages use frameworks for - most notably its net/http package for creating web servers.

#### So what does Go look like?

Glad you asked! If you're familiar with C-like languages (C++, Java, etc.) Go most likely looks rather familiar. While there's a lot of intricacies to the setup of Go - see [How to write Go code](https://golang.org/doc/code.html) for starters - here's what a simple Palindrome program looks like:

```go
package main

import (
	"fmt"
	"strings"
)


func main() {
	p1 := palindrome("madam")
	p2 := palindrome("Eye")
	p3 := palindrome("dog")
	fmt.Println(p1, p2, p3)
}

func palindrome(st string) string {
	s := strings.ToLower(st)
	r := reverseStrings(s)
	if s == r {
		return r + ": is a palindrome! =)"
	}
	return r + ": is not a palindrome! =("

}
func reverseStrings(s string) string {
	splitting := []rune(s)
	for i, j := 0, len(splitting)-1; i < j; i, j = i+1, j-1 {
		splitting[i], splitting[j] = splitting[j], splitting[i]
	}
	return string(splitting)
}
```
*Author's Note: Smiley faces are all mine.*

To start, we import the packages ```fmt``` and ```strings``` as we'll need some of the functions within those packages to print to standout output and manipulate our strings, respectively. In the ```reverseStrings()``` function, we split the string into runes (*runes are integer values mapped to their unicode characters*) reverse it via a for loop, then convert it back into a string.

The ```palindrome()``` function is much simpler - we take in the string, convert it to lowercase, and then perform the ```reverseStrings``` function. We then compare the lowercase string to the reversed - string, and return whether it is a palindrome. We then run a few tests in ```main()``` and print the output.

You can play around with this code at the Go Playground [here](https://play.golang.org/p/LQbaaoJH3g).

#### How do I get started with Go?

To get started with Go, check out [A Tour Of Go](https://tour.golang.org/welcome/1) on the main language site, as it's a nice intro to the basics without the hassle of downloading Go. One of my personal favorite resources is [Go By Example](https://gobyexample.com/), which outlines basic to advanced concepts with full program examples, including URL parsing. For books, I recommend [Introducing Go](https://www.amazon.com/gp/product/1491941952/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1491941952&linkCode=as2&tag=yotomc-20&linkId=QRK7HPHBXX5E4BTB) and [The Go Programming Language](https://www.amazon.com/gp/product/0134190440/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0134190440&linkCode=as2&tag=httptwitco08e-20&linkId=ETDSVP5UBIOEKWMD). The latter is a bit more advanced, but serves as a great reference book. Lastly, where would I be if I didn't recommend my favorite video tutorial? If you're like me and video learning provides a more comprehensive and interactive learning experience than books, I can't stress enough on [Learn How To Code](https://greatercommons.com/learn/5098183625539584) by Todd McLeod. It's a great intro to programming in general, but definitely to Go.

In conclusion, Go shines with concurrency, but has a lot of features that make it a fun and fast language to learn. Plus, the mascot is awesome:

{{< tweet 437395572081688576 >}}

## Reference Links:

[Go at Google](https://talks.golang.org/2012/splash.article#TOC_13.)

[Why Go?](https://hackernoon.com/why-go-ef8850dc5f3c)

[Benefits of Programming with Go](https://www.pluralsight.com/blog/software-development/golang-get-started)

[Why I program with Go](https://tech.t9i.in/2013/01/05/why-program-in-go/)

[Go's Error Handling is Elegant](https://davidnix.io/post/error-handling-in-go/)

[Let's Go: Golang Concurrency](https://code.tutsplus.com/series/lets-go-golang-concurrency--cms-1087)

{{% unsplashcredit link="https://unsplash.com/@mpho_mojapelo?utm_medium=referral&amp;utm_campaign=photographer-credit&amp;utm_content=creditBadge" title="Mpho Mojapelo"%}}
