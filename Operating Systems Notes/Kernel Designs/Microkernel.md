#kernel  
![Basic Overview of a Microkernel](https://wiki.osdev.org/images/2/28/Microkernel.png)  
_Basic overview of a Microkernel_

This keeps the **[[kernel space]]** as minimal as possible, moving most services,
such as device drivers, file systems, and networking to **[[user space]]**. 
The kernel is only responsible for **memory allocation, scheduling, and messaging** ([[IPC]]).
It improves **stability** and makes the system more **modular**, but can reduce performance because it relies heavily on messaging and context switches. (But that doesn't mean that a well-designed [[Microkernel]] can't beat a sloppy [[Monolithic Kernel]])

-> More on related kernels: [[Monolithic Kernel]] & [[Hybrid Kernel]]

### Pros
**More stable**, crashes in [[user space]] services don’t take down the kernel  
**More secure**, isolation of services limits system-wide vulnerabilities  
**Modular**, components can be updated or replaced independently

### Cons
**Slower**, due to overhead from [[IPC]] and frequent context switches  
**More complex**, requires well-designed messaging & process management  
**Driver performance issues**, since drivers run in user space

### Examples
- Mach
- QNX
- [L4](https://wiki.osdev.org/L4 "L4")
- AmigaOS
- [Minix](http://minix3.org/)

References: [Microkernel - OSDev Wiki](https://wiki.osdev.org/Microkernel), [Wikipedia](https://en.wikipedia.org/wiki/Microkernel)