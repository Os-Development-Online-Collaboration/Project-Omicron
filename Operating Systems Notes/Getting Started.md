## Development environment
Most recommended & widely used is **GNU/Linux** primarily due to better availability of tools compared to Windows, making it a standard workflow
[Source: OSDev Wiki](https://wiki.osdev.org/Getting_Started#:~:text=semester%20isn%27t%20realistic.-,Choosing%20your%20development%20environment,-You%20need%20a) 


# What happens when running a program?
It executes instructions, many millions or even billions of times every second.

1. The processor **fetches** an instruction from memory
2. **Decodes** it (i.e., figures out which instruction this is)
3. and **executes** it
4. after it is done with this instruction, the processor moves to the next instruction

The above process describes the basics of **Von Neumann** model of computing. 

# OS's role of virtualization
The OS takes a **physical** resource (such as the processor, or memory, or a disk) and transforms it into a more general, powerful, and easy-to-use **virtual** form of itself. Sometimes, for this reason, we refer to the operating system as a **virtual machine**.

To make users able to tell the OS what to do, the OS provides some interfaces (APIs) that are available to applications. Because the OS provides these calls to run programs, access memory, and devices, and other related actions, we also sometimes say that the OS provides a **standard library** to applications.

The OS is sometimes known as a resource manager. Each of the CPU, memory, and disk is a **resource** of the system; it is the operating system's role to **manage** those resources, doing so efficiently or fairly, or indeed with many other possible goals in mind. 

# Design Goals
- Take physical resources, such as CPU, memory, or disk, and virtualizes them
- Store files **persistently**
- build up **abstractions**
- Provide high **performance**
- **Minimize the overheads** of the OS
- **protection** between applications
- **isolation**; isolating processes from one another to protect
- **reliability**
- **energy-efficiency**
- **security**
- **mobility**
- 