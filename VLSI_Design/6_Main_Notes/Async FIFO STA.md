Multicycle Path:
- From `wr_FF2/Q` to `rd_FF1/D`, indicating that the data might require multiple cycles to be valid in the read domain.

False Path:
    - From `wr_clk` to `rd_FF1/D` (asynchronous crossing).
    - From `wr_clk` to any control signals in the read domain.

Defining asynchronous clock domains:
    - **Path**: Between any signals driven by `wr_clk` and `rd_clk`.
    - **Reason**: These clocks operate independently without a fixed relationship.
`set_clock_groups -asynchronous -group {wr_clk} -group {rd_clk}`