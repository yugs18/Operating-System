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

## CPU Scheduling

- Deals with the **design and implementation of the Short-Term Scheduler (STS)**

---

## Ready Queue to CPU Flow

```text
Ready Queue | P₁ | P₂ | ... | Pₙ | → Short-Term Scheduler → CPU
```

- Short-Term Scheduler uses CPU scheduling criteria
- These criteria define the CPU scheduling technique

---

## Short-Term Scheduling
- **Function**
  - Selects a process from the **Ready Queue** to execute on the CPU
- **Goals**
  - Maximize:
    - CPU utilization
    - Throughput
    - Efficiency
  - Minimize:
    - Waiting time
    - Turnaround time
    - Response time

---

## Process Times / Scheduling Metrics

- **Arrival Time (AT)**
  - Time when a process enters the ready queue for the first time

- **Burst Time (BT)**
  - Time spent by the process executing on the CPU

- **I/O Burst Time (IOBT)**
  - Time spent by the process waiting for I/O in blocked state

- **Start Time (ST)**
  - Time when the process gets CPU for the first time

- **Completion Time (CT)**
  - Time when the process finishes execution

- **Turnaround Time (TAT)**
  - `TAT = CT − AT`
  - Total time spent by the process in the system

- **Waiting Time (WT)**
  - `WT = TAT − BT`
  - Time spent waiting in the ready queue

- **Response Time (RT)**
  - `RT = ST − AT`
  - Time from arrival to first CPU allocation

---

## Schedule Length

- **Schedule Length (L / Makespan)**
  - Total time taken to complete all `n` processes
  - `L = CT of last process − AT of first process`

- **Number of possible schedules**
  - Non-preemptive scheduling → at most `n!`
  - Preemptive scheduling → theoretically infinite

---

## Dispatch Latency

- **Dispatch Latency**
  - Time taken by the dispatcher to:
    - Select the next process
    - Perform context switching
  - Includes **scheduling overhead**
  - Lower dispatch latency ⇒ better responsiveness

---

## Process Types

- **CPU-bound Process**
  - Long CPU bursts
  - Very little I/O

- **I/O-bound Process**
  - Frequent I/O operations
  - Short CPU bursts

---

## Scheduling Categories

- **Non-preemptive Scheduling**
  - Once a process starts execution, it cannot be forcibly removed
  - Process releases CPU voluntarily (completion, I/O, system call)

- **Preemptive Scheduling**
  - OS can forcibly remove a running process
  - Based on:
    - Time slicing
    - Priority

---

## CPU Scheduling Algorithms

- **FCFS (First Come First Serve)**
  - Non-preemptive
  - Simple
  - Suffers from convoy effect

- **SJF (Shortest Job First)**
  - Non-preemptive
  - Minimizes average waiting time
  - Can cause starvation

- **SRTF (Shortest Remaining Time First)**
  - Preemptive version of SJF
  - Preempts running process if a shorter job arrives

- **HRRN (Highest Response Ratio Next)**
  - Non-preemptive
  - Prevents starvation
  - Favors short jobs while considering waiting time

- **Priority Scheduling**
  - Can be preemptive or non-preemptive
  - Higher priority processes execute first
  - Starvation possible (solved using aging)

- **Round Robin (RR)**
  - Preemptive
  - Uses time quantum
  - Fair for interactive systems

- **Multilevel Queue Scheduling**
  - Multiple ready queues
  - Each queue has its own scheduling policy

- **Multilevel Feedback Queue (MLFQ)**
  - Dynamic priority adjustment
  - Adapts based on process behavior

---

## Starvation and Aging

- **Starvation**
  - A process waits indefinitely due to low priority

- **Aging**
  - Gradually increases priority of waiting processes
  - Prevents starvation

---

## CPU Burst Prediction

- Used in SJF and SRTF
- Based on past CPU burst behavior
- Helps estimate future burst times
- Typically implemented using exponential averaging

---

## Gantt Chart Example
```
Time: 0 3 6 10
| P1 | P2 | P3 |
```

- Used to visualize scheduling
- Helps compute:
  - Waiting time
  - Turnaround time
  - Response time

---

## Practical Usage

- **Interactive systems**
  - Round Robin (small time quantum)

- **Batch systems**
  - SJF (if burst prediction is available)

- **General-purpose OS**
  - Multilevel Feedback Queue
  - (Linux uses Completely Fair Scheduler – CFS)

---

## Key Takeaways

- CPU scheduling is central to OS performance
- Trade-off exists between fairness and efficiency
- Preemptive scheduling improves responsiveness
- Scheduling decisions directly impact user experience

---

## Inter-Process Communication (IPC) & Process Synchronization

- **Processes**
  - Are independent by nature
  - May need to **communicate and coordinate** with each other

---

## Why Synchronization is Required

- Lack of synchronization in an IPC environment can lead to:
  - **Inconsistency / incorrect results**
  - **Data loss**
  - **Deadlock** (system lock-up)

---

## Types of Process Interaction

- **Competitive Interaction**
  - Processes compete for access to **shared resources**
  - Examples:
    - Shared variables
    - Shared files
    - Shared memory
  - Lack of synchronization leads to:
    - Race conditions
    - Incorrect results

- **Cooperative Interaction**
  - Execution of one process **affects or depends on another**
  - Processes work together toward a common goal
  - Lack of synchronization can cause:
    - Inconsistency
    - Data loss
    - Deadlock

---

- Process synchronization ensures correct execution order when multiple processes access shared resources.

---

## Process Synchronization Mechanisms

### 1. Busy Waiting
- Process repeatedly checks for resource availability
- CPU keeps spinning (wastes CPU cycles)
- Example:
  - **Spinlock**

---

### 2. Non–Busy Waiting (Blocking)
- Process is blocked when resource is unavailable
- CPU is freed for other processes
- More efficient than busy waiting

---

## Categories of Synchronization Solutions

### A. Software-Based Synchronization (User Mode)

- Implemented purely using **software logic**
- Does **not require special hardware support**
- Runs in **user mode**
- Uses shared variables and strict ordering rules

#### Core Idea
- Processes coordinate by **checking and updating shared variables**
- Goal is to enforce **mutual exclusion** without hardware help

#### Examples

- **Lock Variables**
  - A shared variable indicates whether the critical section is free
  - Process checks the variable before entering
  - ❌ Not atomic → race conditions possible

- **Strict Alternation**
  - Processes take turns entering the critical section
  - ❌ Forces alternation even when not required
  - ❌ Violates progress condition

- **Peterson’s Solution**
  - Uses:
    - Turn variable
    - Interest flags
  - ✔ Correct for **two processes**
  - ❌ Not scalable
  - ❌ Rarely used in real systems

- **Dekker’s Algorithm**
  - One of the earliest correct solutions
  - Combines strict alternation with flags
  - ❌ Complex
  - ❌ Historical importance only

#### Summary
- ✔ No hardware required
- ❌ Inefficient
- ❌ Not scalable
- ❌ Mostly theoretical

---

### B. Hardware-Based Synchronization

- Uses **special atomic CPU instructions**
- Operations execute **indivisibly**
- Cannot be interrupted mid-operation

#### Core Idea
- Hardware guarantees that certain instructions execute **atomically**
- Prevents race conditions at the lowest level

#### Examples

- **Test-and-Set Lock (TSL)**
  - Reads and sets a value in a single atomic step
  - Used to implement **spinlocks**
  - ✔ Simple
  - ❌ Busy waiting
  - ❌ CPU cycles wasted

- **Swap Instruction**
  - Atomically swaps values between memory and register
  - Used for low-level locking mechanisms

- **Compare-and-Swap (CAS)**
  - Updates a value only if it matches an expected value
  - Foundation of **lock-free programming**
  - ✔ Powerful
  - ❌ Complex
  - ❌ May still involve spinning

#### Summary
- ✔ Fast
- ✔ Atomic
- ❌ Busy waiting
- ❌ CPU inefficiency under contention

---

### C. OS-Based Synchronization (Kernel Support)

- Provided directly by the **operating system**
- Processes **block instead of spinning**
- Implemented using kernel mechanisms

#### Core Idea
- If a process cannot enter the critical section, it is **put to sleep**
- CPU is freed for other processes

#### Examples

- **Sleep and Wakeup**
  - Process sleeps when resource is unavailable
  - Woken up when resource becomes available
  - ❌ Risk of missed wakeups if not handled carefully

- **Semaphores**
  - Integer-based synchronization tool
  - Two atomic operations:
    - `wait (P)`
    - `signal (V)`
  - Used for:
    - Mutual exclusion
    - Resource counting
    - Process coordination

- **Monitors**
  - High-level synchronization construct
  - Automatically enforces mutual exclusion
  - Uses condition variables for coordination
  - ✔ Cleaner and safer than semaphores

#### Summary
- ✔ No busy waiting
- ✔ Efficient CPU usage
- ✔ Scalable
- ✔ Used in real operating systems

---

# Pre-Deadlock Concepts

This section consolidates all concepts required to clearly understand
**Deadlocks**, **Synchronization**, and **Resource Management** in Operating Systems.

---

## 1. Program Execution Models

### Sequential Programs
- Single flow of execution
- Instructions execute one after another
- No overlap in execution
- No race conditions
- No deadlocks
- Poor resource utilization

---

### Concurrent Programs
- Multiple processes or threads are **in progress at the same time**
- Execution may be **interleaved**
- Supported even on a single CPU via context switching
- Requires synchronization
- Can lead to:
  - Race conditions
  - Deadlocks
  - Starvation

> Concurrency is a **logical property**.

---

### Parallel Programs
- Multiple processes or threads execute **simultaneously**
- Requires multiple CPU cores or processors
- Improves performance
- Still requires synchronization
- Deadlocks can still occur

> Parallelism is a **hardware property**.

---

### Key Notes
- A program can be concurrent but not parallel
- A program can be parallel and concurrent
- **Deadlocks arise due to concurrency, not parallelism**

---

## 2. Process vs Thread (Awareness Level)

- **Process**
  - Independent execution unit
  - Own address space

- **Thread**
  - Lightweight execution unit
  - Shares address space with other threads of the same process

> Deadlocks occur more frequently with threads due to shared memory.

---

## 3. Resources in Operating Systems

- A **resource** is any entity required by a process to execute.

### Types of Resources
- **Reusable Resources**
  - CPU
  - Memory
  - Files
  - Locks
  - Devices

- **Consumable Resources**
  - Signals
  - Messages
  - Interrupts

> Deadlocks primarily involve **reusable resources**.

---

## 4. Resource Usage Model

Processes typically follow this sequence:
- **Request** a resource
- **Use** the resource
- **Release** the resource

OS keeps track of:
- Resource ownership
- Resource requests
- Waiting processes

---

## 5. Critical Section

- A **critical section** is a part of code that:
  - Accesses shared resources
  - Must not be executed by more than one process/thread at a time

- Critical sections require:
  - Mutual exclusion
  - Synchronization mechanisms

> Deadlocks often arise from **multiple critical sections and improper lock ordering**.

---

## 8. Starvation vs Deadlock

- **Starvation**
  - Process waits indefinitely due to scheduling policy
  - Resource may become available, but process never gets it

- **Deadlock**
  - Set of processes wait forever for resources held by each other
  - Circular waiting
  - No process can proceed

> Deadlock ≠ Starvation

---

## 9. Why Deadlocks Occur

Deadlocks occur because of:
- Concurrency
- Shared resources
- Blocking synchronization
- Improper resource allocation or ordering

---

## Deadlock

- A **deadlock** is a situation in which **two or more processes are waiting indefinitely**
  for an event that can **never occur**.

### Consequences of Deadlock
- Throughput and efficiency drop
- Ineffective utilization of resources
- System appears to be stuck
- Deadlock is **undesirable**

---

## Necessary Conditions for Deadlock

Deadlock can occur **only if all of the following conditions hold simultaneously**:

1. **Mutual Exclusion**
   - At least one resource must be held in a non-shareable mode
   - Typically involves a critical section or shared resource

2. **Hold and Wait**
   - A process holds at least one resource
   - While waiting to acquire additional resources
   - **Hold and wait alone ≠ deadlock**
   - **Deadlock = all necessary conditions together**

3. **No Preemption**
   - Resources cannot be forcibly taken from a process
   - They must be released voluntarily

4. **Circular Wait**
   - A circular chain of processes exists
   - Each process waits for a resource held by the next process in the chain

> If **all four conditions** are present, a deadlock **may occur**.

---

## Deadlock Handling Strategies

- **Deadlock Prevention**
- **Deadlock Avoidance**
- **Deadlock Detection and Recovery**
- **Deadlock Ignorance**

---

## Deadlock Prevention

Deadlock prevention works by **negating one or more necessary conditions**:

- **Mutual Exclusion**
  - Cannot be eliminated (some resources are inherently non-shareable)

- **Hold and Wait**
  - Prevented by enforcing:
    - **Hold OR Wait**
    - Process must request all resources at once

- **No Preemption**
  - Allow resource preemption
  - Resources can be forcibly taken and reassigned

- **Circular Wait**
  - Prevented by imposing a **total ordering** on resources
  - Processes must request resources in increasing order

---

## Resource Allocation Graph (RAG)

- Used to represent resource allocation and requests

### Single-Instance Resources
- **Cycle is both a necessary and sufficient condition**
  - Cycle ⇒ Deadlock

### Multi-Instance Resources
- **Cycle is only a necessary condition**
  - Cycle ⇏ Deadlock (may or may not occur)

---

## Deadlock Avoidance

Deadlock avoidance ensures the system **never enters an unsafe state**.

### Techniques

- **Single Instance Resources**
  - Resource Allocation Graph (RAG)

- **Multiple Instance Resources**
  - **Banker’s Algorithm**
    - Safety algorithm
    - Resource request algorithm

---

## Deadlock Detection

Deadlock detection allows the system to:
- **Let deadlocks occur**
- Periodically **check** whether a deadlock has happened
- Take action to **recover** from it

This approach is used when:
- Deadlocks are rare
- Prevention or avoidance is too costly

---

### Deadlock Detection Techniques

#### 1. Single-Instance Resources
- Use a **Resource Allocation Graph (RAG)**
- If a **cycle exists**, then:
  - Deadlock has occurred

---

#### 2. Multiple-Instance Resources
- RAG alone is **not sufficient**
- OS uses a **Deadlock Detection Algorithm**
  - Similar in structure to Banker’s Algorithm
  - Checks for processes that cannot finish with available resources

> If one or more processes cannot complete → deadlock exists

---

## Deadlock Recovery

Once a deadlock is detected, the OS must recover.

---

### Recovery Methods

#### 1. Process Termination

- **Abort all deadlocked processes**
  - Simple
  - Expensive
  - Loss of work

- **Abort one process at a time**
  - Re-run detection after each termination
  - Continue until deadlock is resolved

**Process selection criteria:**
- Priority of process
- How long process has executed
- Resources held by the process
- Cost of restarting the process

---

#### 2. Resource Preemption

- Temporarily take resources from some processes
- Give them to other processes to break deadlock

**Issues with resource preemption:**
- Selecting a victim process
- Rollback to a safe state
- Preventing starvation of victim process

---

## Deadlock Ignorance

- OS **ignores deadlocks completely**
- Assumes deadlocks are rare

### Example
- UNIX, Linux, Windows

**Reason:**
- Deadlock handling is expensive
- User or administrator can restart the system/process

> Known as the **Ostrich Algorithm**

---

## Comparison of Deadlock Handling Strategies

| Strategy     | Deadlock Allowed | Overhead | Used In Practice |
|--------------|------------------|----------|------------------|
| Prevention   | ❌ No            | High     | Rare             |
| Avoidance    | ❌ No            | High     | Rare             |
| Detection    | ✔ Yes           | Medium   | Limited          |
| Ignorance    | ✔ Yes           | Low      | Common           |

---

## Common Deadlock Examples

- Two processes holding one lock each and waiting for the other
- Circular file locking
- Nested mutex locking without ordering
- Thread deadlocks in shared memory programs

---

## Final Note

Deadlocks are a **consequence of concurrency, synchronization, and resource sharing**.
Understanding deadlocks helps in:
- Writing correct concurrent programs
- Designing OS kernels
- Avoiding system freezes and performance issues

---

## Memory Management
> Primary (Main) Memory → RAM  
> (Registers and cache are part of the memory hierarchy but are not managed directly by the OS)

---

## Linear One-Dimensional View of Memory

- Main memory is viewed as a **linear array of addressable locations**
- Each location stores a **word** (or byte, depending on architecture)

- If address size is **n bits**, then:
  - Total addressable locations = `2ⁿ`

```text
10 bits → 2¹⁰ words → 1 KW (Kilo Words)
20 bits → 2²⁰ words → 1 MW (Mega Words)
30 bits → 2³⁰ words → 1 GW (Giga Words)
```


---

## System Bus
- A **bus** is a group of wires used to transfer data
- Each wire carries **1 bit**
- Address bus width determines maximum addressable memory

---

## Address Binding

- **Address Binding**
  - Association of program instructions and data with memory addresses
- The **linker** resolves references to:
  - External variables
  - Functions
  - Libraries

---

## Binding Time

- **Binding Time**
  - The time at which logical addresses are mapped to physical addresses

### Types of Binding Time

- **Compile-Time Binding (CT)**
  - Addresses decided at compile time
  - Program must be loaded at a fixed location
  - Purely static

- **Load-Time Binding (LT)**
  - Compiler generates relocatable code
  - Loader assigns physical addresses
  - Some flexibility

- **Run-Time Binding (RT)**
  - Address binding occurs during execution
  - Requires hardware support (MMU)
  - Most flexible and widely used

---

## Types of Address Binding

- **Static Binding**
  - Address association cannot change
  - Used in compile-time binding

- **Dynamic Binding**
  - Address association can change during execution
  - Used in run-time binding

---

## Memory Management Techniques

- **Contiguous Memory Allocation**
  - Each process occupies a single continuous block of memory
  - Simple but inefficient

- **Non-Contiguous Memory Allocation**
  - Process memory is divided and placed at different locations
  - Efficient and scalable

---

## Traditional (Older) Memory Management Techniques

These techniques were developed when **main memory was very limited** and hardware support
for advanced memory management (MMU, paging) was minimal or absent.

---

## 1. Overlays

### Concept
- A program is divided into **logical modules**
- Only the **required module** is loaded into memory at a time
- Remaining modules stay on secondary storage

### How it Works
- Program is manually structured into overlays by the programmer
- When one module finishes execution:
  - It is replaced by another required module
- Overlays share the **same memory region**

### Why It Was Used
- Memory was extremely limited
- Programs were larger than available RAM

### Problems
- Programmer must manage overlays manually
- No automatic support from OS
- Complex program design
- Obsolete in modern systems

---

## 2. Partitioning

Memory is divided into **partitions**, and each partition can hold a process.

---

### A. Fixed Partitioning

#### Concept
- Main memory is divided into **fixed-size partitions**
- One process occupies one partition
- Number of processes in memory is limited by number of partitions

#### Characteristics
- Simple to implement
- Easy process allocation and deallocation

#### Problems
- **Internal Fragmentation**
  - Process may not use all memory of the partition
- Limited degree of multiprogramming
- Inefficient memory utilization

---

### B. Variable Partitioning

#### Concept
- Memory is divided into **variable-size partitions**
- Each process is allocated exactly the memory it needs

#### Characteristics
- Better memory utilization than fixed partitioning
- Flexible allocation

#### Problems
- **External Fragmentation**
  - Free memory is split into small non-contiguous holes
- Requires:
  - Compaction (expensive)
  - Relocation support

---

## 3. Buddy System

### Concept
- Memory is managed in blocks of size **2ⁿ**
- When a request arrives:
  - OS finds the smallest block large enough
  - Larger blocks are split recursively

### How it Works
- Each block has a **buddy**
- Two buddies can be merged if both are free
- Merging continues until the largest possible block is formed

### Advantages
- Fast allocation and deallocation
- Easier coalescing than variable partitioning

### Problems
- **Internal Fragmentation**
  - Process rarely fits exactly into 2ⁿ size
- Less flexible than paging

### Usage
- Used in kernel memory allocators
- Example: Linux buddy allocator (for physical memory)

---

## Summary Comparison

| Technique            | Fragmentation Type | Programmer Effort | OS Complexity | Modern Use |
|---------------------|--------------------|-------------------|---------------|------------|
| Overlays             | None (manual)      | High              | Low           | ❌ No |
| Fixed Partitioning   | Internal           | Low               | Low           | ❌ No |
| Variable Partitioning| External           | Low               | Medium        | ❌ No |
| Buddy System         | Internal           | Low               | Medium        | ✔ Limited |

---

## Modern Memory Management Techniques

Modern memory management techniques were developed to:
- Improve memory utilization
- Support multiprogramming
- Provide memory protection
- Allow programs larger than physical memory
- Reduce fragmentation

---

## 1. Paging

### Concept
- Logical memory is divided into **fixed-size blocks called pages**
- Physical memory is divided into **fixed-size blocks called frames**
- Page size = Frame size

### How Paging Works
- A process is divided into pages
- Pages are loaded into any available frames in physical memory
- OS maintains a **page table** to map:
  - Page number → Frame number

### Address Translation in Paging
- Logical address = (Page number, Offset)
- Physical address = (Frame number, Offset)

### Advantages
- **Eliminates external fragmentation**
- Efficient memory utilization
- Supports virtual memory
- Simplifies memory allocation

### Problems
- **Internal fragmentation** (unused space in last page)
- Page table overhead
- Requires hardware support (MMU)

---

## 2. Segmentation

### Concept
- Memory is divided into **logical segments** based on program structure
- Each segment represents a logical unit:
  - Code
  - Data
  - Stack
  - Heap

### How Segmentation Works
- Each segment has:
  - Base address
  - Limit (size)
- Logical address = (Segment number, Offset)
- Segment table maps segment numbers to base and limit

### Advantages
- Matches programmer’s view of memory
- Supports:
  - Protection
  - Sharing
- Easy to grow or shrink segments (e.g., stack)

### Problems
- **External fragmentation**
- Requires compaction
- Complex memory management

---

## 3. Segmented Paging

### Concept
- Combines advantages of **segmentation** and **paging**
- Segments are divided into pages

### How It Works
- Logical address consists of:
  - Segment number
  - Page number
  - Offset
- Segment table points to page tables
- Page tables map pages to frames

### Advantages
- Logical view of segmentation
- Efficient allocation of paging
- Better protection and sharing

### Problems
- Increased complexity
- More memory overhead
- Slower address translation

---

## 4. Demand Paging

### Concept
- Pages are loaded into memory **only when required**
- Not all pages of a process need to be in memory at once

### How Demand Paging Works
- If a process references a page not in memory:
  - **Page Fault** occurs
  - OS loads the required page from disk into memory

### Advantages
- Programs can be larger than physical memory
- Reduced memory usage
- Faster process startup

### Problems
- Page faults are expensive
- Poor performance if page faults are frequent
- Requires good page replacement algorithms

---

## Relation to Virtual Memory

- Demand paging is the **foundation of virtual memory**
- Virtual memory provides:
  - Illusion of large memory
  - Process isolation
  - Efficient multiprogramming

---

## Comparison Summary

| Technique         | Fragmentation Type | Flexibility | Hardware Support | Modern Use |
|------------------|--------------------|-------------|------------------|------------|
| Paging            | Internal           | High        | Required         | ✔ Yes |
| Segmentation      | External           | Medium      | Required         | Limited |
| Segmented Paging  | Internal           | Very High   | Required         | Limited |
| Demand Paging     | Internal           | Very High   | Required         | ✔ Yes |

---

## Functions of Memory Manager

The **Memory Manager** is a core component of the Operating System responsible for
managing main memory efficiently and safely.

Its primary functions are:

---

### 1. Allocation

- Assigns memory space to processes when they are created
- Decides:
  - How much memory to allocate
  - Where to allocate it in main memory

- Allocation depends on:
  - Memory management technique (paging, segmentation, etc.)
  - Availability of free memory

> Goal: Efficient utilization of limited main memory.

---

### 2. Protection

- Ensures that one process **cannot access another process’s memory**
- Prevents:
  - Accidental data corruption
  - Malicious memory access

- Implemented using:
  - Base and Limit registers
  - Page-level protection bits (read/write/execute)
  - MMU checks on every memory access

> Every memory access is validated before execution.

---

### 3. Free Space Management

- Keeps track of unused memory
- Required to efficiently allocate memory to new processes

- Techniques include:
  - Bitmaps
  - Free lists
  - Buddy system

> Poor free space management leads to fragmentation.

---

### 4. Address Translation

- Converts **logical (virtual) addresses** generated by the CPU
  into **physical addresses** in main memory

- Performed by:
  - Memory Management Unit (MMU)

#### Address Translation Flow
```text
CPU
|
| Logical Address
v
MMU
|
| Physical Address
v
Main Memory (RAM)
```


> Address translation enables protection, relocation, and virtual memory.

---

### 5. Deallocation

- Frees memory when:
  - A process terminates
  - A process is swapped out

- Updates internal data structures:
  - Free lists
  - Bitmaps
  - Page tables

> Prevents memory leaks and starvation.

---

## Address Space

An **Address Space** is the range of memory addresses that a process can use.

---

### Logical Address Space (Virtual Address Space)

- Generated by the CPU
- Used by programs
- Independent of actual physical memory layout
- Each process has its **own logical address space**

> Provides isolation and security.

---

### Physical Address Space

- Actual addresses in main memory (RAM)
- Shared among all processes
- Accessed only after address translation

---

## Logical vs Physical Address Space

```text
Process
|
| Logical Address Space
v
+-------------------+
| Virtual Memory |
+-------------------+
|
| Address Translation
v
+-------------------+
| Physical Memory |
+-------------------+
```

---

## Why Address Spaces are Important

- Enable:
  - Process isolation
  - Protection
  - Relocation
  - Virtual memory

- Allow multiple processes to:
  - Believe they own the entire memory
  - Safely coexist in the system

---

## Design & Implementation of NCG Techniques
### Organization of Logical Address Space (LAS), Physical Address Space (PAS) & MMU

Non-Contiguous Memory Management (NCG) allows a process to be stored
in multiple non-adjacent locations in physical memory.
Paging is the simplest NCG technique.

---

## Simple Paging (Example-Based Explanation)

### Given
- Logical Address Space (LAS) = **8 KB**
- Physical Address Space (PAS) = **4 KB**
- Page Size (PS) = **1 KB**

---

### Address Size Calculation

- LAS = 8 KB = 2¹³ bytes → **Logical Address = 13 bits**
- PAS = 4 KB = 2¹² bytes → **Physical Address = 12 bits**

---

## Organization of Logical Address Space (LAS / Virtual Space)

- LAS is divided into equal-sized units called **pages**
- Page size = **1 KB = 2¹⁰ bytes**

### Number of Pages
- N = LAS / Page Size
- N = 8 KB / 1 KB = 8 pages


### Logical Address Structure
- Page offset (d) = log₂(Page size) = **10 bits**
- Page number (p) = log₂(Number of pages) = log₂(8) = **3 bits**

### Logical Address Format
```text
  13-bit Logical Address

    3 bits    10 bits
+---------+---------------+
| Page No | Page Offset |
+---------+---------------+
    p           d
```

> Logical Address = (Page Number, Offset)

---

## Organization of Physical Address Space (PAS)

- PAS is divided into equal-sized units called **frames**
- Frame size = Page size = **1 KB**

### Number of Frames
- M = PAS / Frame Size
- M = 4 KB / 1 KB = 4 frames

### Physical Address Structure
- Frame offset = Page offset = **10 bits**
- Frame number (f) = log₂(Number of frames) = log₂(4) = **2 bits**

### Physical Address Format
```text
  12-bit Physical Address

    2 bits    10 bits
+---------+---------------+
| Frame No| Frame Offset |
+---------+---------------+
      f          d
```

> Physical Address = (Frame Number, Offset)

---

## Organization of MMU (Page Table)

- Each process has its **own page table**
- Page tables are stored in **main memory**
- Page table maps:
  - **Page Number → Frame Number**

### Page Table Characteristics
- Number of entries = Number of pages = **8**
- Each entry stores:
  - Frame number
  - Protection bits (read/write/execute)
  - Valid/invalid bit

### Page Table Size
- Page Table Size = Number of Pages × Size of Each Entry
- PT Size = N × E bytes

---

## Address Translation Using Paging

### Translation Steps
1. CPU generates logical address (p, d)
2. Page number (p) is used to index page table
3. Frame number (f) is obtained
4. Physical address = (f, d)

### Translation Flow Diagram
```
CPU
|
| Logical Address (p, d)
v
Page Table
|
| Frame Number (f)
v
MMU
|
| Physical Address (f, d)
v
RAM
```

---

## Why Paging Works Well

- Eliminates **external fragmentation**
- Allows non-contiguous allocation
- Simplifies memory allocation
- Supports virtual memory

---

## Limitations of Simple Paging

- Page table consumes memory
- Every memory access may require:
  - Page table lookup
- Leads to performance overhead
  - Solved using **TLB** (Translation Lookaside Buffer)

---

## Performance of Paging

Paging introduces an extra level of memory access due to address translation.
Understanding its performance impact is critical.

---

## Timing Issues in Paging

- The **page table is stored in main memory**
- Let:
  - `m` = main memory access time (nanoseconds)

### Without TLB
For every memory access:
1. Access page table → `m`
2. Access actual memory → `m`

### Effective Memory Access Time (EMAT)
```
EMAT = m + m = 2m
```

---

## Paging Access Flow (Without TLB)
```
CPU
|
| Virtual Address
v
Main Memory (Page Table) -- m -->
|
| Physical Address
v
Main Memory (Data) -- m -->
|
v
Data
```

> Paging doubles memory access time → **performance degradation**

---

## Improving Paging Performance

Goal:
> Make **EMAT ≈ m**

This is achieved using **TLB (Translation Lookaside Buffer)**.

---

## Translation Lookaside Buffer (TLB)

- TLB is a **small, fast cache**
- Stores **recent page table entries**
- Located inside or very close to the MMU
- Access time `c`, where:
```
c << m
```

---

## Paging Access Flow (With TLB)
```
CPU
|
| Virtual Address
v
+------------------+
| TLB |
+------------------+
| Hit | Miss
v v
Physical Addr Page Table (m)
| |
| v
| Physical Addr
| |
v v
Main Memory (m) Main Memory (m)
```

---

## Effective Memory Access Time (With TLB)

Let:
- `h` = TLB hit ratio

### EMAT Formula
```
EMAT = h × (c + m) + (1 − h) × (c + m + m)
```

### Interpretation
- High hit ratio → EMAT approaches `m`
- Low hit ratio → EMAT approaches `2m`

---

## Key Points about TLB

- Uses **parallel search**
- Stores:
  - Page number
  - Frame number
  - Protection bits
- On context switch:
  - TLB entries must be flushed or tagged (ASID)

---

## Hashed Paging

### Why Hashed Paging?
- Large address spaces → huge page tables
- Hashing reduces lookup time

---

### How Hashed Paging Works

- Virtual page number is hashed
- Hash table entry points to:
  - Frame number
  - Next entry (for collisions)

---

### Hashed Paging Diagram
```
Virtual Page No
|
v
Hash Function
|
v
Hash Table Bucket
|
+--> (VPN, Frame) -> Next -> ...
```

---

### Collision Resolution Techniques

- **Chaining**
  - Linked list of entries
- **Probing**
  - Check next available slot (less common in OS paging)

---

## Multilevel Paging (Hierarchical Paging)

### Why Multilevel Paging?
- Single-level page table is too large
- Most processes use only a small portion of address space

---

### Concept
- Page table itself is **paged**
- Only required portions are kept in memory

---

### Address Structure (Two-Level Paging Example)
```
| Page Directory | Page Table | Offset |
```

---

### Multilevel Paging Diagram
```
CPU
|
| Virtual Address
v
Page Directory
|
v
Page Table
|
v
Frame Number
|
v
Main Memory
```

---

### Advantages
- Reduces memory used by page tables
- Scales well for large virtual address spaces

### Disadvantages
- Multiple memory accesses without TLB
- More complex address translation

---

## Comparison Summary

| Technique        | Purpose                         | Advantage                     | Limitation                |
|------------------|----------------------------------|-------------------------------|---------------------------|
| Simple Paging    | Basic mapping                   | Easy to implement             | Large page tables         |
| TLB              | Speed up translation            | EMAT ≈ m                      | Limited size              |
| Hashed Paging    | Large address spaces            | Faster lookup                 | Collision handling        |
| Multilevel Paging| Reduce page table size          | Memory efficient              | Extra translation steps   |

---

## Segmentation

Segmentation is a memory management technique that:
- Preserves the **user’s logical view of memory**
- Divides a program into **logical units** called segments

Examples of segments:
- Code
- Data
- Stack
- Heap

---

## Why Paging Alone Is Not Enough

- Paging divides memory into fixed-size pages
- Pages do **not correspond to logical program units**
- Hence, paging **does not preserve the user’s view of memory**

Segmentation solves this by matching memory allocation to program structure.

---

## Organization of Segmentation

- Each segment is stored **contiguously**
- Different segments may be placed at **non-contiguous locations** in physical memory

### Segment Table
Each process has a **segment table**.
Each entry contains:
- **Base** → starting physical address of the segment
- **Limit** → size of the segment

---

## Logical Address Format (Segmentation)
  ```
  Logical Address

  Segment No Offset
  +-----------+-----------+
  |     s     |     d     |
  +-----------+-----------+
```


- `s` → segment number (index into segment table)
- `d` → offset within the segment

---

## Address Translation in Segmentation
```
CPU
|
| Logical Address (s, d)
v
Segment Table
|
| Base + Offset (if d < Limit)
v
Physical Memory
```


- If `d > limit` → **Segmentation Fault**

---

## Performance of Segmentation

### Time
- One access to segment table → `m`
- One access to main memory → `m`

Effective Memory Access Time = 2m

---

### Space
- Segment table can become large
- To reduce space overhead:
  - **Paging is applied to the segment table**

---

## Segmented Paging

Segmented paging combines:
- **Segmentation** (logical view)
- **Paging** (efficient allocation)

### How It Works
- Each segment is divided into pages
- Segment table entry points to a **page table**
- Pages are stored in frames

---

## Segmented Paging Address Format
```
| Segment | Page | Offset |
```

---

## Fragmentation Comparison

- **Paging**
  - Internal fragmentation (last page)
  - No external fragmentation

- **Segmentation**
  - External fragmentation
  - No internal fragmentation

- **Segmented Paging**
  - Internal fragmentation only
  - No external fragmentation

---

## Virtual Memory

Virtual Memory allows execution of programs that are:
- Larger than available physical memory

It provides an **illusion of large memory** to the programmer.

---

## Implementation of Virtual Memory

Virtual memory is implemented using **Demand Paging**.

### Demand Paging
- Pages are loaded into memory **only when required**
- Unused pages remain on disk

---

## Page Fault Handling (Step-by-Step)

1. Process references a page not present in memory
2. **Page Fault** occurs
3. Mode switches to kernel
4. **Virtual Memory Manager (VMM)** takes control
5. Disk manager is invoked to locate required page

If free frame exists:
Load page → Update page table → Unblock process
Else:
Page replacement required

---

## Page Replacement

When no free frame is available, OS must replace a page.

### Reference String
- Sequence of page numbers accessed by a process
- Used to evaluate page replacement algorithms

---

## Page Replacement Algorithms

- **Optimal Replacement**
  - Replaces page that will not be used for the longest time
  - Best performance (theoretical)

- **Least Recently Used (LRU)**
  - Replaces page least recently accessed
  - Good approximation of optimal

- **Most Recently Used (MRU)**
  - Replaces most recently used page
  - Useful in special workloads

- **Counting Algorithms**
  - **LFU (Least Frequently Used)**
  - **MFU (Most Frequently Used)**

---

## Reference Bits

- **Reference Bit**
  - Set when a page is accessed
  - Used to approximate LRU

- **Additional Reference Bits**
  - Multiple bits per page
  - Better history of page usage

---

## Frame Allocation Policies

- **Equal Allocation**
  - Each process gets equal frames

- **Proportional Allocation**
  - Frames allocated based on process size

- **50% Rule**
  - Working set usually occupies about half of allocated frames

---

