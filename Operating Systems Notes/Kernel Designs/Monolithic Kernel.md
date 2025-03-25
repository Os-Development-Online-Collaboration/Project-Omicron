#kernel 
This means that the entire operating system, including process management, memory handling, device drivers, and file systems, runs in **kernel space**, making it the opposite of a [[Microkernel]], which moves many of these services to **user space** to improve stability at the cost of performance.

Here's a cool image which explained me this whole thing better than the texts I read:
![[OS-structure.svg]]

More to the related two kernels can be found on the [[Microkernel]] & [[Hybrid Kernel]] page

### Pros
**Fast**, fewer context switches since everything runs in kernel space  
### Cons
**Less stable**, a failure in one part can crash the entire system  
**Harder to maintain/debug**, due to tight integration

### Pure vs. Modular Monolithic

- A "pure monolithic" kernel is one where all components are built into a single binary, which is common in **embedded systems**, making it rare for general purpose computers
- Most modern monolithic kernels (e.g. Linux, BSDs) allow **loadable kernel modules (LKM)** for flexibility, making them **modular monolithic** kernels.

### Examples
- Linux (monolithic but modular)
- MS-DOS, including Windows 9x (95, 98, Me)
- Mac OS <= 8.6
- Most BSDs (also with modules)
- [Xv6](https://wiki.osdev.org/Xv6 "Xv6")**

 References: [OSDev Wiki](https://wiki.osdev.org/Monolithic_Kernel), [Wikipedia](https://en.wikipedia.org/wiki/Monolithic_kernel)
