1. Connect USB to UART, JTAG and programmer cables to the laptop
2. Terminal 1: Connect_HPC and open Vivado
3. Terminal 2: Start docker in local laptop
4. Inside containter, give 666 permission to USB ports (chmod 666 /dev/tty/USB*)
5. Terminal 3: Start minicom
6. Terminal 2: do "calibrateUart /dev/ttyUSB0" USB0 should be the USB to UART device.



# Loading the .bit file onto the Kintex board

Copy the bit file (processor_1x132.sa.nc.alt.bit)
Launch Vivado (Board is connected and switched ON)
Open Hardware manager
Open Target -> Auto Connect
Program device -> Upload the bitstream
Untick the "Enable end of startup" option and click Program




/// Ajit

Copy the bit file (processor_1x132.sa.nc.alt.bit)
Launch Vivado (Board is connected and switched ON)
Open Hardware manager
Open Target -> Auto Connect
Program device -> Upload the bitstream
Untick the "Enable end of startup" option and click Program

//

* JTAG is beside the power button
//
sudo apt install minicom

//minicom -s should be opened from anywhere

//change permissions
//inside ajit-build-dev folder, 
sudo chmod 666 /dev/ttyUSB0
sudo chmod 666 /dev/ttyUSB1

//USB0 is CP2102 UART module
//USB1 is JTAG from the kintex board

calibrateUart /dev/ttyUSB0
ajit_debug_monitor_mt -u /dev/ttyUSB0
r mode 0x0, 0x3, 0x9, 0x2 (3 is error mode, 0 is uninitialised, reset after Vivado program also)

// below is ajit debug monitor
ajit[0.0]> r mode
r mode returns 0x0
ajit[0.0]> s run.script
ajit[0.0]> q

____________________
validation_ladder/
ipc and impc (= ipc+4)

______________________
Ground black Pin 16
Rx of USB (of USB-UART) brown 18 on FPGA
Tx 17
CP2102 USB to TTL (3.3V however recommended is 1.8V for Kintex 7 KC board)


Reset instructions??????????
