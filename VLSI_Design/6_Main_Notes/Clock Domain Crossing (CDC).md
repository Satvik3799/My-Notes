

![[Pasted image 20240805143943.png]]

Synchronizing Control signals is easier compared to the Data signals. This is due to different path delays in individual bits in a parallel transfer of bits. So handshaking protocols need to be implemented.

## Level to Pulse Circuit

**Purpose:** 
A level to pulse trigger circuit is used to generate a pulse in the low-frequency domain whenever it detects a change (level change) in the synchronized signal from the high-frequency domain.

This circuit is used when we go from Low frequency domain to high frequency domain. At the receiving end a double synchronizer is put and the D-FF $A \bar{B}$ combination is put in order to realise the Level to Pulse circuit.
![[Pasted image 20240805161206.png]]


#Doubt 2 clock cycle delay is needed to be considered?????
## Pulse to Level Circuit

**Purpose:** 
A pulse to toggle circuit is used to generate a toggling signal that changes state with each pulse. This can help in reliably capturing data transitions in the high-frequency domain.
So with this circuit, we can see when the data changes, independent of the clock and these pulses can then be sent to the Low Frequency domain.

![[Pasted image 20240805165719.png]]




# Control Signal Synchronizer

Consider a Response and Acknowledgement signal between two Clock domains.
![[Pasted image 20240806005923.png]]
![[Pasted image 20240806013801.png]]
![[Pasted image 20240806005951.png]]

At the Transmit side, we only need an input that we want to send $V$ and the rest of the components are standard. They can be designed separately and instantiated.

#Doubt  At the Receiving side, we get the output after the $A\bar{B}$ gate (At the top right)



# Data synchronizer
