+++
title = "Tox"
description = "The Tox programming language"
in_search_index = true
date=2019-03-03

[taxonomies]
categories= ["rust","tox","vm"]
+++

I have been working on a programming langauge called Tox that is a statically based programming language that is written in Rust and is based on Lox. Lox is the programming language that you as a reader implement when going through [Crafting Interpreters](http://www.craftinginterpreters.com/contents.html). 

<!-- more -->
## Improvements

After finishing the crafting interpreters book you end up with a programming langauge that is dynamically typed. I generally have no problems with a dynamically typed programming language but one the first improvements that I made to Tox was to add a type system.

This resulted in Tox becoming like this :

```typescript
var foo:int = 10;

var bar:float = 10;

print foo + bar;

function foo(a:int,b:int) -> int {
    return a+b;
}
```

instead of 
```typescript
var foo= 10;

var bar= 10;

print foo + bar;

function foo(a,b) {
    return a+b;
}
```

## Type Inference + Generics

Whilst type systems are very useful I hated the fact that I had to write down the type for every single variable declaration which is pretty cumbersome and is one of my pet peeves with Java and C. After using Rust I discovered type inference and you know what they say, Once you have type inference you can never go back.

The algorithm that most programming languages use is algorithm W which is also known as Hindley Milner type inference. There are many papers that go through it and I've read through many implementations and blog posts on the topic. In the end  I decided to base my implementation on the one outlined within [Modern Compiler Implementation in ML](https://www.amazon.co.uk/Modern-Compiler-Implementation-Andrew-Appel-ebook/dp/B00D2WQAE8/ref=sr_1_1?s=books&ie=UTF8&qid=1551619462&sr=1-1&keywords=Modern+Compiler+Implementation+in++ml). The great thing about 
Hindley Milner type inference is that you also get polymorphism and with polymorphism you also get generics for free. Allowing you to write code like 

```rust
enum List<T> {
    Head(T,List<T>),
    Nil
}

class HashMap<K,V> {
    keys:[K],
    values:[V];

    fn new() -> HashMap<K,V> {
        HashMap {
            keys:[],
            values[]
        }
    }
}

fn id<T>(v:T) -> T {
    return v;
}
  
fn main() {

}
```

Whilst the language is in a good state and it is possible to write small to medium programs within Tox but there are two features that I plan on implementing before I add anything more.  The two features are modules and pattern matching. I have already started working on pattern matching and I have been able to add the type checking of pattern matching but the checking for redundant pattern sometimes fails. 

## Rust

I first started implementing Tox as a way to learn Rust and I have to say I have fallen in love with the language. Unlike what a lot of people say about the I only have praises for it and haven't ran into many problems with it and if I did have a problem the [/r/rust](https://www.reddit.com/r/rust/) community helped and [clippy](https://github.com/rust-lang/rust-clippy) which is a valuable liniting tool helps you write more idiomatic rust. Another factor that made Rust really pleasant to use was the fact that it had pattern matching, pattern matching is a very useful feature and makes langauges that have it very suitable for writing a compiler. If I were to be asked to rewrite Tox I would still choose Rust.