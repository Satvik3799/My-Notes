20-07-2024 19:03

Status:

Tag:


# Short-Channel MOS Device


![[Short-Channel MOS Device 2024-07-20 20.18.44.excalidraw]]


With time, in order to get better PPA the devices reduced in size. The channel length reduced. Earlier, due to long channel length, the depletion region of Drain and Source side PN junction did not matter; But now since the channel is getting narrow, this depletion region matters.
When a positive voltage is applied at Drain end leads to a Reverse-bias for the $N^{+}$ of the Drain end and the $P$ of the substrate. This Reverse-bias means that the depletion width is more, meaning it will reduce the channel even more; so effectively the channel length reduces from what it was.

![[Short-Channel MOS Device 2024-07-21 10.28.35.excalidraw]]

Now the Gate voltage can be a low and the channel can be inverted with a low voltage, i.e. the Threshold Voltage has come down. Because a part of the channel is already inverted by the applied drain voltage.

#concept With shortening of the channel, the threshold voltage has come down and now the Threshold Voltage is a function of Drain Potential. Earlier, neither the Drain current in Saturation region nor the Threshold voltage was a function of Drain Potential.


## Channel Length Modulation (CLM):

The Short-channel effects take place only when the $V_{DS}$ is high. For more $V_{DS}$ the depletion region in the P-sub will be more because its a reverse bias condition. So the Short-channel effect is considered only for Saturation mode.

Long Channel Equation in Saturation mode: (Not a function of $V_{DS}$)
$$
I_{D}= \frac{1}{2} \mu_{n}C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^2
$$
We again use [[Empirical Equation]] in order to simplify the inclusion of $V_{DS}$.
The Channel length is reduced when $V_{DS}$ is increased. So we can write the new channel length to be $L-\Delta L$. This new channel length has to be a function of $V_{DS}$, so we use an Empirical coefficient to include the $V_{DS}$ variable.
$$
\bigg (\frac{\Delta L}{L} \bigg) \rightarrow \lambda \; .\; V_{DS}
$$
The $\lambda$ is called a CLM parameter.
$$

\begin{align}

&I_{D}= \frac{1}{2} \mu_{n}C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^{2}\\
&I_{D}= \frac{1}{2} \mu_{n}C_{ox}\frac{W}{(L - \Delta L)}(V_{GS}-V_{TH})^2\\
&I_{D}= \frac{1}{2} \mu_{n}C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^{2}\bigg ( 1 + \frac{\Delta L}{L} \bigg )\\
&I_{D}= \frac{1}{2} \mu_{n}C_{ox}\frac{W}{L}(V_{GS}-V_{TH})^{2}\bigg ( 1 + \lambda V_{DS} \bigg )\\
\end{align}

$$

So for a Short-channel transistor, the current will be slightly more, by the amount of $\lambda$, than the Long-channel transistor in the saturation mode.
![[Pasted image 20240721153024.png]]


#concept With Device scaling down, the $V_{DD}$ also reduced along with technology node due to the short-channel effect.

# References:

