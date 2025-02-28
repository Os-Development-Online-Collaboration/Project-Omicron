# What does it do?
- Bring the kernel (and all the kernel needs to bootstrap) into memory
- Provide the kernel with the information it needs to work correctly
- Switch to an environment that the kernel will like
- Transfer control to the kernel

# For x86
On x86, the bootloader runs in [[Real Mode]]. 

As a consequence of this, it has easy access to BIOS resources and functions.

## Good use cases
- Memory Map Detection
- Detection of available video modes
- loading of additional files
- Collect information and present it in a way the kernel will be able to understand



# Loading the kernel
#TODO

# Giving the kernel its information
- Tell the root partition to start from
- map of the address space - where physical memory is and where it's not
- popular queries regarding video modes

