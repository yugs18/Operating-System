# Operating Systems - personal notes

These notes are written to solidify my understanding of Operating Systems while studying OS theory.

---

## What is an Operating Systems?

- Interface between user(programmer) & computer.

    User - OS(interface) - hardware

- Basic Structure
```
                Componentes of Hardware
        Memory(P) <-> Control Unit -> Output/Input
                        A.L.U
                    CPU(Processor)

    Architecture of computer - Proposed by Von Neumann
```

- **Control Unit (CU)**
  - Generates **timing and control signals** (clock signals)
  - Controls and coordinates CPU operations
  - Responsible for sequencing and execution of **micro-operations**
    - Micro-operations are low-level actions performed on data stored in CPU registers

- **CPU Memory Access**
  - CPU can directly access **only primary memory (RAM)**
  - Data stored in secondary memory must be loaded into RAM before execution


Example :-
```c
int a,b,c;
b=1, c=2;
a = b+c; -> High - Level Statement (Macro - operation)
    Compiler
Micro-Instructions: 
    1. Load R₁, b 
    2. Load R₂, c 
    3. ADD R₁, R₂ 
    4. Store a, R₁
```
---

- **Arithmetic Logic Unit (ALU)**
  - Also called the **functional unit** of the CPU
  - Performs all **arithmetic operations** (addition, subtraction, etc.)
  - Performs **logical operations** (AND, OR, NOT, comparisons)

---

- **Types of Memory**

  - **Primary (Main) Memory**
    - Examples: RAM, ROM, Cache, Registers
    - Characteristics:
      - Volatile (data is lost when power goes off)
      - Faster access speed
      - More expensive
      - Smaller in size

  - **Secondary (Auxiliary) Memory**
    - Examples: Hard disk, SSD, pen drive, etc.
    - Characteristics:
      - Non-volatile (data does not vanish when power is turned off)
      - Slower access speed
      - Less expensive
      - Larger in size

---

- **Secondary Memory in Von Neumann Architecture**
  - As per **Von Neumann Architecture (VNA)**, secondary memory is considered part of **Input/Output (I/O) devices**
  - CPU cannot directly access secondary memory
  - Data must be transferred to primary memory before execution

- **Program execution in the Von Neumann Architecture**
  - Test.c -> Compiler -> .exe file -> OS -> main memory -> CPU

- When a program is loaded in memory for execution, it's called **Stored Program Concept**
  - Instructions and data are stored together in memory
  - CPU fetches instructions from memory and executes them sequentially

- Fundamental principal of Von Neumann Architecture
  - Stored Program Concept
  - Sequential Execution of Instructions

- **Kernel**
  - Core part of the Operating System
  - Runs in privileged (kernel) mode

- OS consists of Several modules
  - Kernel(core/nucleus)
    - Process Manager(CPU)
    - Memory Manager (Memory)
    - File Manager (Devices)
    - Device Manager (Devices)
    - Protection Manager (Resources)

- OS also act as **Resource Manager**
  - Allocation, Deallocation and Management

- **Control Program** - A program that control all theoperation of the computer.

- Set of utilities to simpify application development
  - Takes charge of hardware
  - Create env/platform that help us to focus on dev. in high-level mode
  OS will perform work at the back of stage

- User -> Application or Program -> OS(Kernel) -> Hardware

---

## Types of Operating Systems

- **Basic Operating Systems**
  - **Batch OS**  
    - Jobs are executed in batches with no user interaction
  - **Real-Time OS**
    - Responds within strict time constraints
  - **Time-Sharing OS**
    - Multiple users share CPU time interactively
  - **Multiprogramming OS**
    - Multiple programs are kept in memory to maximize CPU utilization

- **Advanced Operating Systems**
  - **Distributed OS**
    - Manages resources across multiple connected systems
  - **Network OS**
    - Provides services over a network to connected systems
  - **Multiprocessor OS**
    - Uses multiple CPUs to execute processes concurrently

---

- **Uni-programming**
  - Ability of an OS to hold **only one program in memory at a time**
  - CPU remains idle during I/O operations
- **Multiprogramming**
  - Multiple programs reside in memory simultaneously
  - Improves CPU utilization

---

- **Uni-programming Operating System**
  - OS can load **only a single program** into memory at a time
  - When the program moves to **I/O operations**, the CPU becomes **idle**
  - This leads to:
    - Lower **throughput**
    - Lower **CPU efficiency**
  - This is undesirable; we want **efficient CPU utilization**

---

- **Throughput**
  - Number of programs completed per unit time

---

- **Example of Uni-programming OS**
  - **MS-DOS (Microsoft Disk Operating System)**
    - Used in the early 1990s
    - Command-line based
    - No graphical user interface (GUI)

---

- **Note**
  - In **Unix**, it is called a *process*
  - In **Windows**, it is called a *task*

---

## Types of Multiprogramming

- **Preemptive Multiprogramming**
  - OS can **forcefully deallocate the CPU** from a running process
  - Improves system responsiveness
  - Based on:
    - **Time** (time slicing / time quantum)
    - **Priority**

- **Non-preemptive Multiprogramming**
  - OS does **not** force a process to leave the CPU
  - A process releases the CPU **voluntarily** when:
    - All instructions are completed
    - It requests I/O
    - It makes a system call


---

## Objectives of Multiprogramming

- Maximize **CPU utilization**
- Improve **efficiency** and **throughput**
- Create the impression of **CPU multiplexing** among multiple programs

---

## Drawbacks of Non-preemptive Multiprogramming

- **Starvation**
  - Other processes may wait indefinitely
- **Poor responsiveness**
  - Not suitable for interactive systems


## Advantages of Preemptive Multiprogramming

- Improves **system responsiveness**
- Prevents long CPU monopolization
- Suitable for interactive and real-time systems

---

## Architectural Requirements for Implementing a Multiprogrammed OS

- **Secondary Storage Device (I/O)**
  - Must support **Direct Memory Access (DMA)**
    - Allows efficient data transfer between secondary storage and main memory
    - Reduces CPU involvement during I/O operations

- **Memory System**
  - Must support **address translation**
    - Enables separation of logical (virtual) and physical addresses

- **Processor(CPU)**
  - **Dual Mode Operation** should be supported
    - User & Kernel Mode


## Why Are Two Addresses Needed?

- **Logical Address (Virtual Address)**
  - Generated by the CPU
  - Used by programs
  - Independent of actual memory location

- **Physical Address**
  - Actual location in main memory (RAM)
  - Used by hardware to access memory

- Address translation provides:
  - **Security** (process isolation)
  - **Protection** (one process cannot access another’s memory)
  - **Multiprogramming support**

## Address Translation Diagram
```
  Process --Logical Address--> CPU --> Memory Management Unit(MMU)(Address Translation) --Physical Address--> Main Memory(RAM)
```
- Address translation allows each process to believe it has its own private memory space.


---

## Process Management

- **Program**
  - A program is a **passive entity**
  - Stored on disk (e.g., `.exe` file)
  - Consists of:
    - **Data** – operands, variables
    - **Instructions** – load, add, store, etc.

- **Process**
  - A process is an **active entity**
  - Created when a program is **loaded from disk into main memory**
  - A program **in execution**

---

## Data Types in a Process

- **Static Data**
  - Fixed size
  - Known at compile time

- **Dynamic Data**
  - Memory allocated at runtime
  - Size can change during execution

---

## Process as an Abstract Data Type (ADT)

- A process can be viewed as an **Abstract Data Type**
- An ADT consists of:
  - **Definition**
  - **Representation / Implementation**
  - **Operations**
  - **Attributes**

---

## Process Operations

- **Create()**
  - Allocation of required resources
- **Schedule()**
  - Selection of a process to run on the CPU
- **Execute() / Run()**
  - Execution of instructions from the code section
- **Block() / Wait()**
  - Process blocks due to:
    - System call
    - I/O operation
- **Suspend()**
  - Process moved from main memory to disk
- **Resume()**
  - Process moved from disk back to main memory
- **Terminate()**
  - Deallocation of all allocated resources

---

## Process Attributes

- **Identification**
  - Process ID (PID)
  - Parent Process ID (PPID)
  - Group ID (GID)

- **CPU Related**
  - Program Counter (PC)
  - Priority
  - Process state
  - CPU burst time

- **Memory Related**
  - Memory size
  - Address limits

- **File Related**
  - List of files currently in use

- **Device Related**
  - Allocated I/O devices

---

- All process attributes are stored in the  
  **PCB (Process Control Block)**

---

## Process States and State Transitions

- A process moves through different states during its lifetime:

  - **New**
    - Process is created
    - Required resources are allocated

  - **Ready**
    - Process is ready to run
    - Waiting in the ready queue for CPU allocation

  - **Running**
    - Process is executing instructions on the CPU

  - **Blocked / Waiting**
    - Process is waiting for:
      - I/O operation
      - Completion of a system call

  - **Terminated**
    - Process has completed execution
    - Resources are released

---

## Queues in Process Management

- OS maintains multiple queues
- Queues generally follow **FIFO** order

### On-Memory Queues

- **Ready Queue**
  - Contains PCBs of processes that are ready to execute

- **Blocked / Device Queue**
  - Contains PCBs of blocked processes
  - Each I/O device has its **own device queue**

### On-Disk Queues

- **Job Queue**
  - Contains programs waiting to be loaded into main memory

- **Suspend Queue**
  - Contains processes that are suspended from memory to disk

---

## Schedulers

- **Long-Term Scheduler**
  - Moves process from **New → Ready**
  - Controls degree of multiprogramming

- **Short-Term Scheduler (CPU Scheduler)**
  - Selects process from **Ready → Running**
  - Executes frequently

- **Medium-Term Scheduler**
  - Handles **process suspension and resumption**
  - Swaps processes between memory and disk

---

## Dispatcher

- Responsible for performing **context switching**
- Activities include:
  - Saving the state of the currently running process
  - Loading the state of the next selected process
  - Switching CPU control to the new process

- Context switching introduces overhead but enables multitasking.

---

