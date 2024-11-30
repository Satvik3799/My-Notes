
An ABI ensures that programs compiled by different compilers or written in different languages can work together seamlessly if they adhere to the same ABI.

# RISC-V Compiler Arguments Guide

## Key Arguments
Three main compiler arguments for RISC-V:
- `-march`: Architecture specification
- `-mabi`: Application Binary Interface specification
- `-mtune`: Microarchitecture optimization

- `-march` tells WHAT instructions can be used
- `-mabi` tells HOW to use them, especially for function calls

 Think of it this way:

- `-march` is like saying "I have a car with automatic transmission"
- `-mabi` is like saying "I will drive it in sport mode or eco mode"

## 1. `-march` (Architecture)
### Base ISAs
- `RV32I`: 32-bit ISA, 32 integer registers
- `RV32E`: Embedded 32-bit ISA, 16 integer registers
- `RV64I`: 64-bit ISA, 64-bit registers

### Extensions
- `M`: Integer Multiplication/Division
- `A`: Atomic Instructions
- `F`: Single-Precision Float
- `D`: Double-Precision Float
- `C`: Compressed Instructions

Example: `-march=rv32im` (32-bit with multiplication)

## 2. `-mabi` (ABI)
### Integer ABI Options
- `ilp32`: 32-bit int/long/pointers
- `lp64`: 64-bit long/pointers, 32-bit int

### Floating-Point ABI Options
- `""`: No FP in registers
- `f`: 32-bit FP in registers
- `d`: 64-bit FP in registers

## Common Combinations
| Command | Description |
|---------|-------------|
| `-march=rv32imafdc -mabi=ilp32d` | Full HW floating-point |
| `-march=rv32imac -mabi=ilp32` | No floating-point |
| `-march=rv32imafdc -mabi=ilp32` | HW float available but unused |

## Usage Example
```bash
riscv64-unknown-elf-gcc source.c -march=rv64imafdc -mabi=lp64d
```

## Note
- ABI must match between linked objects
- Extensions are appended to base ISA in order (M,A,F,D,C)
- Hardware must support all specified extensions


# Compilation Flow: From C Code to Execution

---

## 1. Writing Code in C
- You write the program in a high-level language like **C**.
- The source code is architecture-independent (it does not care about the underlying hardware specifics).

---

## 2. Compilation Process
### a. Conversion to Assembly Language
- The **compiler** (e.g., `riscv64-unknown-elf-gcc`) translates the C code into **assembly language** instructions for the target ISA (Instruction Set Architecture), like **RISC-V**.
- The assembly code adheres to the **ABI**:
  - Determines how function arguments and return values are passed (e.g., registers or stack).
  - Aligns and sizes data types correctly (e.g., pointers are 64-bit for `lp64`).

### b. Architecture-Specific Assembly
- The assembly language uses instructions available in the target ISA (e.g., `RV64I` for 64-bit integer operations).
- The ABI ensures this assembly is compatible with any RISC-V hardware or software that adheres to the same ABI.

---

## 3. Assembly to Machine Code
- The **assembler** converts the assembly code into **machine code**, which consists of binary instructions understood by the hardware.
- This machine code is specific to the **microarchitecture** (e.g., an RV64 core with optimizations for branch prediction or cache).

---

## 4. Microarchitecture-Specific Optimizations
- The **`-mtune` flag** in the compiler (if used) allows fine-tuning for a specific microarchitecture.
- For example:
  - Some RISC-V CPUs might execute instructions faster if they're reordered or pipelined in a certain way.
  - The compiler applies optimizations specific to the microarchitecture.

---

## 5. Execution on Hardware
- The machine code is loaded into the hardware's memory and executed by the CPU.
- The CPU executes instructions based on its **microarchitecture implementation** of the ISA.

---

## Flow Summary
1. **C Code** → High-level logic.
2. **Compiler**:
   - Converts C → **Assembly (ISA-specific)**, adhering to the ABI.
   - Applies optimizations for performance.
3. **Assembler**: Converts assembly → **Machine Code**.
4. **Hardware**: Executes machine code using its **microarchitecture**.

---

## Example with RISC-V

Let’s say your C code contains:
```c
int sum(int a, int b) {
    return a + b;
}
```

#### Compiled Assembly (Adhering to ABI):


`sum:     add a0, a0, a1   # Add registers a0 and a1 (ABI convention for argument passing)     ret              # Return`

#### Machine Code (For RISC-V ISA):


`0000000 ADD A0, A1 0100001 RET`

#### Microarchitecture Execution:

- The RISC-V CPU interprets these binary instructions, optimizing their execution based on the hardware design (e.g., pipelining, out-of-order execution).

---

### In Conclusion

- **ABI** governs how code components interact at a binary level (e.g., passing arguments in registers).
- **ISA** defines the set of instructions the compiler can use.
- **Microarchitecture** determines how these instructions are executed for optimal performance.


### **1. Definition**

| **Aspect**      | **ABI**                                                                                                   | **ISA**                                                                                         |
| --------------- | --------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **What is it?** | A set of rules governing how software components interact at the binary level.                            | A specification of the set of instructions a processor can execute.                             |
| **Scope**       | Focuses on software-level compatibility (function calls, data layout, etc.).                              | Focuses on hardware-level compatibility (instructions, registers, etc.).                        |
| **Purpose**     | Ensures that binaries (e.g., libraries, executables) can work together seamlessly, even across compilers. | Ensures that software written for a specific ISA can run on any hardware implementing that ISA. |

### **2. Focus and Responsibilities**

| **Aspect**               | **ABI**                                                                                                    | **ISA**                                                                                                            |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Calling Conventions**  | Specifies how functions pass arguments and return values (e.g., via stack or registers).                   | Does not deal with calling conventions.                                                                            |
| **Data Type Layout**     | Defines how data types (e.g., `int`, `long`, `float`) are laid out in memory and their sizes.              | Specifies which instructions exist to operate on data types.                                                       |
| **Registers**            | Specifies which registers are used for function arguments, return values, and which registers need saving. | Defines the complete set of registers (e.g., general-purpose, special-purpose) in the architecture.                |
| **Binary Compatibility** | Ensures compiled binaries work with other binaries or the OS on the same architecture.                     | Ensures software targeting an ISA can run on any processor implementing that ISA, regardless of microarchitecture. |
| **Hardware-Specific?**   | No, it's an agreement for binary-level software compatibility.                                             | Yes, it's tied to hardware because it defines the processor's capabilities.                                        |

---

### **3. Examples**

#### **ABI**

- **`lp64` (Linux on 64-bit systems)**:
    - **Pointers**: 64-bit
    - **Long**: 64-bit
    - **Int**: 32-bit
- Defines how arguments are passed in registers (e.g., `a0` and `a1` in RISC-V).
- Ensures interoperability between binaries compiled by different compilers for the same platform.

#### **ISA**

- **`RISC-V ISA (RV32I, RV64I)`**:
    - Specifies instructions like `ADD`, `SUB`, and `LW`.
    - Defines 32 or 64-bit general-purpose registers.
    - Describes the behavior of special instructions (e.g., memory load/store, branching).

---

### **4. Relation Between ABI and ISA**

- The **ABI** operates on top of the **ISA**.
    - The **ISA** provides the foundation (e.g., instructions, registers).
    - The **ABI** determines how the ISA features are used for interoperability (e.g., which registers hold function arguments).

For example:

- The **ISA** defines that RISC-V has registers `a0` to `a7`.
- The **ABI** specifies that `a0` is used for the first argument in a function call and `a1` for the second.