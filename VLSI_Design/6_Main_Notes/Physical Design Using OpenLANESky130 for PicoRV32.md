
[Github](https://github.com/Satvik3799/Physical-design-with-OpenLANE-using-Sky130-PDK?tab=readme-ov-file#steps-to-build-custom-standard-cell-and-its-integration)
[[23M1117_EE671_Assign_1.pdf]]

I got this workshop opportunity during a hackathon I was a part of. I lost obviously, I participated in it before coming here. I got a chance to meet people in the industry and got insights into how the VLSI industry works, like different types of roles and everything. That's what I wanted from this, to connect to people. In this workshop, we were given the code for PicoRV32 and we were supposed to make a GDS file for this design. There were two approaches, one was the normal one and another with out own designed and characterized Standard Cell for an Inverter. 

Steps to do make a Standard Cell:
1. Define a SPICE Deck. and run transient simulation. (PMOS: w=70 l=23, NMOS: w=35 l=23) along with contact dimensions.
2. Plot Output voltage vs Time.
3. Get the Rise time and Fall times.
4. Set the grid parameters according to the tracks.info file. it was put on the li1 layer. with grid 0.46um 0.34um 0.23um 0,17um
5. Write LEF
6. To integrate this cell, config.tcl file is edited. 



Specification on Inverter:
For pMOS width = 1.740μm and nMOS width = 0.595μm.
Rise Time = 234.21ps
Fall Time = 234.86ps

