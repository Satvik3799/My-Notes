### Question

A display screen is arranged as rows and columns of pixels. A screen has **R** rows and **C** columns of pixels. Each pixel needs **X** bits of storage for Red, Green, Blue, and Alpha (transparency) components. **F** represents the Frame Rate Per Second. **N** represents the compression Rate in Memory. **S** represents the size of SRAM.

Given:
- **R** = 1024
- **C** = 1536
- **X** = 128
- **F** = 32
- **N** = 4
- **S** = 6

You are required to calculate:

1. Total size of memory required to store one frame of video (in MB).
2. Bandwidth required to stream video at **F** frames per second (in MBPS).
3. Number of compressed frames that can fit in SRAM of **S** MB.

Note:
- Round answers: If 1.545 or 1.546, round to 1.55. If 1.563, round to 1.56.

---

### Answer with Explanation

#### 1. **Total size of memory required to store one frame of video**

We calculate the memory required for one frame step by step:

- **Memory per pixel**: Each pixel requires **X = 128 bits**. Convert bits to bytes:
  
  $$
  \frac{128 \text{ bits}}{8 \text{ bits/byte}} = 16 \text{ bytes}
  $$

- **Total pixels in one frame**: The screen has **R × C** pixels:
  
  $$
  1024 \times 1536 = 1,572,864 \text{ pixels}
  $$

- **Memory for one frame (uncompressed)**: Multiply the number of pixels by the memory per pixel:
  
  $$
  1,572,864 \times 16 = 25,165,824 \text{ bytes}
  $$

  Convert to megabytes:
  
  $$
  \frac{25,165,824}{1024 \times 1024} = 24.00 \text{ MB}
  $$

- **Memory for one frame (compressed)**: With a compression factor of **N = 4** (4:1 compression), the compressed memory required for one frame is:
  
  $$
  \frac{24.00 \text{ MB}}{4} = 6.00 \text{ MB}
  $$

So, the **total size of memory required to store one frame of video is 6.00 MB**.

---

#### 2. **Bandwidth required to stream video at F frames per second**

The bandwidth is the memory required per second to stream video. Given **F = 32** frames per second:

$$
\text{Bandwidth (MBPS)} = 6.00 \text{ MB/frame} \times 32 \text{ frames/second} = 192.00 \text{ MBPS}
$$

Thus, the **bandwidth required to stream video at 32 frames per second is 192.00 MBPS**.

---

#### 3. **Number of compressed frames that can fit in SRAM**

The size of SRAM is **S = 6 MB**. Each compressed frame takes **6.00 MB** of memory, so the number of frames that can fit in SRAM is:

$$
\text{Number of frames in SRAM} = \frac{S}{\text{Compressed memory per frame}} = \frac{6.00}{6.00} = 1 \text{ frame}
$$

Thus, **1 compressed frame can fit in 6 MB of SRAM**.

---

### Explanation of the Compression Part

Compression reduces the memory required to store a frame. In this case, a compression factor of **N = 4** means that the original memory size of each frame is reduced to **one-fourth** of its original size. Specifically:

$$
\text{Compressed Size} = \frac{\text{Original Size}}{N}
$$

For example:
- The **uncompressed size** of one frame is 24.00 MB.
- After applying the **compression factor of 4**, the compressed size of the same frame is:

$$
\frac{24.00 \text{ MB}}{4} = 6.00 \text{ MB}
$$

This means the memory required to store each frame is reduced by 75%. Compression helps to save space and bandwidth, allowing more data to be stored or transmitted in the same resources. In this case, without compression, one frame would require 24.00 MB of memory. But after compression, the same frame only needs 6.00 MB, allowing more frames to be stored or streamed with less memory.
