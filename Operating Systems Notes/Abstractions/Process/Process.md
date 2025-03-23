#Concept 

# Informal definition
It is a **running program**

# Machine State
To understand what constitutes a process, we have to understand its **machine state**: what a program can read or update when it is running. 

## Memory
Instructions lie in memory; the data that the running program read and writes sits in memory as well. The memory that the process can address (called its **address space**) is part of the process.

## Registers
Also part of the process's machine state are **registers**; many instructions explicitly read or update registers and thus clearly they are important to the execution of the process. 

## I/O Information
Programs often access persistent storage devices too. Such I/O information might include a list of the files the process currently has open, and will also need to be stored in a process. 

# Operations of the Process API
- **Create**: An operating system must include some method to create new processes. When you type a command into the shell, or double-click on an application icon, the OS is invoked to create a new process to run the program you have indicated.
- **Destroy**: As there is an interface for process creation, systems also provide an interface to destroy processes forcefully. Of course, many processes will run and just exit by themselves when complete; when they don’t, however, the user may wish to kill them, and thus an interface to halt a runaway process is quite useful.
- **Wait**: Sometimes it is useful to wait for a process to stop running; thus some kind of waiting interface is often provided.
- **Miscellaneous Control**: Other than killing or waiting for a process, there are sometimes other controls that are possible. For example, most operating systems provide some kind of method to suspend a process (stop it from running for a while) and then resume it (continue it running).
- **Status**: There are usually interfaces to get some status information about a process as well, such as how long it has run for, or what state it is in.

![[Loading - From Program To Process.png]]

# Steps for Process Creation
1. **Load** its code and any static data (e.g., initialized variables) into memory, into address space of the process.
2. Some memory must be allocated for the program's **run-time stack** (or just **stack**)
3. Allocate some memory for the program's **heap**
4. Further **Initialization Tasks**

# Process States
A process can be in one of three states:
- **Running**: In the running state, a process is running on a processor. This means it is executing instructions.
- **Ready**: In the ready state, a process is ready to run but for some reason the OS has chosen not to run it at this given moment.
- **Blocked**: In the blocked state, a process has performed some kind of operation that makes it not ready to run until some other event takes place. A common example: when a process initiates an I/O request to a disk, it becomes blocked and thus some other process can use the processor. 

![[Process - State Transitions.png]]

# Example of simple process transition

| Time | Process0 | Process1 | Notes             |
| ---- | -------- | -------- | ----------------- |
| 1    | Running  | Ready    |                   |
| 2    | Running  | Ready    |                   |
| 3    | Running  | Ready    |                   |
| 4    | Running  | Ready    | Process0 now done |
| 5    | -        | Running  |                   |
| 6    | -        | Running  |                   |
| 7    | -        | Running  |                   |
| 8    | -        | Running  | Process1 now done |

# Example of complex process transition
| Time | Process0 | Process1 | Notes                                 |
| ---- | -------- | -------- | ------------------------------------- |
| 1    | Running  | Ready    |                                       |
| 2    | Running  | Ready    |                                       |
| 3    | Running  | Ready    | Process0 initiates I/O                |
| 4    | Blocked  | Running  | Process0 is blocked, so Process1 runs |
| 5    | Blocked  | Running  |                                       |
| 6    | Blocked  | Running  |                                       |
| 7    | Ready    | Running  | I/O done                              |
| 8    | Ready    | Running  | Process1 now done                     |
| 9    | Running  |          |                                       |
| 10   | Running  |          | Process0 now done                     |

# Data Structures
```c
// The registers xv6 will save and restore
// to stop and subsequently restart a process
struct context {
	int eip;
	int esp;
	int ebx;
	int ecx;
	int edx;
	int esi;
	int edi;
	int ebp
}

// the different states a process can be in
enum proc_state { UNUSED, EMBRYO, SLEEPING,
				  RUNNABLE, RUNNING, ZOMBIE };

// the information xv6 tracks about each process
// including its register context and state
struct proc {
	char* mem; // Start of process memory
	uint sz; // Size of process memory
	char* kstack; // Bottom of kernel stack for this process
	enum proc_state state; // Process state
	int pid; // Process ID
	struct proc* parent; // Parent process
	void* chan; // If !zero, sleeping on chan
	int killed; // If !zero, has been killed
	struct file* ofile[NOFILE]; // Open files
	struct inode* cwd; // Current directory
	struct context context; // Switch here to run process
	struct trapframe* tf; // Trap frame for the current interrupt
}
```

