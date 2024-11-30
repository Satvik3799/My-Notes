Implements an **AHB (AMBA High-performance Bus) slave module** named `AHB2LED`. This module is a simple interface that interacts with the AHB-Lite protocol and drives an **LED output** based on data written to it via the AHB bus. Here's a breakdown of its functionality:

### **Inputs and Outputs**

1. **AHB-Lite Interface:**
    - **Inputs:**
        - `HSEL`: Slave select signal; indicates if this slave is selected.
        - `HCLK`: Clock signal for synchronous operation.
        - `HRESETn`: Active-low reset signal to initialize the module.
        - `HREADY`: Indicates whether the previous transfer is complete and the bus is ready for a new transfer.
        - `HADDR`: 32-bit address bus used for selecting specific memory-mapped registers.
        - `HTRANS`: Transaction type (e.g., idle, non-sequential, sequential).
        - `HWRITE`: Indicates write (`1`) or read (`0`) operation.
        - `HSIZE`: Indicates the size of the data being transferred.
        - `HWDATA`: Data bus for writing data.
    - **Outputs:**
        - `HREADYOUT`: Indicates that the slave is ready to complete the current transfer (always `1` in this module, i.e., zero wait-state operation).
        - `HRDATA`: 32-bit data bus for read operations.
2. **LED Output:**
    - `LED`: 8-bit output representing the state of the LEDs.

---

### **Registers**

1. **Address Phase Sampling Registers:** These registers (`rHSEL`, `rHADDR`, `rHTRANS`, `rHWRITE`, `rHSIZE`) capture the signals from the AHB address phase when `HREADY` is high. This ensures stable and synchronized sampling for the data phase.
    
2. **Data Register (`rLED`):** This 8-bit register stores the value written to the module via `HWDATA` and drives the `LED` output.
    

---

### **Behavior**

1. **Address Phase Sampling (`always` block):**
    
    - On the rising edge of `HCLK` or the falling edge of `HRESETn`:
        - If `HRESETn` is deasserted (`0`), all sampled registers are cleared to their default values.
        - If `HREADY` is high, the module samples the `HSEL`, `HADDR`, `HTRANS`, `HWRITE`, and `HSIZE` signals. This indicates that a new address phase is valid.
2. **Data Phase Write (`always` block):**
    
    - On the rising edge of `HCLK` or the falling edge of `HRESETn`:
        - If `HRESETn` is deasserted (`0`), the `rLED` register is cleared to `0`.
        - If:
            - The slave is selected (`rHSEL` is `1`).
            - A write transaction is indicated (`rHWRITE` is `1`).
            - A valid data phase transaction (`rHTRANS[1]` is `1`).
        - Then, the lower 8 bits of `HWDATA` are written into the `rLED` register.
3. **Transfer Response:**
    
    - `HREADYOUT` is always `1`, meaning the module is always ready for a single-cycle write or read operation.
4. **Read Data:**
    
    - The `HRDATA` output is set to the `rLED` value padded with zeros to form a 32-bit word.
5. **LED Output:**
    
    - The `LED` output is directly driven by the `rLED` register.

---

### **Key Points**

1. **Write Operation:**
    
    - During a valid write transaction, the lower 8 bits of `HWDATA` are stored in the `rLED` register, which updates the `LED` output.
2. **Read Operation:**
    
    - During a read transaction, the `HRDATA` bus outputs the current value of the `rLED` register.
3. **Zero Wait-State:**
    
    - `HREADYOUT` is always `1`, indicating no delays or wait states in data transfer.

---

### **Example Usage**

- The module could be used to control 8 LEDs connected to the `LED` output in a memory-mapped system. For instance:
    - Writing `0x55` to the base address of this module would light up LEDs in the pattern `01010101`.
    - Reading from the base address would return the current LED state as a 32-bit word.

This is a simple yet practical design to demonstrate interfacing with AHB-Lite and controlling external peripherals like LEDs.