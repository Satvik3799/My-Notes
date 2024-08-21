In a BJT:
	Base has very thin in width. From the Emitter, the electrons are injected into the base and then to the collector. By diffusion, the concentration of Electrons will drop exponentially. But since the Base is very small, the change in concentration drop of electrons looks linear. and Effectively the electrons can flow and we get the Bipolar Junction current. 

We can notice the BJT kind of formation in the transistors with very small channel length. So the channel behaves like a Base.![[Pasted image 20240820184519.png]]
When a transistor is ON, it is the Drift current that dominates the total current and when it is OFF, the Diffusion current dominates.

In Earlier models, we assumed the OFF current to be 0. Now for small channels, we have to consider the OFF current due to the BJT formation.
#formula 
$$
\begin{align}
&I_{OFF} = I_{o}\;\exp\bigg( \frac{V_{GS}-V_{T}}{n \phi_{T}} \bigg) \bigg(1-\exp (\frac{-V_{DS}}{\phi_{T}})\bigg)\bigg(1+\lambda V_{DS}\bigg)\\
\end{align}
$$
 #concept By looking at this OFF-current equation, we can say that the leakage current will be affected by the Gate voltage ($V_{GS}$) and the Threshold voltage ($V_{TH}$) exponentially!! 
 If the Threshold voltage is reduced in order to increase the ON current capacity of the device, this will affect the exponential term in the OFF-Current equation and it would lead to more leakage current. This Sub-threshold Leakage Current will be in nano Amps (nA).

# Defining Switch like behaviour

 Ideal switch like behaviour is, below $V_{TH}$ the Transistor is OFF, and just after $V_{TH}$ the Transistor can conduct current of its maximum capacity. The graph goes abruptly upwards, right after $V_{TH}$.
#### Sub-threshold slope 
The linear graph was exponential, but it can be seen as a very little change when we plot it in a logarithmic graph, but since we want to use the logarithmic graph, the linear change is not quite visible.
![[Pasted image 20240821142842.png]]
Since the Sub-threshold leakage current is in orders of $nA$, and the ON current is in the order of $\mu A$ we need to plot a logarithmic graph.
We are interested in the small changes before the current becomes very large. 

Taking $log_{10}$ of the $I_{OFF}$ equation, we get:

$$
\begin{align}
&log_{10}(I_{D}) = log_{10}(I_{0}) + \bigg(\frac{V_{GS}-V_{T}}{n \phi_{T}} \bigg) log_{10}(e) + log_{10} (1) - \bigg( \frac{-V_{DS}}{\phi_{T}} \bigg)log_{10}(e) \\
\end{align}
$$
We want to get the slope with respect to the X-axis ($V_{GS}$), in order to find the small changes in the current due to applied gate voltage $V_{GS}$.

$$
\begin{align}
&\frac {d\;log_{10}(I_{D})}{d\; V_{GS}} = 0 + \bigg(\frac{1}{n \phi_{T}} \bigg) log_{10}(e) + 0 - 0 \\
\end{align}
$$

So we get the slope as:

$$
\begin{align}
&s = \frac{1}{\bigg(\frac{log_{10}(e)}{n \phi_{T}} \bigg)} \\
&s = n \phi_{T} \times log_{e}(10)\\
\end{align}
$$
Here, $n$ is the non-ideality factor, which is 1.5 for planar devices. For a FinFET, this number is lower.


$$
\begin{align}
&s = n \phi_{T} \times log_{e}(10) = (1.5) \times (2.3 \times 10^{-3}) \times (0.4345) \approx 90 \frac{mV}{decade}  \\
\end{align}
$$

#concept This reads, I have to reduce the Gate Voltage ($V_{GS}$) by $90 \; mV$ in order to drop the current by a factor of 10 to turn off the transistor. So how good a transistor is, can be determined by this number. 

But, we cannot keep reducing the $V_{GS}$, at some point a non ideality kicks in, which will lead to increase in current rather than decrease. This non ideality is also known as [[Gate Induce Drain Leakage (GIDL)]].![[Pasted image 20240821142744.png]] As a designer, we should be aware of this GIDL point of our device.
