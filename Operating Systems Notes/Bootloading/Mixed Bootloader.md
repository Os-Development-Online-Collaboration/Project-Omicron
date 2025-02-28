#Design 

Another way to avoid the 512-byte barrier is to split the [[Bootloader]] in two parts, where the first half (512 bytes) can load the rest. This can be achieved by inserting a '512-bytes' break in the ASM code, making sure the rest of the loader is put after the [[Bootsector]].

