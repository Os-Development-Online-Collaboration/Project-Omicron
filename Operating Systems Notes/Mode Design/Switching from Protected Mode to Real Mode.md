#Concept

It is possible for a [[Protected Mode]] operating system to use [[Virtual 8086 Mode]] mode to access [[BIOS Functions]]. However VM86 mode has its own complications and difficulties. 

Some OS designers think that it is simpler and clearner to temporarily return to [[Real Mode]] on those occasions when it is neccesary to access a [[BIOS]] function. 

This requires creating a special Ring 0 program, and placing it in a physical memory address that can be accessed in [[Real Mode]]. 

The OS usually needs to pass an information packet about which [[BIOS]] function to execute. 

The program needs to go through the following steps:
1. Disable the interrupts:
	- Turn off maskable interrupts using CLI.
	- Disable NMI (optional).
2. Turn off [[Paging]]:
	- Transfer control to a 1:1 page.
	- Ensure that the [[GDT]] and [[IDT]] are in a 1:1 page.
	- Clear the PG-flag in the zeroth control register.
	- Set the third control register to 0.
3. Use [[GDT]] with 16-bit tables (skip this step if one is already available):
	- Create a new [[GDT]] with a 16-bit data and code segment:
		- Limit: 0xFFFFF
		- Base: 0x0
		- 16-bit
		- Privilege level: 0
		- Granularity: 0
		- Rad and Write: 1
	- Load new [[GDT]] ensuring that the currently used selectors will remain the same (index in cs/ds/ss will be copy of original segment in new [[GDT]])
4. Far jump to 16-bit [[Protected Mode]]:
	- Far jump to 16-bit [[Protected Mode]] with a 16-bit segment index.
5. Load data segment selectors with 16-bit indexes:
	- Load ds, es, fs, gs, ss with 16-bit data segment.
6. Load [[Real Mode]] [[IDT]]:
	- Limit: 0x3FF
	- Base 0x0
	- Use lidt
7. Disable [[Protected Mode]]:
	- Set PE bit in CR0 to false.
8. Far jump to [[Real Mode]]:
	- Far jump to  [[Real Mode]] with [[Real Mode]] segment selector (usually 0).
9. Reload data segment registers with [[Real Mode]] values:
	- Load ds, es, fs, gs, ss with appropriate [[Real Mode]] values (usually 0).
10. Set stack pointer to appropriate value:
	- Set sp to stack value that will not interfere with [[Real Mode]] program.
11. Enable interrupts:
	- Enable maskable interrupts with STI.
12. Continue on in [[Real Mode]] with all [[BIOS]] interrupts. 

# x86 Example 
```x86
[bits 16]

idt_real:
	dw 0x3ff		; 256 entries, 4b each = 1K
	dd 0			; Real Mode IVT @ 0x0000

savcr0:
	dd 0			; Storage location for pmode CR0.

Entry16:
        ; We are already in 16-bit mode here!

	cli			; Disable interrupts.

	; Need 16-bit Protected Mode GDT entries!
	mov eax, DATASEL16	; 16-bit Protected Mode data selector.
	mov ds, eax
	mov es, eax
	mov fs, eax
	mov gs, eax
	mov ss, eax

	; Disable paging (we need everything to be 1:1 mapped).
	mov eax, cr0
	mov [savcr0], eax	; save pmode CR0
	and eax, 0x7FFFFFFe	; Disable paging bit & disable 16-bit pmode.
	mov cr0, eax

	jmp 0:GoRMode		; Perform Far jump to set CS.

GoRMode:
	mov sp, 0x8000		; pick a stack pointer.
	mov ax, 0		; Reset segment registers to 0.
	mov ds, ax
	mov es, ax
	mov fs, ax
	mov gs, ax
	mov ss, ax
	lidt [idt_real]
	sti			; Restore interrupts -- be careful, unhandled int's will kill it.
```