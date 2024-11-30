
 The final goal of the project is to realise an AJIT SoC, that is specific for Cryptography only, by  removing some peripherals that would not be needed for any Cryptographic operation. The SoC is to be used in the field of Post Quantum Cryptography or PQC for short and Fully Homomorphic Encryption, FHE for short, methods. These methods use polynomial multiplication extensively and these polynomial multiplications are very slow as the degree of polynomial increases. So my task is to speed up this part to do encryption and decryption quickly. This will be handled by the Number Theoratic Transform module, which is the hardware accelerator. and finally integrate this with the AJIT processor and realise an SoC. The AJIT processor has been chosen because the organization whose project this is, has security as its primary goal, then power consumption as the secondary goal. We can realise a greater layer of security because the processor is in-house and we have all the source code available to us. and Also the AJIT processor has shown better use cases in the Embedded world, as it is being used in NAVIC as of now. The AJIT processor a different flavours, like the RISC-V processors. The AJIT can be single core single CPU per thread up to Quad core, Double CPUs per thread. That too, it can be 32 bit or a 64 bit. AJIT also follows RISC ideology, and it is based on SPARC ISA. The SPARC ISA allows it to be much faster when it comes to context switching, which is crucial in embedded applications where interrupts are very frequent. AJIT has an out of Order execution pipeline. A single issue in-order 7 stage pipeline. The flow of an instruction down the pipeline depends on the type of instruction, like for load-store instructions the execution flow varies from other instructions. To be able to use this processor, there is a tool-chain which allows to go very low level programming. I have used it to modify the Stack pointer, base pointer, from where the data and code should be stored, in Flash or DRAM. To test the capability of the AJIT processor to run the NTT algorithm, I have done a Bare metal code and one with its own RTOS, called CORTOS. I had to manually setup stack size, memory ranges, and other things, but with CORTOS, I only need to mention how much size do I want and if I want to use Flash or directly the DRAM only. CORTOS manages itself. The tool-chain offers C simulation of the processor, as well as the FPGA implementation. So I have done the Software run and the Hardware run of the algorithm on the Xilinx Kintex7 KC705 Platform. That too, for single thread and double thread. 

| Type           | Measurement Unit | AJIT Processor (Single Thread) | AJIT Processor (Dual Thread) | PYNQ-Z2 (Dual Core ARM A9) |
|----------------|------------------|---------------------------------|------------------------------|---------------------------|
| Software Run   | Clock Cycles     | 700481                          | 2969265                     | N/A                       |
|                | Milli-Seconds    | 8.75                            | 37.11                       | N/A                       |
| Hardware Run   | Clock Cycles     | 342104                          | 3971314                     | N/A                       |
|                | Milli-Seconds    | 4.27                            | 49.64                       | 67.78                     |


## AJIT Specifics
AJIT has an out of Order execution pipeline. It consists of various stages such as fetch, iCache, decode, register read, execute, write back, and retire.
The flow of an instruction down the pipeline depends on the type of instruction. 
For example, an integer arithmetic operation has the flow Fetch → Icache → Decode → RegRead → Exec → WriteBack → Retire
whereas, a load operation to the integer register file has the flow Fetch → Icache → Decode → RegRead → Loadstore → Dcache → WriteBack → Retire.

Proof of concept: @SCL Chandigarh
	7mm X 7mm chip area
	144 functional I/O’s, 256 pin package.
	0.5 W at 66 MHz (slow corner). 

NAVIC AJIT specifications:
	Manufactured at UMC (Taiwan) - 65nm tech node
	4mm X 4mm SoC area, and  1mm X 1mm CPU area. 
	Overall system is operated at 125Mhz, but the CPU can run at 500Mhz.
	System Power dissipation is 250mW@125Mhz. CPU power dissipation is 50mW.


## PQC and FHE
 In PQC, as the name suggests, these schemes are specific to the encryption methods which would not be decrypted by Quantum computers. And we do need this right now, because what people could do is store the critical information right now and decrypt it later when they have access to a Quantum computer. 
 
 Similarly, in FHE, the idea revolves around one thing, being able to perform mathematical operations like Addition and multiplication on encrypted data. For ex., A client could send some encrypted numbers like 70 and 30, Add them while they are encrypted on the server side, and get the result back in the encrypted forma and decrypt it when the client has it back.  
 
My goal is to design a hardware accelerator and eventually realise an SoC, and not develop some cryptographic scheme. So I have worked on this project without going much deeper into the cryptographic section of the project.

### NTT and Its Role in Cryptography

NTT is a discrete Fourier transform optimized for polynomial operations over finite fields. It’s crucial in **lattice-based cryptography**, like the Kyber and FHE schemes, where it drastically improves efficiency in polynomial multiplication, reducing complexity from O(n2)O(n2) to O(nlog⁡n)O(nlogn). This efficiency is especially important in post-quantum cryptographic schemes, where large polynomials are frequently used.

Walk me through the C-code.

For the AJIT processor, implementing NTT required several essential components:

1. **Barrett Reduction** for efficient modular arithmetic,
2. **Twiddle Factors** to handle root-of-unity multiplications,
3. **Butterfly Units** for transforming polynomial coefficients,
4. **Pointwise Multiplication** to manage polynomial terms, and
5. **Address Generation** to streamline data access during transformations.

### NTT Implementation on AJIT

1. **Single-thread Implementation**:
    
    - I executed NTT on the **single-core AJIT processor** running at 80 MHz, focusing first on a software implementation in C using **bare-metal programming**.
    - Then, using CORTOS, which helps manage resources like memory, the single-thread implementation allowed me to analyze performance and resource usage on both an AJIT emulator and a Kintex KC705 FPGA.
2. **Dual-thread Implementation**:
    
    - To further optimize, I split the NTT input data across the two threads—processing even and odd index arrays in parallel.
    - This split approach leverages the AJIT’s dual-thread support and significantly improves computation time, showing a clear benefit of the processor’s architecture for data-parallel tasks.

## Crystals Kyber Scheme
