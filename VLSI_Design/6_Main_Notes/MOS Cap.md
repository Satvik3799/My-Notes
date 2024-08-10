12-07-2024 13:40

Status: 

Tag:


# MOS Cap



![[Drawing 2024-07-12 13.43.17.excalidraw]]


##### Accumulation ($V_{GB}<0$) :
**When $V_{GB}$ is negative**, the gate's metal plate will have more electrons and it will attract holes from the P-substrate. So the concentration of Holes will be more than the deep bulk (Body) of the substrate.

##### Depletion ($V_{GB}>0$) : 
<span style="color: red;"> Where is the depletion region? Where is N-type region and P-type region </span> #Doubt
When $V_{GB}$ is positive, the gate's terminal will have more holes and to terminate the electric fields electrons will get attracted. So at the surface, the electron concentration will be more than the deep bulk of the substrate.
Another perspective could be, the **[[Immobile ions]] (Acceptor atom)** are there because the holes are repelled. These acceptor atoms have become negative in charge, because they have taken an electron from the Si. So the electric fields terminate at ions located at different places.
![[Pasted image 20240713194018.png]]
We know from the Boltzmann-Maxwell relationship: #formula 
## $\frac{n_{surface}} {n_{bulk}}=  {exp} \bigg \{ {{\frac{q\psi_s}{K_{B}T}}}\bigg \}$

Now the Surface and the bulk has different electron concentration. With very small Voltage ($\psi_s$) change, it can lead to exponential increase in the electron concentration at the surface. 
After a certain point, no matter what the voltage is the concentration of the electron at the surface will not change and it will saturate. This point is observed at $n_{surface}= N_A$, i.e when the electron concentration at the surface becomes same as hole concentration in the substrate. So essentially we have inverted the surface region.

##### Inversion ($V_{GB}> \psi_{s}$): #formula

## $\psi_{s}= \frac{K_{B}T}{q} \ln \bigg ({\frac {n_{surface}} {n_{bulk}}}\bigg )$ 
Considering the scenario when, $n_{surface}= N_A$ 


### Calculating the Threshold Voltage ($V_{th}$):

- Gate potential needed to **"Invert"** the surface.

#### $V_{GB} = \psi_{s}+ \psi_{ox}$
Where $\psi_{s}$ is the surface potential and $\psi_{ox}$ is the oxide potential.

##### Calculating the Oxide potential:
From the relation, $Q = CV$. 
Q is the net charge involved, which is the Charge accumulated by inversion and the Depletion charge. So the net charge $Q = Q'_{D}+Q'_I$, where $Q'_D$ and $Q'_I$ defines absolute charges.

The Oxide capacitance is given by, $C = \frac{\epsilon A}{D}$. 
$C_{ox}= \frac{\epsilon_{r} \epsilon_{0} W L }{t_{ox}}$

The Oxide potential is defined as:
$$
\psi_{ox} = \frac{-(Q'_{D} + Q'_{I})}{C'_{ox}}
$$

We want to use capacitance with normalized area, we do it by defining Charge Per Unit Area. So eventually, we can write $C_{ox}= \frac{\epsilon_{r} \epsilon_{0}}{t_{ox}}$

And define Depletion Charge as, 
$$Q'_{D}= qN_A(WLW_D)$$Where $W_D$ is the width of the depletion region.  #Doubt Why Si's permittivity is taken and not SiO2? Lec3-27:49
$$W_D= \sqrt{\frac{2\epsilon_{si}|{\psi_s}|}{qN_A}}$$
Here, $|\psi_{s}|$ is taken. It is positive for an NMOS and negative for a PMOS.
So,

$$
\begin{align}
Q'_{D} = qN_A(WL)\sqrt{\frac{2\epsilon_{si}|{\psi_s}|}{qN_{A}}}\\
Q'_{D} = (WL)\sqrt{{2\epsilon_{si}|{\psi_s}|}{qN_A}}
\end{align}
$$
So, we can write charge per unit area.
$$
\frac{Q'_{D}}{WL} = Q_{D}= \sqrt{{2\epsilon_{si}|{\psi_s}|}{qN_A}}
$$

We can define Inversion Charge as, #formula #Doubt How did this relation come?
$$
\begin{align}
&Q'_{I}= C'_{ox}(V_{GB}- V_{TH})\\
&-\frac{Q'_{I}}{C'_{ox}} = V_{GB} - V_{TH}
\end{align}
$$

So,
The Oxide potential is defined as:
$$
\psi_{ox} = \frac{-(Q'_{D} + Q'_{I})}{C'_{ox}}
$$
We know that: $V_{GB}= \psi_{s}+ \psi_{ox}$
$$
\begin{align}

&V_{GB}= \psi_{s} - \frac{(Q'_{D} + Q'_{I})}{C'_{ox}}  \\
&V_{GB}=\bigg( \psi_{s}- \frac{Q'_D}{C'_{ox}} \bigg)- \frac{Q'_{I}}{C'_{ox}} \\
&V_{GB}=\bigg( \psi_{s}- \frac{Q'_D}{C'_{ox}} \bigg) + V_{GB} - V_{TH} \\
&0=\bigg( \psi_{s}- \frac{Q'_D}{C'_{ox}} \bigg) - V_{TH} \\
&V_{TH}=\bigg( \psi_{s}- \frac{Q'_D}{C'_{ox}} \bigg) \\
&V_{TH}=\bigg( \psi_{s}- \frac{1}{C'_{ox}}\sqrt{{2\epsilon_{si}|{\psi_s}|}{qN_A}} \bigg) \\
\end{align}
$$

The conclusion is :
START
In order to have a current flow in the form of free electrons, we need to invert the channel/surface. To do that, we first deplete the surface, meaning $V_{GB}>0$. That work that the gate voltage has to do in order to invert the channel is called the **Threshold Voltage**. 
So even if we apply a large amount of voltage, it is only $V_{GS}-V_{TH}$ amount of volage is going to be available for us to create more inversion charge and thereby increase the current flow in the channel/surface. Below the Threshold voltage, there is no inversion charge hence no current can flow. 
$$
V_{TH}=\bigg( \psi_{s}- \frac{1}{C'_{ox}}\sqrt{{2\epsilon_{si}|{\psi_s}|}{qN_A}} \bigg)

$$
END


With the MOS Cap only, we cannot have a current flow even after inverting the surface because there is an Oxide layer in between. So a four terminal device called [[MOS Transistor]] was developed.

# References:

