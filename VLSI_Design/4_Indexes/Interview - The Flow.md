# The Flow

## [[Introduction]]

 My name is Satvik Patel, and I’m from Gujarat. I have 1 year of experience as an Embedded Hardware Design Engineer in a start-up, where I worked on PCB design and debugging for Smart Home products based on ESP32 microcontrollers. My role also involved tasks like component sourcing, talking to PCB manufacturers for the design requirement, soldering, and 3D printing boxes for our products. This fueled my passion for electronics and I started rebuilding some electronics products on my own. Now, I don't go to 3rd party repairs even for my laptop, I do it on my own.  I have also done some freelance projects for the company, that was its 2nd source of revenue. I also got to Reverse engineer one product from Atomberg, to integrate with our own and pitch the idea to them. I really enjoyed doing all that, it allowed me to learn from very diverse set of people.
	
 **Why VLSI then, and not embedded?**
	I started taking interest in Electronics when I was in my UG 3rd year, where I had a course on VLSI. I use to look under electronic product casings to see what's there and try to make some sense of it. VLSI gave a new POV that I never had. It made me curious about what is there inside that black box. I used to never reach out to my professors, but I couldn't help but ask questions on this topic. The professor introduced me to FPGAs and how they are used to prototype Processors. I did some courses on designing them, the first one was "From NAND to Tetris". During my job, there were also some projects related to FPGAs. Similar to what a Zynq SoC is, the processing side and the Programmable Logic sidde, they were working on a design that did something similar but on the PCB level. They had an Quad Core ARM cortex A series processor and phsically separate Effinix FPGA. It is starting to pick up right now, the name of the board is Vaaman. The company's name is Vicharak, but CEO is same and we handled projects for both companies. Also, we used to meet on weekends to teach eachother some peculiar things they thought was unique. It could be anything, a product idea, a research paper, teaching a software like github etc. So the software guys would teach linux and github. In one of these sessions I got introduced to VLIW architecture. and I couldn't make much sense of the things they were teaching. So I decided to give the enterance test again and decided to pursue masters. I looked for specific curriculum that would allow me to be related to the FPGAs and Architectural stuff. And Here I am now.
	
 **Hobbies:** 
	I enjoy sports like cricket, badminton, and table tennis, and I’ve represented my college during my B.Tech days. I also love playing computer games, especially Counter-Strike. It is said that this game is Chess with Guns. And I believe it to be true because it has taught me to stay calm under pressure, strategize, and execute with precision. 
	
Please let me know, if there's something you'd like to know about me.

## [[MTP Project and Seminar]] 

 The final goal of the project is to realise an AJIT SoC, that is specific for Cryptography only, by  removing some peripherals that would not be needed for any Cryptographic operation. The SoC is to be used in the field of Post Quantum Cryptography or PQC for short and Fully Homomorphic Encryption, FHE for short, methods. These methods use polynomial multiplication extensively and these polynomial multiplications are very slow as the degree of polynomial increases. So my task is to speed up this part to do encryption and decryption quickly. This will be handled by the Number Theoratic Transform module, which is the hardware accelerator. and finally integrate this with the AJIT processor and realise an SoC. The AJIT processor has been chosen because the organization whose project this is, has security as its primary goal, then power consumption as the secondary goal. We can realise a greater layer of security because the processor is in-house and we have all the source code available to us. and Also the AJIT processor has shown better use cases in the Embedded world, as it is being used in NAVIC as of now. The AJIT processor a different flavours, like the RISC-V processors. The AJIT can be single core single CPU per thread up to Quad core, Double CPUs per thread. That too, it can be 32 bit or a 64 bit. AJIT also follows RISC ideology, and it is based on SPARC ISA. The SPARC ISA allows it to be much faster when it comes to context switching, which is crucial in embedded applications where interrupts are very frequent. AJIT has an out of Order execution pipeline. A single issue in-order 7 stage pipeline. The flow of an instruction down the pipeline depends on the type of instruction, like for load-store instructions the execution flow varies from other instructions. To be able to use this processor, there is a tool-chain which allows to go very low level programming. I have used it to modify the Stack pointer, base pointer, from where the data and code should be stored, in Flash or DRAM. To test the capability of the AJIT processor to run the NTT algorithm, I have done a Bare metal code and one with its own RTOS, called CORTOS. I had to manually setup stack size, memory ranges, and other things, but with CORTOS, I only need to mention how much size do I want and if I want to use Flash or directly the DRAM only. CORTOS manages itself. The tool-chain offers C simulation of the processor, as well as the FPGA implementation. So I have done the Software run and the Hardware run of the algorithm on the Xilinx Kintex7 KC705 Platform. That too, for single thread and double thread. I do have some plans in my mind to test it against a GPU I have in my laptop. I haven't discussed it with my guide and co-guide, but I do have an idea to make a simple processing cores, like in the GPUs.

| Type         | Measurement Unit | AJIT Processor (Single Thread) | AJIT Processor (Dual Thread) | PYNQ-Z2 (Dual Core ARM A9) |
| ------------ | ---------------- | ------------------------------ | ---------------------------- | -------------------------- |
| Software Run | Clock Cycles     | 700481                         | 2969265                      | N/A                        |
|              | Milli-Seconds    | 8.75                           | 37.11                        | N/A                        |
| Hardware Run | Clock Cycles     | 342104                         | 3971314                      | N/A                        |
|              | Milli-Seconds    | 4.27                           | 49.64                        | 67.78                      |


## [[GPU with NIOS II]]
		
The project focuses on developing a simplified Graphics Processing Unit (GPU) specifically made to work with the NIOS II embedded processor. This project creates a basic hardware design to process some 3D vectors and show them on the VGA display, A true GPU is programmable and can also work as a General-Purpose GPU (GPGPU), so it can perform a wide range of computational tasks mostly relate to liner algebra beyond just graphics rendering, by following the SIMD method. This project aims to display simple 3D geometry structures that rotate on specific axis on a VGA monitor. We used the Intel Quartus Prime, Intel Platform Designer for system architecture and the DE2-115 development board with an Altera Cyclone IV FPGA. We designed modules for Vertex Shading, Rasterization and VGA controller. 
The system operates at a resolution of 640x480 pixels with a refresh rate of 60 Hz. This configuration adheres to the industry-standard VGA timing for 640x480 at 60 Hz, which specifies a pixel clock frequency of 25.175 MHz. At this resolution and refresh rate, the GPU processes 640 pixels per line × 480 lines per frame × 60 frames per second, totalling 18,432,000 pixels per second.
Like in the traditional GPU pipeline, first step is Vertex Shading. This module will convert the 3D coordinates into 2D coordinates. Before that, since we want our shape to rotate, we multiply the vertices with rotation matrix to rotate it for a specific axis. Then we have the pixel data and now we want to connect them to draw a line and make a shape. We use Bresenham's line algorithm to draw the line. With this algorithm we get all of the points between the two points for which we draw the line. and These points will be stored in Frame buffers, FIFOs, then to be shown on the display.

From this project, I got more interested into GPU programming ever since I got to learn that GPUs can be programmed and they're not just to show graphics. I did some basic computations related to GPU. Like adding two arrays of $2^{128}$ elements. I have Nvidia RTX 3070ti in my laptop which has 6144 CUDA cores running at 1.5Ghz base clock. It has Ray tracing cores and the DLSS feature. I wanted to utilize it for general purpose computing. I used these computing threads in the CUDA core to do this job. It took about 0.3ms for GPU and 17ms for the CPU. 

In this [[GPU programming Flow]], first data is prepared on the host (CPU). Some memory is allocated on the device (GPU) using functions like `cudaMalloc()`. Then the prepared data from CPU is sent to GPU via `cudaMemcpy()` function with the `cudaMemcpyHostToDevice` flag. A kernel function is defined with the `__global__` keyword, specifies the operations to be executed in parallel across multiple threads on the GPU. This kernel is launched with a defined execution configuration using the `<<<blocksPerGrid, threadsPerBlock>>>` syntax, which determines the grid and block dimensions for parallel execution. To ensure that the GPU has completed its tasks before the CPU proceeds, especially when subsequent operations depend on the GPU's output, `cudaDeviceSynchronize()` is called. After processing, the results are copied back from the device to the host using `cudaMemcpy()` with the `cudaMemcpyDeviceToHost` flag. Finally, allocated GPU memory is freed using `cudaFree()` to maintain optimal resource utilization.


## [[RISC VI-Stage Pipelined Processor]]

The other candidates before me must have talked about this project, so I'll mention only what is different in my project.
The ISA and everything is same, But I did not include Load-store multiple. Apart from this, all instructions are there. During the viva, we were criticized because our processor had only a clk and reset port. So that got me thinking and I designed later a Cache controller for this project. 

I did a direct mapped 1 Mega bit of size cache. It will take the inputs as current instruction, and a port that would be connected to memory port when the cache misses the data. And it will output if its a hit or miss along with the data that is there in the cache. This design was specific for instruction cache only as I wanted to design as simple cache as possible. Otherwise I would have to account for the data being written to the cache from the MEM stage of the processor as well. In the current design, I only need to check if the instruction to be fetched would be there in the cache or not and give hit or miss.
The hit will be identified by the Tag bits and the valid bits stored in the cache memory. 

Its a 1Mb of cache, with 8 cache lines. Each cache line with 8 word offset, each cache line can have up to 8 instructions. So to map the 16 bit instruction, 3 bits are for offset, 3 bits are for Indexing the cache lines, and the rest of the 10 bits are for Tag. Also one bit for Valid. 

In case of a hit it will output that instruction from the RAM, since the Cache line has capability to have 8 instructions in it, it will use the offset bits to identify the correct 16-bits. In case of a miss, it will output a busy signal, and request data from memory. This is validated in test bench by giving the data at its input port with a stimulus. It will release the busy signal and move into cache update state. That data will be put in the index pointed by the instruction it is asking for and the valid and tag bits will be updated accordingly.

Branch history predictor:
	I did a **1-bit branch predictor** with a **Branch Target Buffer (BTB)** by predicting both the outcome and target address of branch instructions. The BTB is a cache-like structure where each entry includes a valid bit, a tag derived from the branch instruction's address, the target address to jump to if the branch is taken, and a 1-bit predictor indicating whether the branch is likely to be taken (`1`) or not taken (`0`). During the instruction fetch stage, the processor uses the Program Counter (PC) to check into the BTB. If there's a BTB hit (i.e., the valid bit is set and the tag matches the PC), the processor consults the 1-bit predictor: if it predicts 'taken', the processor fetches the next instruction from the stored target address; if 'not taken', it fetches from the sequential address. Upon executing the branch, the actual outcome is compared to the prediction. If the prediction was incorrect, the processor flushes the mis-fetched instructions from the pipeline, updates the BTB entry with the correct target address and actual outcome, and resumes fetching from the correct address.


## [[RISC V with TL-Verilog]]

It was a workshop project, coordinated by VSD and Steve Hoover from Redwood EDA. He is one of the co-founder of TL-Verilog language. It is a High level language, which reduces the code size and claims it is better when it comes to verification part of the design. I say they claim it because I have not used it exhaustively to know the exact differences. I used to pipeline structure that it offers. When we do Forwarding in a pipelined designed we define different signal name and everything for a specific stage in a pipeline, but here we don't need separate names. The language knows that its different stage because we define stages by writing @1, @2 etc etc and write logic for that specific stage. The registers between the stage are implied. I was into this workshop mostly for the RISC V processor part. I wanted to get started with RISC V, and I got to understand how the RISC V tool chain is used, how to compile for a specific architecture with specific ABI. For the design part, we were given all the necessary parts, like the logic block for memories. We only had to write a logic for PC fetching, ALU operations, Branch instruction and Data forwarding.   
#### **ABI:**
- A set of rules governing how software components interact at the binary level.
- The **ISA** defines that RISC-V has registers `a0` to `a7`.
- The **ABI** specifies that `a0` is used for the first argument in a function call and `a1` for the second.
- Defines how data types (e.g., `int`, `long`, `float`) are laid out in memory and their sizes.

## [[Physical Design Using OpenLANESky130 for PicoRV32]]

I got this workshop opportunity during a hackathon I was a part of. I lost obviously, I participated in it before coming here. I got a chance to meet people in the industry and got insights into how the VLSI industry works, like different types of roles and everything. That's what I wanted from this, to connect to people. In this workshop, we were given the code for PicoRV32 and we were supposed to make a GDS file for this design. There were two approaches, one was the normal one and another with out own designed and characterized Standard Cell for an Inverter. 

Steps to do make a Standard Cell:
1. Define a SPICE Deck. and run transient simulation. (PMOS: w=70 l=23, NMOS: w=35 l=23) along with contact dimentions.
2. Plot Output voltage vs Time.
3. Get the Rise time and Fall times.
4. Set the grid parameters according to the tracks.info file. it was put on the li1 layer. with grid 0.46um 0.34um 0.23um 0,17um
5. Write LEF
6. To integrate this cell, config.tcl file is edited. 

## [[ARM Based SoC Design]]

A workshop related to ARM Cortex M0 SoC design, the IP was given to us and we were supposed to integrate peripherals to it. I added Timer, Memory and LED/GPIO Peripheral. I designed the LED peripheral. It has AHB interface signals and one output signals of 8 bits. Whatever we write in the peripheral's WDATA port, it will be stored in a register if the Peripheral is selected, and Write transaction is valid and if it is a Valid data transaction. The lower 8 bits of data are mapped to the output register and if we try to read this output register a 32-bit data is read with MSB 24 bits being 0. These peripherals were interfaced with the ARM Cortex M0. and an Assembly code was written into the BRAM by converting it into Hex file with KeilU.

## [[FIFO]]

## [[MAC unit with BIST]]

Traditional pen-paper solution could be used to do multiplication, but we would need n-1 adder stages to do that. That is way too slow. We use Carry Save Adders, and Add two numbers together and such additions are happening parallely. 
![[Pasted image 20241129234240.png]]
Even though the carry is being passed to the next column, it is not rippling. From the previous stage, the carry would be available for the 2nd Full adder. 

## [[Real-Time traffic sign detection with Pynq Z2 board]]


## Post-interview questions

1. Now that you know about me, my experience, and my skills, but I would love to know from your end, what are the main qualities and skills you are looking for, in the ideal candidate for this position, and what am I lacking in your opinion?
2.  What’s a new skill that is a big priority for the team to learn?
3. What is the team dynamics and the goal of the team?
4. What do the best hires on your team do in the first 30 days?
5. What challenges I could face at the start of the job, for first 3 months, 6 months etc
6. What would outstanding performance look in this job?
7. What common characteristics do you see in people who are successful in this position?


## HR Questions

1. How did you ended up here at IITB doing M.tech?
2. Do company research. Which product line it has, its key products?
3. 
## ❓ Questions
- 

## 🔗 Related links

