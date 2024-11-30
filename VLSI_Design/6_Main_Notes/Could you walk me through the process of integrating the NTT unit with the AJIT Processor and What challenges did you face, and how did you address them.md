
My seniors at the HPEC lab have passed on a grate legacy so to say, gave templates thhhat we can use to integrate any Hardware accelerators to the AJIT processor.
So we integrate an accelerator with the use of te AJIT's own communication protocols, a DMA and two FIFOs. So we have the processor, which has two separate protocols, AJIT FIFO BUS (AFB) and AJIT Core Bus (ACB) bus protocols. ACB is like Axi lite protocol, some data signals, address signals, and data is sent in packets. One at a time. AFB is like Axi stream protocol, continuous stream of data till all the packets are sent. There are intermediate blocks to convert the ACB and AFB protocols to the Axi Protocols.

There are two ways to integrate, with and without DMA.

Without DMA, the AFB bus is used and the data is sent though the AFB bus to the AFB to AXI module then to the accelerator.
![[Pasted image 20241113124259.png]]

With DAM, uses AFB and ACB. The Data to and from the accelerator and processor travels from the ACB Bus to the DMA, then to the sending FIFO and then received by the accelerator. Now to control the DMA AFB bus is used. The command and status signals from the DMA are used to maintain communication between the DMA data transfer and the accelerator.
![[Pasted image 20241113124241.png]]

I have verified the operation with a test bench on Gate level implementation. Right now there are some issues in getting the new processor IP. So the module integration is yet to be done. But the individual module is ready. The main module was already designed by my senior. I just had to make wrapper for the NTT module that I have to integrate. But right now sir wants me to work on the Verilog implementation because it was designed to prototype as a proof of concept and we cannot have a module that is designed by an HLS tool for the fabrication of the chip. 