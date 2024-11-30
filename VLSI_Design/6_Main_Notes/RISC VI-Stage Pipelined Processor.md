## From starting





## What is different from others

The other candidates before me must have talked about this project, so I'll mention only what is different in my project.
The ISA and everything is same, But I did not include Load-store multiple. Apart from this, all instructions are there. During the viva, we were criticized because our processor had only a clk and reset port. So that got me thinking and I designed later a Cache controller for this project. 

I did a direct mapped 1 Mega bit of size cache. It will take the inputs as current instruction, and a port that would be connected to memory port when the cache misses the data. And it will output if its a hit or miss along with the data that is there in the cache. This design was specific for instruction cache only as I wanted to design as simple cache as possible. Otherwise I would have to account for the data being written to the cache from the MEM stage of the processor as well. In the current design, I only need to check if the instruction to be fetched would be there in the cache or not and give hit or miss.
The hit will be identified by the Tag bits and the valid bits stored in the cache memory. 

Its a 1Mb of cache, with 8 cache lines. Each cache line with 8 word offset, each cache line can have up to 8 instructions. So to map the 16 bit instruction, 3 bits are for offset, 3 bits are for Indexing the cache lines, and the rest of the 10 bits are for Tag. Also one bit for Valid. 

In case of a hit it will output that instruction from the RAM, since the Cache line has capability to have 8 instructions in it, it will use the offset bits to identify the correct 16-bits. In case of a miss, it will output a busy signal, and request data from memory. This is validated in test bench by giving the data at its input port with a stimulus. It will release the busy signal and move into cache update state. That data will be put in the index pointed by the instruction it is asking for and the valid and tag bits will be updated accordingly.

Branch history predictor:
	I did a **1-bit branch predictor** with a **Branch Target Buffer (BTB)** by predicting both the outcome and target address of branch instructions. The BTB is a cache-like structure where each entry includes a valid bit, a tag derived from the branch instruction's address, the target address to jump to if the branch is taken, and a 1-bit predictor indicating whether the branch is likely to be taken (`1`) or not taken (`0`). During the instruction fetch stage, the processor uses the Program Counter (PC) to check into the BTB. If there's a BTB hit (i.e., the valid bit is set and the tag matches the PC), the processor consults the 1-bit predictor: if it predicts 'taken', the processor fetches the next instruction from the stored target address; if 'not taken', it fetches from the sequential address. Upon executing the branch, the actual outcome is compared to the prediction. If the prediction was incorrect, the processor flushes the mis-fetched instructions from the pipeline, updates the BTB entry with the correct target address and actual outcome, and resumes fetching from the correct address.