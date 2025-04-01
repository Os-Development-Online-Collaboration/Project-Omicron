#Mode

code that runs in user mode is restricted in what it can do. For example, when running in user mode, a [[Process]] can't issue I/O requests; doing so would result in the processor raising an exception; the OS would then likely kill the [[Process]].