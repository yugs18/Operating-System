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

