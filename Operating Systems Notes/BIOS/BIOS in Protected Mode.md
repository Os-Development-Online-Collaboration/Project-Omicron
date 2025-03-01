#Interface 

In [[Protected Mode]], almost all [[BIOS Functions]] are unavailable, and trying to call them will return in exceptions or unreliable responses. 

# Potential services that work in protected mode
- SMBios
- PCI
- PnP
- VBE

# Accessing BIOS when in Protected Mode
If you must use [[Real Mode]] [[BIOS Functions]] after the CPU has been switched into [[Protected Mode]], then consider [[Virtual 8086 Mode]] or perhaps exit [[Protected Mode]], and momentarily return to [[Real Mode]]. 

Both methods have serious problems, and therefore any calls to the [[BIOS]] should be done before any physical device is programmed by your code:
- [[BIOS]] calls may use interrupts, which means that you need to forward IRQs or map the PIC back to its original configuration.
- [[BIOS]] calls may access devices that you have already configured - notably the PIT and PIC
- [[BIOS]] calls can enter [[Protected Mode]] on their own to access MMIO registers, which is beyond the limits of [[Virtual 8086 Mode]].
- In [[Real Mode]], you have no way of managing interrupts and your drivers may get stuck for interrupts being lost.
- In [[Real Mode]], you have no control over time, performance and security guarantees.