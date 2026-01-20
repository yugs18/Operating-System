# Operating system - personal notes

These notes are written to solidify my understanding of Operating systems while studying OS theory.

---

## What is an Operating Systems?

- Interface between user(programmer) & computer.

    User - OS(interface) - hardware

- Basic Structure
```
                Compontes of Hardware
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
    Compipler
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
