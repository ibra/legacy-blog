+++
title = "Rust Is The Most Fun I've Had Programming In Ages"
description = "Just checking in."
category = "Ramble"
date = 2021-10-30

[extra]
author = "Ibrahim"

[taxonomies]
tags = ["rust"]
categories = ["Ramble"]
+++

Rust is the most fun I've had programming in a long, long time, and I'm super excited to see what the future holds for it <!-- more -->, with [WebAssembly](https://webassembly.org/) becoming even more widely adopted and it being called the most loved programming language according to the StackOverflow Developer survey of 2021.

![Stack Overflow Survey](https://ibrahim.is-terrible.com/5e9WlZekE.png)

I would consider myself a Rust beginner at best, but this language is so damn fun that I'm actively looking for excuses to make any project idea that I have in it.

## Background

A lot of my programmer friends have been using Rust for a while, it always looked kind of weird to me as someone coming from a high-level C# and Javascript background, things like the lack of ternary and other choices with the syntax make it look odd to the occasional onlooker.

However, after using it for a few projects, the Rust syntax has quickly grown to become the one I most love out of everything I've ever used. ~~Also holy shit match expressions are so based.~~

```rs
fn fizzbuzz (number: u32) -> String {
    match (number % 3, number % 5) {
        (0, 0) => "fizzbuzz".to_string(),
        (0, _) => "fizz".to_string(),
        (_, 0) => "buzz".to_string(),
        (_, _) => number.to_string()
    }
}
```

Recently, I made a [discord bot in Rust](https://github.com/ibra/philososhark-rs) and that was extremely fun, and the [serenity](https://github.com/serenity-rs/serenity) library is an amazing wrapper for the Rust API.

Before that, as a tiny initial project, I made a tiny CLI tool for shortening links, called [snippy](https://github.com/ibra/snippy).

I also plan to use Rust in some performance-critical application because Rust in general is kinda zooming, [sometimes outperforming even C if optimized](https://kornel.ski/rust-c-speed).

## ...Why?

So... why should you even Rust? In my case it was just because I wanted to try something that everyone who used seemed to absolutely love, and I wanted to see what the hype was about.

But truth be told, Rust, even in the _relatively_ early stages it is in, has a lot of uses. Something i've seen it be amazing at is command-line tools, streamlining the process even more with its direct compilation to an executable.

Anything that's supposed to be memory-safe and/or concurrent should definitely consider Rust as an option, as that's what it excels at.

On top of that, like i said at the start, WebAssembly is taking off, and fast. It promises faster web applications and is supported in all major browsers including Apple, Google, Microsoft, and Mozilla. It can become a compilation target for languages, and Rust was actually one of the early targeters to WebAssembly and can directly compile to WebAssembly without the need for extra tools.

It's not like this is experimental either, tons of great frameworks like [Rocket](https://rocket.rs/) and [Actix](https://actix.rs/) exist and are mature frameworks ready to be used in production.

Rust also has its uses in game development with the emergence of engines like [Bevy](https://www.bevy.com/), but I personally wouldnt recommend it for production beyond experimenting and prototyping or the occasional game jam game, having dabbled in it a bit.

## Conclusion

So yeah that was about it, Rust is very epic, bunch of uses, and even if you have none its just extremely fun to dabble in. So go try it. [Now](https://www.rust-lang.org/learn/get-started).
