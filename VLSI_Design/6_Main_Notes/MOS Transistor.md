17-07-2024 10:19

Status:

Tag:


# MOS Transistor


![[Pasted image 20240717212131.png]]

#concept  When we apply an Electric-field, it is not necessary that the current will flow. When the field is applied, the Charges move randomly, The Brownian Motion. Generation and recombination is happening constantly. So the charges move with a velocity with a variable of Electric-filed and to account for this random motion, we use the term [[Mobility]], the velocity is called the [[Drift Velocity]].
$$
v_{d}= \mu E
$$
# The Current Equation

At some $x$ distance from the source side, the voltage is $V_{x}$.
$$
\begin{align}
&V(0) = 0 \\
&V(L) = V_{D}
\end{align}
$$
The current is only in the inverted channel, so only inversion charge is there to support the current flow. So,
$$
\begin{align}
&Q_{I}= -C_{ox}(V_{G}-V_{TH}-V) \qquad (Charge \; per \; unit \; area) \\
&Q_{I}= \frac{Q'_{I}}{WL} \\
&Q'_{I}= Q_{I}(WL)
\end{align}
$$
Current can be defined as $I = \frac{dQ}{dt}$

So,
$$
\begin{align}
&I_{D}= \frac{dQ'}{dt} = \frac{d}{dt} \bigg (-C_{ox}(V_{G}-V_{TH}-V) \;.\; WX \bigg) \\
&I_{D}=\bigg (-C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) \frac{dx}{dt}
\end{align}
$$
The term $\frac{dx}{dt}$ is the drift velocity:
$$
v_{d}=\frac{dx}{dt}=\mu E
$$
Where E is the applied electric field and $\mu$ is the [[Mobility]].
The electric field can be written as, $V=Ed$, where d is the distance.

$$
\begin{align}
&I_{D}=\bigg (-C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) \frac{dx}{dt} \\
&I_{D}=\bigg (-C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) (-\mu_{e}E) \qquad (-ve \;sign \; due \; to \; mobility \; of \; electorns)  \\
&I_{D}=\bigg (C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) (\mu_{e}\frac{dV}{dx}) \\
&I_{D}=\bigg (C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) \mu_{e} \; ({dV}) \\
&I_{D}\; (dx)=\bigg (C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) \mu_{e} \; ({dV}) \\
\end{align}
$$
Integrating Left side for the whole length of the channel and Right side for the entire applied voltage.
$$
\begin{align}
&\int_0^L I_{D}\; (dx)= \int_0^{V_{d}} \bigg (C_{ox}(V_{G}-V_{TH}-V) \;.\; W \bigg) \mu_{e} \; ({dV}) \\
&I_{D}L = \mu_{n}C_{ox}{W} \bigg [ (V_{GS}-V_{TH})V_{DS}- \frac{V_{DS}^{2}}{2}  \bigg]
\end{align}
$$

So the Current Flow in the Channel is given by:
### Linear Region Current Equation ($0 < V_{GS}< V_{TH}$  )

$$
I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ (V_{GS}-V_{TH})V_{DS}- \frac{V_{DS}^{2}}{2}  \bigg]
$$

#concept PN junction has drift and diffusion current both, and due to the diffusion current we have the exponential rise of current relationship. But here, only drift current is there.

At the Source end:
Source is kept at Ground potential. $V_{GS}-V_{TH}$ causes the channel to invert and eventually allows the current to flow.

At the Drain end:
Drain is kept at a potential $V_{DS}$. The effective voltage at the drain end is $V_{GS}-V_{TH}-V_{DS}$

#concept If we keep increasing $V_{DS}$, then:
For $V_{DS} < V_{GS}-V_{TH}$ : The drain end will be positive and the current will increase quadratically.
For $V_{DS} > V_{GS}-V_{TH}$ : The drain end will be negative and the current will saturate. (**[[Pinch-Off region]]**)

In the saturation region, the current equation becomes:
When $V_{DS}=V_{GS}-V_{TH}$
$$
\begin{align}
&I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ (V_{GS}-V_{TH})V_{DS}- \frac{V_{DS}^{2}}{2}  \bigg]\\
&I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ (V_{GS}-V_{TH})(V_{GS}-V_{TH})- \frac{(V_{GS}-V_{TH})^{2}}{2}  \bigg]\\
&I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ \frac{(V_{GS}-V_{TH})^{2}}{2}  \bigg]\\


\end{align}
$$

So The current equations are:

For Linear Region: $V_{DS} \leq V_{GS}- V_{TH}$
$$
I_{D} = \mu_{n}C_{ox}\frac{W}{L} V_{DS} \bigg [ (V_{GS}-V_{TH})- \frac{V_{DS}}{2}  \bigg]
$$

For Saturation Region: $V_{DS} > V_{GS}- V_{TH}$
$$

I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ \frac{(V_{GS}-V_{TH})^{2}}{2}  \bigg]

$$
# Body Effect:

When we consider the Body effect, the above current equations change.
From the [[MOS Cap]] concepts, we know that:
$$
\begin{align}
&V_{TH}= \psi_{s}+ \psi_{ox}\\
&V_{TH}= \psi_{s}+ \frac{1}{c_{ox}} \sqrt{2 \epsilon_{si} q N_{A}|\psi_s|}\\

\end{align}
$$
![[Pasted image 20240720173820.png]]

#concept The body terminal is always kept the same as the Source terminal. By changing the voltage at the body terminal we can change the Threshold Voltage $V_{TH}$ of a device. 
For an NMOS, the body terminal is kept at ground. But if the Body terminal is at a higher potential than Source, i.e. $V_{S}- V_{B}= V_{SB}>0$ , then the body terminal will have already provided some electrons to invert the channel and hence the Gate voltage needs to do lesser work, work of inverting the channel, to invert the channel. Hence the Threshold Voltage $V_{TH}$ reduces. 

When we include the body effect, the threshold voltage term will need to be modified. We use an [[Empirical Equation]] to do it. 

$$
V_{TH} = V_{THO} + \gamma (\sqrt{|\psi_{s}+ V_{SB}|} - \sqrt{|\psi_s|})
$$
Here, $V_{THO}$ is the Threshold Voltage $V_{TH}$ at $V_{SB} = 0$. 
$\gamma$ , unit $\sqrt{V}$ , is an empirical body effect coefficient, which means doesn't have an accurate physical interpretation. ([[Empirical Equation]])
For NMOS - $\gamma > 0$ 


# $I_{D}\;-\; V_{DS}$ Graph


For Linear Region: $V_{DS} \leq V_{GS}- V_{TH}$
$$
I_{D} = \mu_{n}C_{ox}\frac{W}{L} V_{DS} \bigg [ (V_{GS}-V_{TH})- \frac{V_{DS}}{2}  \bigg]
$$

For Saturation Region: $V_{DS} > V_{GS}- V_{TH}$
$$

I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ \frac{(V_{GS}-V_{TH})^{2}}{2}  \bigg]

$$

#concept  As $V_{GS}$ increases, the point at which the device goes into saturation moves, i.e. $V_{DS}$ at which the saturation occurs changes. The gap increases Quadratically, as we can see the $(V_{GS}-V_{TH})$ term is quadratic in the equations.

![[Pasted image 20240720184445.png]]


# $I_{D}\;-\; V_{GS}$ Graph


For Linear Region: $V_{DS} \leq V_{GS}- V_{TH}$
$$
I_{D} = \mu_{n}C_{ox}\frac{W}{L} V_{DS} \bigg [ (V_{GS}-V_{TH})- \frac{V_{DS}}{2}  \bigg]
$$

For Saturation Region: $V_{DS} > V_{GS}- V_{TH}$
$$

I_{D} = \mu_{n}C_{ox}\frac{W}{L} \bigg [ \frac{(V_{GS}-V_{TH})^{2}}{2}  \bigg]

$$

#concept  Unlike before, the Saturation region is first and then the linear region. When $V_{GS} < V_{TH}$, the Current doesn't flow. As the $V_{GS}$ increases, so does the Current. This relationship is Quadratic in nature until $V_{GS} = V_{DS}+ V_{TH}$. After that point, the Current increases linearly with increment in $V_{GS}$.  

 ![[Pasted image 20240720185650.png]]

#concept In an NMOS, the source terminal sources the electrons, hence the name source and the drain collects the electrons coming from the source terminal. The conventional current flow might be the Drain to Source but the flow of electron is from the Source to the Drain.
# References:

