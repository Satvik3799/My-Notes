21-08-2024 16:43

Status:

Tag:


# Substate Leakage

![[Substate and Gate Leakage 2024-08-21 16.45.19.excalidraw]]

When $V_{BS}$ is increased, it supplies electron to the channel which will make it easier for the conduction to start, leading to a decrease in $V_{TH}$. The decrement in $V_{TH}$ will lead to an increment in the drain current $I_{D}$. (Ref: [[MOS Transistor]])

Basically, the PN junctions are getting forward biased due the $V_{BS}$ being positive. This is helping in reducing the Threshold voltage, but it also leads to more leakage current.

#concept Varying $V_{BS}$ to lower the threshold voltage is a valid method, but it leads to more leakage current. 
![[Substate and Gate Leakage 2024-08-21 18.22.24.excalidraw]]




# Gate Leakage

$$
\begin{align}
&C = \frac{\epsilon_{0}A }{t_{ox}} \\
\end{align}
$$
As the devices scaled down, the Gate oxide thickness needed to be increased and High K materials needed to be used, because we wanted the gate capacitance to remain the same. 
Earlier, the Gate current used to be zero; but as the devices scaled down, and the Quantum mechanical effects started to come up due to thin gate oxides which would lead to electrons tunnelling through the Gate oxides. This led to a Gate Current $I_{G} > 0$. 

#concept We wanted Gate oxide thickness to increase while keeping the capacitance the same.

Hafnium Di-oxide ($HfO_2$) was used instead of Silicon Dioxide. HfO2 has $\epsilon_{r} = 12$, which means we can increase the $t_{ox}$ by a factor of 3; because SiO2 has $\epsilon_{r}=4$.


# References:

