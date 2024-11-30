
Code - [[Sync_FIFO.v]]
### Case Statement Conditions:

1. **`2'b00`: No Operation (Neither Read nor Write)**
    
    - This condition is when both `wr` and `rd` are 0.
    - No changes are made to the pointers or status flags.
    - The FIFO remains in its current state, with the write and read pointers unchanged, and the full and empty status flags remaining as they are.
2. **`2'b01`: Read Operation Only**
    
    - This condition is when `wr` is 0 and `rd` is 1.
    - **Action:** Perform a read operation if the FIFO is not empty (`~empty_reg`).
        - Increment the read pointer (`r_ptr_next = r_ptr_reg + 1`).
        - Set `full_next` to 0 because reading frees up space, so the FIFO cannot be full.
        - Check if the FIFO becomes empty after the read operation. If the incremented read pointer equals the write pointer, set `empty_next` to 1.
3. **`2'b10`: Write Operation Only**
    
    - This condition is when `wr` is 1 and `rd` is 0.
    - **Action:** Perform a write operation if the FIFO is not full (`~full_reg`).
        - Increment the write pointer (`w_ptr_next = w_ptr_reg + 1`).
        - Set `empty_next` to 0 because writing adds data, so the FIFO cannot be empty.
        - Check if the FIFO becomes full after the write operation. If the incremented write pointer equals the read pointer, set `full_next` to 1.
4. **`2'b11`: Simultaneous Read and Write**
    
    - This condition is when both `wr` and `rd` are 1.
    - **Action:** Perform both read and write operations.
        - Increment both the write and read pointers (`w_ptr_next = w_ptr_reg + 1` and `r_ptr_next = r_ptr_reg + 1`).
        - This effectively means that one item is read and another is written in the same cycle, maintaining the number of items in the FIFO.
        - The `full` and `empty` status flags remain unchanged because the net effect on the FIFO's occupancy is zero.