#Tip 

The hardware assists the OS by providing different modes of execution. In [[User Mode]], applications do not have full access to hardware resources. In [[Kernel Mode]], the OS has access to the full resources of the machine. Special instructions to **trap** into the kernel and **return-from-trap** back to user-mode programs are also provided, as well as instructions that allow the OS to tell the hardware where the **trap table** resides in memory. 

