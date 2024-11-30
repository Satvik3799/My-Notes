02-08-2024 16:02

Status:

Tag:


# Setup Time and Hold Time

In practical scenarios, we use an Edge-triggered Flip-flop. It is realised using a Master-Slave configuration. 
![[Pasted image 20240802162757.png]]

Because of this configuration, setup and hold time comes into picture. 

We use a bottom-up approach for this concept. From Cross-coupled SR latch (Can be found here [[Metastability]]) to D latch (Level triggered) to Master-slave D Flip-flop (Edge triggered)


# D-latch

A single D latch or transparent latch is ![[Pasted image 20240802162152.png]]

The D input avoids [[Race Condition]] because at the other input to the SR latch will always be inverse of the first. 

### Propagation Delay


$$
\begin{align}
&t_{pd}=max(t1+t3 , t2)+ loop\;delay \\
&t_{pd}=max(t1+t3 , t2)+ t4 +t5 \\
\end{align}
$$


## Worst Case Setup

![[Pasted image 20240802162146.png]]

#Doubt What would happen if latch sets with in worst case setup?

As long as the clock is high, the input at D will get reflected at Q, i.e. Being transparent as long as clock is high. 
As long as clock becomes high, the latch will set according to its first input after $t_a$ time.
The last input that we give via D, must be before $t_a$ time before the clock pulse goes down. We already know the pulse width of the clock signal. We need to make sure that we give the last signal before $t_a$ time or else it could get into [[Metastability]]. 

We say that, 

#concept The Data has to be setup this much time before the clock goes 1 to 0 transition. This is called **Setup time**

In reality, we also have an inverter before the clock is applied to the latch.
Consider an inverter after the clock signal. We can say that, till now the analysis was done on the CLK2 signal.

![[Pasted image 20240802163153.png]]

Now, when the CLK signal goes 0 to 1, the CLK2 signal will go 1 to 0.
The inverter will have some delay, which will cause another type of timing constraint called **Hold time**. 

The pulse width of CLK and CLK2 will be the same.
So, For CLK2 signal, we know when the data should not be changing to avoid metastable state (Setup time).
When we look at the CLK2 signal, we can get the Worst-case setup ($t_a$) for the latch. We know after what time the data should not be changing.
So we have this whole time period to work with.
![[Drawing 2024-08-02 18.03.59.excalidraw]]
Since the CLK signal actually is the main signal we work with, we analyse with respect to the CLK.

#concept We look at the falling edge of the CLK2 signal, because that's when we can see that when the last data should be sent to the latch. And Since this signals comes after an inverter, we can see that at the positive edge of the CLK signal we sample the data.

So right before the rising edge of CLK comes, the data should not change. And After the rising edge of CLK comes, the CLK2 will take $t_6$ amount of time to fall from 1 to 0. $t_6$ is the delay of the inverter. That $t_6$ is the Hold time of the edge triggered flip-flop. The data should be stable for another $t_6$ amount of time, the data should not change.

New setup time becomes $t_{a}-t_6$.

#concept The presence of inverter (U6) divides the **Worst-case setup** of latch into Setup and Hold time

# Master-Slave Edge Triggered flip-flop

![[Pasted image 20240802181637.png]]

#concept We can see that there are two inverters after CLK signal. In practical FF, the data sampling always happens at positive edge of the signal, and since Master-slave configuration uses an inverter to manage the operations between master and slave, we use one more inverter for the slave to have the original waveform as the CLK. Because the slave side is the one that is responsible to show the actual data sampled by the master side.

## Setup Time

![[Pasted image 20240802185202.png]]

The setup time is the same as we analysed for the single D-latch. 
The sampling of input data is done by the Master side. So when the CLK is rising the data should not be changing before $t_{a}-t_6$ time.
## Hold Time

![[Pasted image 20240802185146.png]]
The data should not change till $t_{6}$ amount of time. #Doubt The data need to be stable for $max(U6, U6-U1)=U6$
## Propagation delay ($t_{co}$) of this Edge triggered flip-flop

![[Pasted image 20240802183556.png]]

Propagation delay is the time it take for the FF to show output after the clock has been given, so we only need to consider the timings after the CLK signal has risen.
The master side will only sample the data and then pass it to the salve configuration.
After the data ha been sampled at the rising CLK edge, it takes the following amount of time for slave latch to set, i.e. the time to show output at Q.
$$
t_{6}+ t_{7}+ max(t_{8}, t_{9}) + t_{10}+ t_{11}
$$


![[Pasted image 20240802190103.png]]



# R-R path: Minimum Clock Period and Hold Time

![[Pasted image 20240803190752.png]]

![[Setup Time and Hold Time 2024-08-03 19.08.48.excalidraw]]

The Clock Period should be such that the Launch FF must have finished the propagation delay ($t_{cq}$) and Combinational circuit delay, then wait till setup time of the Capture FF.

The hold time should be such that the Capture FF must hold the data for at least the propagation delay ($t_{cq}$) and Combinational circuit delay. 

#concept We want to consider Max timing values of the $t_{comb}$ and $t_{cq}$ , to figure out the minimum clock period. Because we want to see how late the data can arrive, what is the worst case value for the late data arrival before the clock edge.
#concept  For Hold Time constraints, we consider Min timing values of the $t_{comb}$ and $t_{cq}$ . Because we want to see how early the data can arrive as we want the data to arrive a little late after the clock edge so that the next FF can properly sample the data.
# Considering Clock Skew

Clock skew is the difference in arrival time of a clock signal at different FFs.

### Min Path and Max Path

![[Pasted image 20240803184902.png]]

Consider FFs R1 (Launch FF) and R3 (Capture FF), R1 gets the clock before R3. The data path between them is called the Min path. Launch FF gets CLK before Capture FF.
Consider FFs R6 (Launch FF) and R2 (Capture FF), R2 gets the clock before R6. The data path between them is called the Max path. Launch FF gets CLK after Capture FF.

## Max path consideration

![[Pasted image 20240803192300.png]]
![[Setup Time and Hold Time 2024-08-03 19.24.16.excalidraw]]
Focus on the Boxed timings. The Capture FF clock has arrived early, we don't want that. So the clock frequency must be decreased in order to account for this much time. So the max value of Clock Skew that can make the capture FF trigger early must be considered. 

![[Pasted image 20240803193927.png]]

For Hold time, the capture FF must hold the data for another $t_{skew}$ amount of time more.


## Min Path

![[Pasted image 20240803194120.png]]

Since the Capture FFs clock is arriving late, the amount of skew can be subtracted from the propagation delay and comb delay because now it is working to our advantage. We can now increase the clock frequency.

For hold time, now the Max value of Skew will be considered because we want the clock to arrive as late as possible.
# References:

[[Metastability]]