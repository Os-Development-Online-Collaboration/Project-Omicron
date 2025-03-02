Real Mode is a simplistic 16-bit mode that is present on all x86 processors. 

# History
It was the first x86 mode design and was used by many early operating systems before [[Protected Mode]] was implemented. For compatibility purposes, all x86 processors begin execution in Real Mode. 

# Pros
- The [[BIOS]] installs device drivers to control devices and handle interrupts.
- [[BIOS Functions]] provide operating systems with an advanced collection of low level API functions.
- Memory access is faster due to the lack of descriptor tables to check and smaller registers.

# Cons
- Less than 1 MB of RAM is available for use.
- There is no hardware-based memory protection (GDT), nor virtual memory.
- There is no built in security mechanisms to protect against buggy or malicious applications.
- The default CPU operand length is only 16 bits.
- The memory addressing modes provided are more restrictive than other CPU modes.
- Accessing more than 64k requires the use of segment register that are difficult to work with.

# Misconceptions
## Real Mode can only access 16-bit registers
That is not true. All of the 32-bit registers (EAX, ...) are still usable, by adding the "operand Size Override Prefix" (0x66) to the beginning of any instruction. 

# Memory Addressing
There is a little over 1 MB of "addressable" memory (including the [[High Memory Area]]). 

The usable amount will be much less than 1 MB. Memory access is done using [[Segmentation]] via a segment::offset system.

## Registers
There are six 16-bit segment registers: CS, DS, ES, FS, GS, and SS. 

When using segment registers, addresses are given with the following notation
```
12F3  :  4B27
  ^       ^
Segment   Offset
```

Segments and Offsets are related to physical addresses by the equation:
```
PhysicalAddress = Segment * 16 + Offset
```

## The Stack
SS and SP are 16-bit segment:offset registers that specify a 20-bit physical address, which is the current "top" of the stack. 

The stack stores 16-bit words, grows downwards, and must be aligned on a word (16-bit) boundary. It is used every time a program does a PUSH, POP, CALL, INT, or RET opcode and also when the [[BIOS]] handles any hardware interrupt. 

## High Memory Area
If you set DS (or any segment register) to a value of 0xFFFF, it points to an address that is 16 bytes below 1 MB. If you use that segment register as a base, with an offset of 0x10 to 0xFFFF, you can access physical memory addresses from 0x100000 to 0x10FFEF. This (almost 64 kB) area above 1 MB is called the "High Memory Area" in Real Mode. 

Note that you have to have the A20 address line activated for this to work.

## Addressing Modes
Real Mode uses 16-bit addressing mode by default. The typical programs that run in Real Mode are often limited in the number of bytes available, and it takes one extra byte in each opcode to use 32-bit addressing instead. 

