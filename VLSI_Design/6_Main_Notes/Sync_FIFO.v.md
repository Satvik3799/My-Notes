```
`timescale 1ns/1ps

module FIFO #(

  parameter B = 8,  // number of bits in a word

  parameter W = 4   // number of address bits

)

//Ports

(

  input wire clk, reset,

  input wire rd, wr,

  input wire [B-1:0] w_data,

  output wire empty, full,

  output wire [B-1:0] r_data

);

  reg [B-1:0] Registers [2**W-1:0];  // registers inside Register File

  reg [W-1:0] w_ptr_reg, w_ptr_next, w_ptr_succ;

  reg [W-1:0] r_ptr_reg, r_ptr_next, r_ptr_succ;

  reg full_reg, empty_reg, full_next, empty_next;

  

  wire wr_en;

  

  // write operation

  always @(posedge clk) begin

    if (wr_en) Registers[w_ptr_reg] <= w_data;

  end

  // read operation

  assign r_data = Registers[r_ptr_reg];

  

  // write enabled only when FIFO is (not full)

  assign wr_en = wr & ~full_reg;

  

  /**********************************/

  // FIFO control logic

  /**********************************/

  // register for read and write pointers

  always @(posedge clk or posedge reset) begin

   if (reset) begin

      w_ptr_reg <= 0;

      r_ptr_reg <= 0;

      full_reg <= 1'b0;   //Default Full False

      empty_reg <= 1'b1;  //Default Empty True

   end

   else begin

      w_ptr_reg <= w_ptr_next;

      r_ptr_reg <= r_ptr_next;

      full_reg <= full_next;

      empty_reg <= empty_next;

    end

end

  // next-state logic for read and write pointers

  always @(*) begin

    // // successive pointer values

    // w_ptr_succ = w_ptr_reg + 1;

    // r_ptr_succ = r_ptr_reg + 1;

    // default: keep old values

    w_ptr_next = w_ptr_reg;

    r_ptr_next = r_ptr_reg;

    full_next = full_reg;

    empty_next = empty_reg;

    case ({wr, rd})

    //When read and write are false - No operation

      2'b00: ;  

    //Only read from FIFO

      2'b01:

        if (~empty_reg) // not empty

        begin

          r_ptr_next = r_ptr_reg + 1;

          full_next = 1'b0;

          if ((r_ptr_reg + 1) == w_ptr_reg)

            empty_next = 1'b1;

        end

    //Only Write into FIFO

      2'b10:

        if (~full_reg) // not full

        begin

          w_ptr_next = w_ptr_reg + 1;

          empty_next = 1'b0;

          if ((w_ptr_reg + 1) == r_ptr_reg)

            full_next = 1'b1;

        end

  

    //Read and Write together

      2'b11: // write and read

        begin

          w_ptr_next = w_ptr_reg + 1;

          r_ptr_next = r_ptr_reg + 1;

        end

    endcase

  end

  

  // output

  assign full = full_reg;

  assign empty = empty_reg;

  

endmodule
```