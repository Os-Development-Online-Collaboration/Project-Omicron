#Interface


# The AH Register
To access a [[BIOS]] function, you generally set the AH CPU register (or AX, or EAX) to a particular value, and then do an INT opcode. 

The value in AH (or AX, or EAX), combined with the particular interrupt number selected requests a specific [[BIOS]] function. 

# Other Registers
Other CPU registers hold any "arguments" to the function, and often the return values from the function, also. 

# Common Errors
ALWAYS make sure that the INT and AH values are written in [[Hexadecimal Notation]]. 

# Error handling for BIOS Functions
The [[BIOS]] functions themselves should never crash. On any error they will:
- almost always set the carry flag (test with JC),
- sometimes return "ah = 0x86 (unsupported function)",
- sometimes return "ah = 0x80 (invalid command)"
- or (for seriously buggy BIOSes) return with nothing changed.

Try to always test these error returns, as in many circumstances the [[BIOS]] functions might appear to be returning valid (but very wrong) data -- rather than an error code. 

# The INT 0x10 functions
- INT 0x10, AH = 1 -- set up the cursor
- INT 0x10, AH = 3 -- cursor position
- INT 0x10, AH = 0xE -- display char
- INT 0x10, AH = 0xF -- get video page and mode
- INT 0x10, AH = 0x11 -- set 8x8 font
- INT 0x10, AH = 0x12 -- detect EGA/VGA
- INT 0x10, AH = 0x13 -- display string
- INT 0x10, AH = 0x1200 -- Alternate print screen
- INT 0x10, AH = 0x1201 -- turn off cursor emulation
- INT 0x10, AX = 0x4F00 -- video memory size
- INT 0x10, AX = 0x4F01 -- VESA get mode information call
- INT 0x10, AX = 0x4F02 -- select VESA video modes
- INT 0x10, AX = 0x4F0A -- VESA 2.0 protected mode interface

# The INT 0x11 function
Reserved for Hardware Detection

# The INT 0x12 function
"Get low memory size"

# The INT 0x13 functions
- INT 0x13, AH = 0 -- reset floppy/hard disk
- INT 0x13, AH = 2 -- read floppy/hard disk in CHS mode
- INT 0x13, AH = 3 -- write floppy/hard disk in CHS mode
- INT 0x13, AH = 0x15 -- detect second disk
- INT 0x13, AH = 0x41 -- test existence of INT 13 extensions
- INT 0x13, AH = 0x42 -- read hard disk in LBA mode
- INT 0x13, AH = 0x43 -- write hard disk in LBA mode

# The INT 0x15 functions
- INT 0x15, EAX = 0xE820 -- get complete memory map
- INT 0x15, AX = 0xE801 -- get contiguous memory size
- INT 0x15, AX = 0xE881 -- get contiguous memory size
- INT 0x15, AH = 0x88 -- get contiguous memory size
- INT 0x15, AH = 0xC0 -- Detect MCA bus
- INT 0x15, AX = 0x0530 -- Detect APM [[BIOS]]
- INT 0x15, AH = 0x5300 -- APM detect
- INT 0x15, AX = 0x5303 -- APM connect using 32 bit
- INT 0x15, AX = 0x5304 -- APM disconnect

# The INT 0x16 functions
- INT 0x16, AH = 0 -- read keyboard scancode (blocking)
- INT 0x16, AH = 1 -- read keyboard scancode (non-blocking)
- INT 0x16, AH = 3 -- keyboard repeat rate

