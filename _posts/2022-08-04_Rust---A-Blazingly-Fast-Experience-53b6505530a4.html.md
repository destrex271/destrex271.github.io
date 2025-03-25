Rust — A Blazingly Fast Experience

Rust — A Blazingly Fast Experience
==================================

Throughout the years multiple programming languages have come and gone. Some of them has such a massive effect that multiple languages…

---

### Rust — A *Blazingly Fast* Experience

![](https://cdn-images-1.medium.com/max/800/1*jExu-5oF195FbKArTExBJg.png)

Throughout the years multiple programming languages have come and gone. Some of them had such a massive effect that multiple languages were based off of them while at the same time some other languages were soon forgotten.

Some of the most influential languages include C, also known as the mother of all modern languages, its most famous derivative C++, Java, C# and many more. The introduction of C in 1972 revolutionized the way we could program computers, C++ enriched this experience by introducing Object Oriented Paradigms in C but everything comes to a certain end, doesn’t it?

I am not implying that the user base for C++ is decreasing but the lack of updates in the language and sometime its “quirks” have forced many companies to switch there code bases from C++ to other modern languages. For example [Go](https://go.dev/) and [Carbon-Lang](https://github.com/carbon-language/carbon-lang) have been developed by Google for the purpose to replace their existing C++ code base.

One of the most promising candidates among these languages include [Rust](https://www.rust-lang.org/). Rust started as a personal project by an employee named Graydon Hoare at Mozilla which was later sponsored by the company in 2009. And as of now the father of Linux, Linus Torvalds, announced in the Open Source Summit 2022, organized in Austin, Texas, that he is “cautiously optimistic” about bringing rust into the next major release of the [Linux Kernel](https://github.com/torvalds/linux)(most probably 5.20).

### Why Rust?

There are a plethora of programming languages that could have been considered for the same tasks that rust performs but there are some features that set it apart:

#### 1. Performance

Rust is one of the fastest languages till date with Go-lang being the only competitor. Rust is *blazingly* fast and memory efficient. It does not include a garbage collector which reduces the overhead processing cost for these operations.

#### **2. Reliability**

The Ownership model of Rust ensures that the programmer is not able to cause any problems with the memory management part of their application. Although the concept of ownership and borrowing might intimidate you at first but once you get a hold of them you can write efficient programs in rust.

#### 3. Versatile and Cross-platform

Rust can be used to write various type of applications that can run on a range of devices. Some of the fields include Lower Level programming(“Like writing drivers etc..”), WebAssembly, Backend Developement etc. Since Rust is powered by the LLVM Compiler Infrastructure, it can easily run on embedded devices too.

### My Journey

I started out with rust just a month ago and quickly realized that Rust was actually a really powerful language.

Although some concepts were pretty weird. For example, some features that we take for granted in other high level languages like python and javascript were absent.

#### Ownership & Borrowing

First lets talk about the concept of ownership and borrowing. Lets take this piece of Rust code as an example:

So as you can see above if we try to access the variable x after passing it to the print function the program will “panic”, which is the same as Exceptions in Python and Java. This happens because in rust all the “complex” data types like strings are stored in a very different manner as compared to other languages.

![](https://cdn-images-1.medium.com/max/800/1*JLZunsObbnVAae0Rbusjyw.png)

As you can see in the figure above the values to these variables are stored in the heap while the pointer to that particular location in the heap memory and other properties like length are stored in the stack. So lets say if another variable is assigned the value of a variable x which contains a string and then if we drop x, then the value stored in the heap would also be removed and therefore the second variable would point to an empty location, resulting in a [*Dangling Pointer*](https://en.wikipedia.org/wiki/Dangling_pointer).

This causes a lot of issues at runtime and therefore to tackle this the ownership system was setup which passes the ownership of the entire value all together. For example:

To avoid issues like this we “borrow” the value by assigning or passing a reference to that variable instead of transferring its ownership. For example:

This example clearly shows how we can pass a reference to a variable by using the ampersand(&) operator(*Just like C, right?Well not that much).*

You can also send a mutable reference which means you can alter the value of the reference passed but you need to remember that you can only pass a single mutable reference or multiple immutable references.

### Where are my Classes🤯?

Yup, that was my reaction when I learnt that there are no classes in Rust. Although Rust supports high levels of abstraction but that does not imply that it has the concept of classes builtin*(it used to but now it does not)*, but honestly after diving in a little deeper I realized that we don’t need them here, because we already have ***structs*** and ***traits*** to solve all our problems.

#### Structs

Structs in rust are of three types:

1. Named Structs *(Standard C-type structs)*
2. Tuple Structs *(struct Point(i32, i32, i32);)*
3. Unit Structs *(struct Test;)*

For Eg:

Out of this we usually use the first two. Structs can be used to create user defined data types containing multiple primitive data types. This compensates for storing our data members/object properties as we do in a class but what about the member methods😕?

For that we have ***Traits***.

#### Traits

Traits are used to define a functionality that can be shared by multiple types.We can define a specific function and that function always takes a reference to the type associated. Lets take a look at an example to understand traits better:

We can easily define a trait using the ***trait*** keyword.

As you can see we use the ***impl*** *(which stands for implement)* keyword to associate a trait with a User Defined Data Type.

> **Note:** The ***for*** keyword used here has a different functionality from the one we use in a for loop, although the keyword remains the same.

### Conclusion

Well these were some of the things that I learnt while I was learning the basics of Rust. If you notice any discrepancy in the data mentioned above feel free to point them out in the comment section.

To conclude, I would only say that Rust is an amazing programming language and even if you won’t use it in your job it would be an amazing experience to learn such a beautiful approach to writing programs.

Do checkout the official [*Rust-Lang Book*](https://doc.rust-lang.org/book/). You can also checkout my [*Github*](https://github.com/destrex271/rustLang)repository which contains a set of basic Rust programs, some of which have been used as examples in this Blogpost.

More articles regarding Rust and other fun pieces of Technology will be coming up soon, **so stay tuned!**

By [Akshat Jaimini](https://medium.com/@destrex271) on [August 4, 2022](https://medium.com/p/53b6505530a4).

[Canonical link](https://medium.com/@destrex271/rust-a-blazingly-fast-experience-53b6505530a4)

Exported from [Medium](https://medium.com) on March 25, 2025.