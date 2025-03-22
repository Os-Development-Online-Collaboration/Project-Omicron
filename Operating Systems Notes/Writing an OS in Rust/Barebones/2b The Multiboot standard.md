The [Free Software Foundation](https://en.wikipedia.org/wiki/Free_Software_Foundation) made an open bootloader called [Multiboot](https://wiki.osdev.org/Multiboot) 

-> Avoids the need for each OS to have its own bootloader
-> Allows Multiboot-compilant bootloaders to load any Multiboot compilant OS

Reference implementation: [GNU GRUB](https://en.wikipedia.org/wiki/GNU_GRUB) (most popular among Linux)

Insert a [Multiboot header](https://www.gnu.org/software/grub/manual/multiboot/multiboot.html#OS-image-format) at the beginning of the Kernel file to make it Multiboot-compilant

## Problems

- Only 32-Bit [[Real Mode]] is supported. ( you have to do the CPU config to switch to 64-Bit long mode yourself)
- Designed to make the bootloader simple instead of the kernel
- Bad Docs
- GRUB needs to be installed on the host system, making development on Windows / Mac difficult

