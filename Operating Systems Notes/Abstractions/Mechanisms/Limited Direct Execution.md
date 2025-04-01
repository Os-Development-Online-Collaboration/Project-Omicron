#Mechanism 

# program flow
1. Create a process entry for it in a process list
2. allocate some memory for it
3. load the program code into memory (from disk)
4. locate the entry point
5. jump to entry point
6. start running user code
7. jump back to kernel once finished


# Direct Execution Protocol (Without Limits)
![[direct execution protocol - without limits.png]]

"Without limits on running programs, the OS wouldn't be in control of anything and thus would be 'just a library' - a very sad state of affairs for an aspiring operating system!"

# Problem 1 - Restricted Operations
## Advantage
- Fast: The programs runs natively on the hardware CPU and thus executes as quickly as one would expect

# Limited Direct Execution Protocol
![[limited direct execution protocol.png]]