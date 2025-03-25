### Bootimage tool

This tool first compiles the kernel and the [[Bootloader]], then links them together to create a bootable [disk image](https://wiki.osdev.org/Disk_Images)

```
cargo install bootimage
rustup component add llvm-tools-preview

cargo bootimage
```

**What does it do?**
- compiles the kernel to an [ELF](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format) file
- compiles the bootloader dependency as a standalone executable
- links the bytes of the kernel ELF file to the bootloader

### Booting in QEMU

```
qemu-system-x86_64 -drive format=raw,file=target/x86_64-omicron_os/debug/bootimage-omicron_os.bin
```

### Write to an USB stick

>[!warning] Careful
Everything on that device will be overwritten!

```
dd if=target/x86_64-omicron_os/debug/bootimage-omicron_os.bin of=/dev/sdX && sync
```

### Cargo run

Makes it easier to run the kernel in QEMU:

```toml
# in .cargo/config.toml

[target.'cfg(target_os = "none")']
runner = "bootimage runner"
```

