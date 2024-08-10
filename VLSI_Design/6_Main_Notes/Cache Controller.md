26-07-2024 00:49

Status:

Tag: #Project


# Cache Controller

## I-Cache - Instruction Cache

We want to store current instruction as well as the next 4 instructions.

Cache is specified in blocks.

Cache size - 128 Bytes

- Divided into 8 separate blocks of 16 bytes - (16x8 = 128)
- Each block stores 4 different data of 32 bits (4 bytes), which are accessed with offset bits.

![[Pasted image 20240726005555.png]]

### How to identify the blocks and access right data bits?

- The cache stores the instructions which are very frequent. The instruction inside one of the 8 blocks, inside one of the 4 entries.
- We can not take entire 32-bit and compare it, it is inefficient. So we only take LSB's 10 bits and compare it with the already stored cache entries. 
	- For Ex. a 32-bit instruction - 0011_1010_1011_1111_1111_1010_1000_1111
		- We take the 10 bits of LSB - 10_1000_1111
		Mostly these 10 bits will be different in most of the cases.
		We divide these bits into (Tag - Index - Offset).
		![[Pasted image 20240726010327.png]]First the tag will be checked, and then the index and then the offset, if they match with then it is called a **Cache Hit**, else it will be called a **Cache Miss**.
		 



### Explanation of Address Bits in MEM_READ and CACHE_UPDATE States

#### Address Bits 9 to 4 in MEM_READ State

In the MEM_READ state, the address bits 9 to 4 are used to form the block address to fetch a 16-byte block from the main memory. Here’s why:

1. **Block Address Calculation**:
   - A 16-byte block (2^4 bytes) requires 4 bits for the offset within the block.
   - The remaining bits of the address specify which block in memory is being accessed.

2. **Address Breakdown**:
   - The address provided by the CPU is 10 bits.
   - Bits [3:0] are the offset within the 16-byte block (since 2^4 = 16).
   - Bits [9:4] specify which 16-byte block is being accessed in memory.

3. **MEM_READ State Usage**:
   - When fetching data from the main memory, you need to specify the address of the entire block to be fetched, not just a byte within it.
   - Therefore, the address bits [9:4] are sent to the memory to fetch the corresponding block.

#### Address Bits 6 to 4 in CACHE_UPDATE State

In the CACHE_UPDATE state, the address bits 6 to 4 are used to index into the cache's storage arrays (`STORE_DATA`, `STORE_TAG`, `STORE_VALID`). Here’s why:

1. **Cache Indexing**:
   - The cache has 8 lines (blocks), which can be indexed with 3 bits (2^3 = 8).
   - These lines store the data blocks fetched from memory.

2. **Address Breakdown**:
   - The cache uses a subset of the address bits to select the appropriate cache line.
   - Bits [6:4] are used as the index to select one of the 8 cache lines.

3. **CACHE_UPDATE State Usage**:
   - When updating the cache with a new block of data fetched from memory, you need to know which cache line to update.
   - The index bits [6:4] identify the specific cache line where the new block will be stored.
   - The `STORE_DATA`, `STORE_TAG`, and `STORE_VALID` arrays use this index to update the corresponding line with the new data, tag, and valid bit.

### Summary of Address Bit Usage

- **MEM_READ State**:
  - Uses address bits [9:4] to form the block address.
  - This specifies the 16-byte block to fetch from memory.

- **CACHE_UPDATE State**:
  - Uses address bits [6:4] to index into the cache.
  - This selects the specific cache line to update with the new data, tag, and valid bit.

### Detailed Example

Assume the address provided by the CPU is `0b1010110010` (binary) or `0x2B2` (hex).

- **Offset (bits [3:0])**: `0010` (2 in decimal)
  - Refers to the specific byte within the 16-byte block.

- **Index (bits [6:4])**: `011` (3 in decimal)
  - Selects the 4th cache line.

- **Tag (bits [9:7])**: `101` (5 in decimal)
  - Used to differentiate blocks that map to the same cache line.

### FSM Operation with Address Bits

1. **MEM_READ State**:
   - Address bits [9:4] = `101011`
   - Memory fetches the block starting from this address.

2. **CACHE_UPDATE State**:
   - Address bits [6:4] = `011`
   - Cache updates the 4th line with the fetched block, storing the data and tag `101`.

By dividing the address into these components, the cache can efficiently manage memory access and ensure correct data retrieval and storage.







# References:

