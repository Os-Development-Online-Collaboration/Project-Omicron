#Writing an OS in Rust
![Basic Overview of writing an OS in Rust](https://os.phil-opp.com/freestanding-rust-binary/)
*Basic Overview of writing an OS in Rust*

### intro
To write an ooperating system kernel, code that does not depend on any operating system features is depended. This means most of Rust standard library can not be used. To create an OS kernel in Rust, an executable needs to be created that can run without an underlying operating system 

### Disabling the Standard Library 
By default Rust creates link to the standard library, which depends on the operating system for features such as threads, files, or networking. Since the plan is to write an operating system, the use of any OS-dependent library won't be needed and therefore the automatic inclusion of the standard library through ```no_std```

### Panic Implementation 
When disabling the standard library one of the important things that are missing is a panic handler. The ```panic_handler``` attribute defines the function that the compiler should invoke when a panic occurs; a painc is when bad things happen in the code. There are two ways to cause a panic in practice: 1. taking an actaion that causes the code to panic or 2. expliocitliy calling the panic macro.The panic handler attribute itself defines the function that the compiler should invoke when a panic occurs. Normally the standard library provides its own panic handler function, but in a ```no_std``` environment it needs to be defined itself.

### the ```eh_personality``` Language Item 
Language items are special funtions and types that are required internally by the compuiler.  While provvidingcustom implementations of language items are possible, it should only be done as a last resort. Reason for this is that language items are highly unstable implmentation details and not even type checked. the ```eh_personality``` language item marks a function that is used for implementing stack unwinding. By default, Rust uses unwinding to run destructor of all live stack variables in case of a panic. This ensures that all used memory is freed and allows the parent thread to catch the panic and continue execution. 

### The start attribute 
It is commonly thought that the ```main``` function is the first function called when a program is run. However, most languages have a runtime system, which is responsible for things such as garbage collection or software threads. The runtime needs to be called befoer ```main``` since it needs to initialize itself. rust binary typically links the standard library, execution starts in a C runtime library called ```crt0``` ("C runtime zero"), which sets up the environement for a C application. 