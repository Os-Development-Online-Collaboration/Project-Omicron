#Design 

A two-stage [[Bootloader]] actually consists of two bootloaders after each other. The first being small with the sole purpose of loading the second one. The second one can then contain all the code needed for loading the kernel. [GRUB](https://wiki.osdev.org/GRUB "GRUB") uses two (or arguably, three) stages.