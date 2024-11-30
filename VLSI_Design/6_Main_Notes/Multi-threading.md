1. [[Mutex Vs. Semaphores]]
2. [[Concurrency, Threading and Parallelism]]
3. [[Hardware Threads]]

# Overview

Multithreading allows efficient parallel computing by enabling multiple threads within a process to execute simultaneously, optimizing resource usage.

- **Parallel Computing**: Multithreading facilitates efficient execution by running multiple threads at once.
- **Process vs. Thread**: A process has its own address space; threads share the parent’s space, making them lightweight.
- **Execution Context**: Threads represent different execution contexts within a process, allowing concurrent operations.
- **Synchronization Constructs**: Mechanisms like mutexes and semaphores ensure safe access to shared resources among threads.
- **Memory Efficiency**: Threads consume less memory than processes, making them suitable for applications with high concurrency needs.
- **Trade-offs**: While multithreading offers benefits, it requires careful management of synchronization to avoid issues.
- **Complexity Management**: While multithreading can optimize performance, it introduces complexity that necessitates a solid grasp of synchronization techniques to mitigate potential issues.

# Multi-threading: Hardware vs Software Threads

When discussing a **multi-threaded processor**, it’s essential to differentiate between **hardware threads** and **software threads**. Here’s a detailed explanation:

---

## 1. **Hardware Threads**
- **Definition**: Hardware threads refer to the **physical capability** of a processor to manage multiple threads of execution concurrently. 
- **Mechanism**: This is achieved through **Simultaneous Multithreading (SMT)** or similar technologies.
- **Key Idea**: Multiple threads share resources (like ALUs, caches, or execution units) within a single physical core. 
- **Objective**: To maximize the utilization of the core's resources.

### Characteristics:
1. **Shared Resources**:
   - Threads within a single core share execution units, caches, and pipelines.
   - These threads take advantage of idle cycles caused by cache misses or branch mispredictions.
   
2. **Appears as Multiple CPUs**:
   - To the operating system, each hardware thread looks like an independent processor.
   - E.g., a single core with SMT enabled may appear as two logical processors.

3. **Limited Number**:
   - The number of hardware threads is fixed and determined by the processor architecture.
   - Example: A 4-core processor with SMT supporting 2 threads per core provides 8 hardware threads.

### Examples of SMT in Real-World Processors:
1. **Intel Hyper-Threading Technology (HTT)**:
   - Found in Intel Core i7, i9, and Xeon processors.
   - Each core can handle 2 hardware threads simultaneously.

2. **AMD Simultaneous Multithreading (SMT)**:
   - Found in AMD Ryzen and EPYC processors.
   - Allows 2 threads per core for efficient resource utilization.

3. **IBM POWER9**:
   - Supports up to 8 hardware threads per core.
   - Used in high-performance servers and supercomputers.

4. **ARM Cortex-A77 (in DynamIQ setups)**:
   - SMT is not common in most ARM processors but is used in specific designs for server-grade ARM cores.

---

## 2. **Software Threads**
- **Definition**: Software threads are **logical constructs** created and managed by the operating system or application.
- **Mechanism**: The OS scheduler maps these threads to hardware threads for execution.
- **Objective**: To divide a program into multiple independent tasks that can execute concurrently.

### Characteristics:
1. **Not Limited by Hardware**:
   - There can be more software threads than hardware threads or cores.
   - Excessive threads can lead to **context-switching overhead**.

2. **Managed by the OS**:
   - The operating system handles scheduling, pausing, and resuming threads.
   - Threads can run on any available hardware thread.

3. **Portability**:
   - Software threads are portable across different processor architectures, unlike hardware threads.

---

## 3. **How Hardware and Software Threads Interact**
The relationship between hardware and software threads determines system performance.

### Example Scenario:
- **Processor**: A quad-core processor with SMT (2 hardware threads per core) = 8 hardware threads.
- **Application**: Creates 16 software threads.
- **OS Behavior**:
  - The OS scheduler maps 16 software threads to 8 hardware threads.
  - If all software threads are active, context switching occurs, introducing overhead.

---

## 4. **Key Differences**

| Aspect                 | Hardware Threads                          | Software Threads                           |
|------------------------|------------------------------------------|------------------------------------------|
| **Definition**          | Threads managed by the processor's hardware. | Threads created by software (OS or application). |
| **Resource Sharing**    | Share core resources (ALUs, pipelines).   | Depend on OS scheduler to share resources. |
| **Fixed/Variable**      | Fixed, defined by processor architecture. | Variable, can exceed hardware capabilities. |
| **Efficiency**          | Maximizes core utilization.              | Can introduce overhead if excessive.      |
| **Visibility to OS**    | Appear as independent processors.         | Mapped to available hardware threads.     |

---

## 5. **Real-World Examples**

### Intel Hyper-Threading
- Found in **Intel Core i7-12700K**:
  - **12 cores** (8 performance cores + 4 efficiency cores).
  - Performance cores support SMT: 2 threads per core.
  - Total = **20 threads** visible to the OS.

### AMD Ryzen 9 5900X
- 12 cores, **2 threads per core**.
- Total = **24 threads** visible to the OS.

### IBM POWER9
- High-end servers use processors with **8 threads per core**.
- Designed for workloads like databases and scientific computing.

---

## 6. **Advantages of SMT**
- **Increased Throughput**:
  - SMT keeps execution units busy even during stalls (e.g., cache misses).
  
- **Improved Resource Utilization**:
  - Multiple threads can use idle resources in a single core.

- **Better Performance in Multi-Tasking**:
  - SMT excels in workloads with many lightweight threads.

---

## 7. **Limitations of SMT**
1. **Resource Contention**:
   - Hardware threads share resources, leading to potential contention.
   
2. **Performance Variability**:
   - SMT doesn’t provide a linear performance boost (e.g., 2x threads ≠ 2x performance).

3. **Power and Complexity**:
   - SMT increases power consumption and design complexity.

---

## 8. **Separate Compute Units**
**Separate Compute Units** are not required for SMT. Multiple hardware threads can exist on a single core, sharing resources. However, if compute units (like cores) are physically separate, they operate independently.

### Example:
- **Multi-core Processor**: 4 cores, no SMT → 4 hardware threads.
- **Multi-core with SMT**: 4 cores, SMT (2 threads/core) → 8 hardware threads.

---

## Conclusion
When we say a processor is "multi-threaded," it often refers to **hardware threads** because this describes the architectural capability of the processor. However, software threads play a crucial role in utilizing hardware threads effectively.
