## std
Standard library for rust, foundation of portable rust software
- offers core types, like `Vec<T>` and `Option<T>` 
- available in all rust crates by default

-> some features of **std** *depend on OS system features*, which we can't use in the Kernel
-> some of the features that we *can* use:

- [iterators](https://doc.rust-lang.org/book/ch13-02-iterators.html)
- [closures](https://doc.rust-lang.org/book/ch13-01-closures.html)
- [pattern matching](https://doc.rust-lang.org/book/ch06-00-enums.html)
- [option](https://doc.rust-lang.org/core/option/) & [result](https://doc.rust-lang.org/core/result/)
- [string formatting](https://doc.rust-lang.org/core/macro.write.html)
- [ownership system](https://doc.rust-lang.org/book/ch04-00-understanding-ownership.html)

## Disabling the std library
Add the [`no_std` attribute](https://doc.rust-lang.org/1.30.0/book/first-edition/using-rust-without-the-standard-library.html):

```rust
// main.rs

#![no_std]

fn main() {
    println!("Hello, world!"); // -> error, since println macro not part of std
}
```

Without std, there's a few things that we need to be aware of:
- We can't use macros which are part of **std**, such as `println`
- We need our own `#[panic_handler]` since the **std** library provides its own
- We need to disable unwinding, so the `eh_personality` language item is not needed
- Since the freestanding executable does not have access to the rust **runtime system** we need a different entry point than the "main" function -> add `#[no_main]`

### Runtime System
- Environment **where the program is intended to run**, it takes care of application memory, access of variables, passing parameters to procedures, interfacing with the OS. 

### Linker
- Program that combines the generated code into an executable
- Every machine has its own Linker, since the executable format is differs from each other.

-> In this case there's an error as the Linker thinks the program depends on the C runtime, which it doesn't

*Adding the bare metal target*
```
rustup target add thumbv7em-none-eabihf
```

*running the build*
```
cargo build --target thumbv7em-none-eabihf
```

### "!" return type
An exclamation mark in rust means that the function is marked as **diverging function**, returning the "never" type `!` ( so the function should never return )
### cargo.toml
Contains crate config, such as: crate name, author, [semantic version](https://semver.org/) number, and dependencies. It's essentially something similar to *package.json* used in node.js dev.


