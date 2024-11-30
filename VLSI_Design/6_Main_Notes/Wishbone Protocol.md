The **Wishbone** protocol is an open-source System-on-Chip (SoC) interconnect that provides a standardized way to connect IP cores. Its architecture is based on a master-slave model and uses a simple handshake mechanism to facilitate communication. Here are the key points:

#### Main Signals and Their Functions

1. **Common Signals**:
    
    - **CLK_I**: Clock signal for synchronization.
    - **RST_I**: Reset signal to initialize the interface.
    - **DAT_I, DAT_O**: Data input/output arrays for data transfer.
    - **SEL_O**: Select signals indicating valid data bytes.
2. **Master Signals**:
    
    - **ADR_O**: Address bus to specify the memory location or register.
    - **CYC_O**: Indicates the start and continuation of a bus cycle.
    - **STB_O**: Strobe signal for data transfer initiation.
    - **WE_O**: Write enable signal; high for write, low for read.
    - **TGA_O, TGC_O**: Optional tags for address and cycle information.
3. **Slave Signals**:
    
    - **ACK_I**: Acknowledges the completion of a valid data transfer.
    - **ERR_I, RTY_I**: Optional signals for error handling and retry requests.

#### Communication Mechanism

- The protocol operates using **handshaking**:
    - The **master** asserts `CYC_O` and `STB_O` to initiate a transfer.
    - The **slave** responds with `ACK_I` to signal successful completion or `ERR_I`/`RTY_I` for errors or retries.
    - Data is exchanged on the `DAT_I/DAT_O` bus, with control via `SEL_O` and `WE_O`.

#### Features

- Modular data widths (8, 16, 32, 64 bits).
- Single or block transfers.
- Support for synchronous and asynchronous design.
- Big and little endian compatibility.
- Flexible interconnect topologies (point-to-point, shared bus, crossbar).