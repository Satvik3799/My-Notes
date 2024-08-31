
### As width of a transistor scales, so will every capacitance of the transistor

We want to plot a graph of Gate capacitance as the Gate voltage varies.

When $V_{GS}<0$, the MOSFET is in cut-off mode, where the capacitance will stay constant. It will just be the parallel plate capacitance. For negative applied voltage, the electrons will come to the Gate terminal plate and attract the already abundant holes inside the P-substrate. ![[Pasted image 20240824003513.png]]
The capacitance can be given by:

$$
\begin{align}
&C_{0}=C_{ox}WL \\
\end{align}
$$
Where $C_{ox}$ is given as: ($t_{o}$ is the thickness of the oxide)
$$
\begin{align}
& C_{ox} = \frac{\epsilon_{si}}{t_o} \\
\end{align}
$$


As the Gate voltage increases and nears the threshold voltage, the channel starts to accumulate the negative charge in the P-substrate near to the channel. So the capacitance will be the series of Oxide capacitance and the depletion capacitance. So now, the capacitance will reduce.![[Pasted image 20240824003500.png]]


After it crosses the threshold voltage and is in the linear region, the Capacitance again increases. In the linear region, the channel has already been inverted; and we want to worry about only the linear region's capacitance.
![[Transistor Capacitances 2024-08-24 00.38.43.excalidraw]]



## Capacitances of a Transistor:
![[Pasted image 20240824003939.png]]

The gate capacitance can be given by, 

$$
\begin{align}
&C_{G}= C_{GS}+ C_{GD}+C_{GB} \\
\end{align}
$$

**For Digital Design POV, this would be considered $C_{G}=C_{ox}WL$**
Otherwise, 
Saturation: $C_{GS}$ will be more than the $C_{GD}$ and $C_{GB}$. 
Linear: $C_{GD}$ will be more than the the $C_{GD}$ and $C_{GB}$. 

When Annealing is done, in order to reduce the defects. The Silicon Wafer is heated to high temperatures. The atoms spread due to the heat and the $N^+$ regions expand. So the channel length reduces.
![[Pasted image 20240824004802.png]]
There comes an overlap capacitance when this happens, which is given by $C_{ov}=C_{ox}WL_{ov}$

So the new Gate Capacitance now can be given by:

$$
\begin{align}
& C_{G}^{'}= C_{G}+2C_{ov} = C_{ox}WL + 2C_{ox}WL_{ov} \\
\end{align}
$$
$L_{ov}$ can be considered as a Technology parameter.

$$
\begin{align}
& C_{G} = C_{ox}WL + 2C_{ox}WL_{ov} \\
& C_{G} = C_{ox}WL + 2C_{ov}W \\
\end{align}
$$
Here, the Units of $C_{ox}$ and $C_{ov}$ are different.

$$
\begin{align}
&C_{ox} \rightarrow \frac{fF}{\mu m^{2}}\;\;\;\;\;\; \& \;\;\;\;\;\; C_{ov} \rightarrow \frac{fF}{\mu m}  
\end{align}
$$
Eventually, the Technology parameters and the Design parameters can be separated.

$$
\begin{align}
& C_{G} = (C_{ox}L + 2C_{ov})\;W \\
\end{align}
$$

#concept If $W$ increases, the Gate capacitance will increase too.


## Diffusion Capacitances

If $C_{j0}$ is the **capacitance per unit area** of a PN junction, then the net capacitance of a PN junction will be given by:

#formula 
$$
\begin{align}
&C_{PN}=C_{j0}WL \\
\end{align}
$$

Transistors are 3D, we need to look at where all diffusions are taking place and then figure out different capacitances.
![[Pasted image 20240824165827.png]]

Bottom Plate Capacitance: 
$$
\begin{align}
& C_{BOT} = C_{j}WL_{s} \\
\end{align}
$$
Side Wall Capacitance:
$$
\begin{align}
&C_{SW} = C_{j}X_{j}(W+2L_{s}) \\
&C_{SW} = C_{jsw}(W+2L_{s}) \\
\end{align}
$$
Here, $C_{j}X_{j}$ can be considered a technology constant, and make $C_{jsw}$.

So the Drain-Body and Source-Body Capacitances can be given by: 
$$
\begin{align}
&C_{SB}=C_{DB} = C_{BOT}+C_{SW} \\
& = C_{j}WL_{s} + C_{jsw}(W+2L_{s}) \\
\end{align}
$$
The SI units of $C_{j}$ and $C_{jsw}$ are: 
$$
\begin{align}
&C_{j} \rightarrow \frac{fF}{\mu m^{2}}\;\;\;\;\;\; \& \;\;\;\;\;\; C_{jsw} \rightarrow \frac{fF}{\mu m}
\end{align}
$$




The expression for $C_{j}$ is given here. Which says
#concept When $V_{SB}$ is increased, which is the reverse bias, the capacitance drops. 
![[Pasted image 20240824171739.png]]