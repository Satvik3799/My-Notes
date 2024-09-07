07-09-2024 18:37

Status:

Tag:


# TI_IIITH

### Overview of Memory Scheduling Algorithms:

When processes request memory, the operating system must decide where in memory to allocate the requested block. Different algorithms are used to select the most appropriate free memory blocks.

#### 1. **First Fit**:

- **How it works**: The OS scans memory from the beginning and allocates the first block large enough for the process.
- **Advantages**: Simple and fast, as it stops searching as soon as it finds a suitable block.
- **Disadvantages**: Can leave small, unusable gaps (fragmentation) in memory, reducing efficiency over time.

#### 2. **Best Fit**:

- **How it works**: The OS looks for the smallest free block that can fit the requested memory.
- **Advantages**: Minimizes wasted space by using the smallest available block, improving memory utilization.
- **Disadvantages**: Slower than First Fit because it needs to scan all free blocks to find the best match. May lead to many small unusable gaps (external fragmentation).

#### 3. **Worst Fit**:

- **How it works**: The OS allocates the largest free block for the process, hoping to leave larger remaining blocks for future allocations.
- **Advantages**: Can reduce fragmentation in theory by leaving bigger free blocks.
- **Disadvantages**: Often results in inefficient use of memory, as smaller requests can scatter large blocks, worsening fragmentation.

#### 4. **Next Fit**:

- **How it works**: Similar to First Fit, but it continues the search for a suitable block from where the last allocation occurred, not from the start.
- **Advantages**: Faster than Best Fit, especially in systems with frequent allocations, as it doesn’t always start searching from the beginning.
- **Disadvantages**: Like First Fit, it can leave small gaps.

### Fragmentation:

A key challenge for these algorithms is **fragmentation**:

- **Internal fragmentation**: Occurs when more memory is allocated than needed by a process.
- **External fragmentation**: Occurs when there are free blocks of memory, but they are too small to satisfy new allocation requests.




## Question

A series RLC circuit is excited by a 10V sinusoidal voltage source of variable frequency. It is observed that the circuit exhibits resonance at 100 Hz and has a 3 dB bandwidth of 5 Hz.

What will be the voltage across the inductor \( L \) at resonance?

## Hint

To find the voltage across the inductor at resonance, first calculate the quality factor \( Q \) of the circuit using the formula:
$[ Q = \frac{f_0}{\Delta f} ]$
where ( $f_0$ ) is the resonance frequency and ( $\Delta f$ ) is the bandwidth. Then, use the fact that the voltage across the inductor at resonance is \( Q \) times the source voltage.





# References:

