
`cargo` builds for the *host system* by default, i.e. the system you're running on.
### Rust release channels

Rust has three different release channels:
- **Nightly**, produced every night ( ongoing development )
- **Beta**, released every six weeks, for testing 
- **Stable**, released after six weeks of beta testing.

 ```
nightly: * - - * - - * - - * - - * - - * - * - *
                     |                         |
beta:                * - - - - - - - - *       *
                                       |
stable:                                *
```

-> Manage Rust installations with  [Rustup](https://www.rustup.rs/)

We will use rust `nightly`, in order to opt in on experimental features such as *feature flags*

## Target system

Describes CPU architecture, the vendor, the operating system, and the [ABI](https://stackoverflow.com/a/2456882)

The JSON below describes our Target system configuration

```json
{
    "llvm-target": "x86_64-unknown-none",
    "data-layout": "e-m:e-p270:32:32-p271:32:32-p272:64:64-i64:64-i128:128-f80:128-n8:16:32:64-S128",
    "arch": "x86_64",
    "target-endian": "little",
    "target-pointer-width": "64",
    "target-c-int-width": "32",
    "os": "none",
    "executables": true,
    // Cross platform Linker
	"linker-flavor": "ld.lld", 
	"linker": "rust-lld",
	// No Stack unwinding support
	"panic-strategy": "abort",
	// Avoid stack corruption
	"disable-redzone": true,
	// Enable + / disable - target features
	"features": "-mmx,-sse,+soft-float", // - SIMD features ->  + soft float
	// Use corresponding ABI
	"rustc-abi": "x86-softfloat"
	
}
```


### The `build-std` feature 

*requires version 2020-07-15 or higher*

Our custom target does not have the `core` by default, because it is not a supported host triple (e.g., `x86_64-unknown-linux-gnu`)

We have to use a feature from the `nightly`build, called `build-std`, to recompile the `core`library and other standard library crates on demand.

*local [cargo configuration](https://doc.rust-lang.org/cargo/reference/config.html)*

```toml
# in .cargo/config.toml

[unstable]
build-std = ["core", "compiler_builtins"]
```

## VGA text Mode

Simple, old-school way of displaying text on the screen using [VGA](https://en.wikipedia.org/wiki/Video_Graphics_Array)

 - 25 lines, each contain 80 character cells
 - Special Memory area mapped to the [VGA Hardware](https://wiki.osdev.org/VGA_Hardware)

### Pointer
Variable that stores a memory address, rather than the value itself

```rust
foo = 0xb8000
```

It's not possible to directly manipulate memory, unless marked as `unsafe` 

```rust
unsafe {
 ...
}
```

The `unsafe` block allows to:

- Dereference a raw pointer
- Call an unsafe function or method
- Access or modify a mutable static variable
- Implement an unsafe trait
- Access fields of a `union`

>[!Warning]
>This is not how we want to do things in rust!
>It's easy to **mess up when working with raw pointers in unsafe blocks**
>e.g. writing beyond the buffer's end if not being careful
>
>-> minimize use of `unsafe` as much as possible

**``offset(n)``**
moves a raw pointer by `n` positions in memory

**`isize`**
signed integer
