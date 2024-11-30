
1. [[Top moule - GPU]]
2. [[Line Rasternizer]]

### Intro
The project focuses on developing a simplified Graphics Processing Unit (GPU) specifically made to work with the NIOS II embedded processor. This project creates a basic hardware design to process some 3D vectors and show them on the VGA display, A true GPU is programmable and can also work as a General-Purpose GPU (GPGPU), so it can perform a wide range of computational tasks mostly relate to liner algebra beyond just graphics rendering, by following the SIMD method. This project aims to display simple 3D geometry structures that rotate on specific axis on a VGA monitor. We used the Intel Quartus Prime, Intel Platform Designer for system architecture and the DE2-115 development board with an Altera Cyclone IV FPGA. We designed modules for Vertex Shading, Rasterization and VGA controller. 
The system operates at a resolution of 640x480 pixels with a refresh rate of 60 Hz. This configuration adheres to the industry-standard VGA timing for 640x480 at 60 Hz, which specifies a pixel clock frequency of 25.175 MHz. At this resolution and refresh rate, the GPU processes 640 pixels per line × 480 lines per frame × 60 frames per second, totalling 18,432,000 pixels per second.

Like in the traditional GPU pipeline, first step is Vertex Shading. This module will convert the 3D coordinates into 2D coordinates. Before that, since we want our shape to rotate, we multiply the vertices with rotation matrix to rotate it for a specific axis. Then we have the pixel data and now we want to connect them to draw a line and make a shape. We use Bresenham's line algorithm to draw the line. With this algorithm we get all of the points between the two points for which we draw the line. and These points will be stored in Frame buffers, FIFOs, then to be shown on the display.

From this project, I got more interested into GPU programming ever since I got to learn that GPUs can be programmed and they're not just to show graphics. I did some basic computations related to GPU. Like adding two arrays of $2^{128}$ elements. I have Nvidia RTX 3070ti in my laptop which has 6144 CUDA cores running at 1.5Ghz base clock. It has Ray tracing cores and the DLSS feature. I wanted to utilize it for general purpose computing. I used these computing threads in the CUDA core to do this job. It took about 0.3ms for GPU and 17ms for the CPU. 

In this [[GPU programming Flow]], first data is prepared on the host (CPU). Some memory is allocated on the device (GPU) using functions like `cudaMalloc()`. Then the prepared data from CPU is sent to GPU via `cudaMemcpy()` function with the `cudaMemcpyHostToDevice` flag. A kernel function is defined with the `__global__` keyword, specifies the operations to be executed in parallel across multiple threads on the GPU. This kernel is launched with a defined execution configuration using the `<<<blocksPerGrid, threadsPerBlock>>>` syntax, which determines the grid and block dimensions for parallel execution. To ensure that the GPU has completed its tasks before the CPU proceeds, especially when subsequent operations depend on the GPU's output, `cudaDeviceSynchronize()` is called. After processing, the results are copied back from the device to the host using `cudaMemcpy()` with the `cudaMemcpyDeviceToHost` flag. Finally, allocated GPU memory is freed using `cudaFree()` to maintain optimal resource utilization.
## Specifications 

Operates at 50Mhz. and has interface only to the VGA port, as it is outside the FPGA and input of 50Mhz clock.
**Design Flow and Specifications:**

1. **Vertex Shading:**
    
    - **Functionality:** Transforms 3D vertex coordinates to 2D screen coordinates, applying necessary transformations such as rotation and scaling.
    - **Data Representation:** Each vertex is represented by its 3D coordinates (x, y, z), with each coordinate typically using 16-bit fixed-point representation for precision.
2. **Rasterization:**
    
    - **Functionality:** Converts transformed vertices into pixel data, determining which pixels on the screen correspond to the geometric shapes defined by the vertices.
    - **Color Depth:** Since the display is monochromatic (black and white), each pixel is represented by a single bit—'1' for white (illuminated) and '0' for black (non-illuminated).
3. **Frame Buffer:**
    
    - **Structure:** A memory buffer that stores the pixel data to be displayed on the screen.
    - **Size:** For a 640x480 resolution with 1-bit per pixel, the frame buffer requires 640 × 480 bits, equating to 307,200 bits or 38.4 KB.
    - **Implementation:** Utilized on-chip memory resources of the FPGA to store the frame buffer, ensuring quick access and efficient data retrieval.
4. **VGA Controller:**
    
    - **Functionality:** Manages the timing signals required for VGA output, including horizontal and vertical synchronization, and reads pixel data from the frame buffer to send to the display.
    - **Pixel Clock:** Operates at a pixel clock frequency of 25.175 MHz, adhering to the standard VGA timing for 640x480 resolution at 60 Hz refresh rate.
    - **Data Output:** Outputs a serial stream of pixel data to the VGA DAC, which converts the digital signals to analog voltages for display

### Questions:

1. **Design Decisions:**
    
    - Can you explain the key design decisions you made when developing the GPU for the NIOS II core? What were the trade-offs you considered, and how did they influence the final architecture?
2. **Functional Requirements:**
    
    - The project outlines several functional requirements for the GPU, such as vertex processing and rasterization. How did you prioritize these requirements during the design phase, and what challenges did you face in meeting them?
3. **Implementation Challenges:**
    
    - Describe a significant technical challenge you encountered during the implementation of the GPU. How did you approach solving this problem, and what was the outcome?
4. **Performance Optimization:**
    
    - Given that modern GPUs are designed for high performance, what strategies did you employ to optimize the performance of your GPU? How would you measure the effectiveness of these optimizations?
5. **General-Purpose GPU (GPGPU) Capabilities:**
    
    - You mentioned that the GPU could function as a General-Purpose GPU. What specific features or architectural elements would you need to implement to fully realize GPGPU capabilities? How do these features differ from traditional graphics rendering?
6. **Parallel Processing:**
    
    - Modern GPUs leverage parallel processing to enhance performance. Can you discuss how you incorporated parallel processing techniques in your design? What limitations did you encounter, and how did you address them?
7. **Integration with NIOS II Core:**
    
    - Explain the integration process of the GPU with the NIOS II core. What communication protocols did you use, and how did you ensure efficient data exchange between the two components?
8. **Future Enhancements:**
    
    - In your report, you mentioned potential future enhancements for the GPU, such as integrating CUDA capabilities. What specific benefits would this integration provide, and what challenges might arise during implementation?
9. **Impact of the Project:**
    
    - Reflecting on the overall impact of your project, how do you believe it contributes to the field of VLSI design and embedded systems? What lessons did you learn that could be applied to future projects?
10. **Scenario-Based Question:**
    
    - Imagine you are tasked with upgrading your GPU design to support advanced rendering techniques like ray tracing. What architectural changes would you propose, and how would you ensure that the new design remains efficient and cost-effective?

### Performance Parameter Questions:

1. **Throughput and Latency:**
    
    - How did you measure the throughput and latency of your GPU design? What specific metrics did you use to evaluate its performance, and what were the results?
2. **Resource Utilization:**
    
    - Can you discuss the resource utilization of your GPU on the DE2-115 development board? How did you ensure that the FPGA resources (such as logic elements, memory blocks, and DSP slices) were optimally utilized?
3. **Frame Rate and Rendering Speed:**
    
    - What frame rate did your GPU achieve when rendering simple 3D graphics? How did you optimize the rendering speed, and what factors influenced the frame rate?
4. **Power Consumption:**
    
    - Power efficiency is crucial in embedded systems. How did you assess the power consumption of your GPU? What strategies did you implement to minimize power usage while maintaining performance?
5. **Scalability:**
    
    - If you were to scale your GPU design to support more complex graphics or higher resolutions, what performance parameters would you need to monitor? How would you ensure that the design remains scalable?
6. **Benchmarking:**
    
    - Did you use any benchmarking tools or methodologies to compare the performance of your GPU against existing solutions? If so, what benchmarks did you choose, and what were the key findings?
7. **Memory Bandwidth:**
    
    - Discuss the memory bandwidth requirements of your GPU. How did you design the memory management system to handle data efficiently, and what impact did this have on overall performance?
8. **Latency in Data Transfer:**
    
    - What measures did you take to minimize latency in data transfer between the NIOS II core and the GPU? How did you evaluate the effectiveness of these measures?
9. **Impact of Parallelism:**
    
    - How did you quantify the impact of parallel processing on the performance of your GPU? Can you provide specific examples of tasks that benefited from parallel execution?
10. **Performance Bottlenecks:**
    
    - During testing, did you identify any performance bottlenecks in your GPU design? How did you diagnose these issues, and what steps did you take to resolve them?



