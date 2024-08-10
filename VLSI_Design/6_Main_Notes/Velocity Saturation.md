30-07-2024 00:45

Status:

Tag:


# Velocity Saturation

#fact  #concept In the Si lattice the electrons cannot achieve drift velocity more than $10^{5} \;{m/s}$ . We want to convert this limit into Maximum Permissible $V_{DD}$ Voltage level.

There is a critical electric field, beyond which the saturation takes place. So,
$$
\begin{align}
&v_{d}= \mu_{e}E \\
&v_{d_{saturation} }= \mu_{e}E \\
&v_{d_{saturation} }= \mu_{e} \bigg (  \frac{V_{sat}}{L} \bigg) \\
&V_{sat}=   \bigg (  \frac{v_{d_{saturation}} \times L}{\mu_{e}} \bigg) \\
\end{align}
$$
Now the highest drift velocity is associated with highest voltage we can apply across the Drain and Source terminal $V_{DS}$.
#concept #formula If $V_{DS}$ is applied more than this voltage, then there will be no more increase in the acceleration of the electrons hence no more increase in the drain current.$$V_{sat}=   \bigg (  \frac{v_{d_{saturation}} \times L}{\mu_{e}} \bigg)$$
When $V_{GS}$ is  just above the threshold voltage, the transistor will be in the Triode/linear region. It will behave normally, with $V_{DS}$ when going above $V_{GS}-V_{TH}$ the transistor going into saturation region. The $V_{GS}-V_{TH}$ line shown in the figure is for $V_{GS}3$. 
For $V_{GS}3$ the current should've saturated after the $V_{GS}- V_{TH}$, but it saturated at the $V_{sat}$ voltage level applied at $V_{DS}$. This lowering of drain current is due to Velocity Saturation.

![[Drawing 2024-07-30 19.57.24.excalidraw]]

Now we need to incorporate this effect into the drain current equation for out transistor model.


$$
\begin{align}
&I_{D}= \frac{1}{2} \mu_{n}C_{ox}\frac{W}{L}(V_{min}) \bigg [ (V_{GS}-V_{TH}) - \frac{V_{min}}{2} \bigg] \bigg ( 1 + \lambda V_{DS} \bigg )\\
&Where, \\
&V_{min}= min(V_{GS}-V_{TH}, V_{DS}, V_{sat})
\end{align}

$$
When in Saturation mode,
$V_{min} =  V_{GS}-V_{TH}$ 
When in Linear mode,
$V_{min} =  V_{DS}$ 

Here, $V_{TH}$ to be considered is the [[Empirical Equation]] of the threshold voltage.

Usually with 5 technology parameters, a foundry can characterise a transistor. Of course there are more complicated models, which has 100s of such parameters. A transistor model with these parameters is called **Level 1 Spice model**
1. $k_{n^{'}}= \mu_{e}C_{ox}$ - Si properties
2. $V_{D_{sat}}$ - Velocity Saturation
3. $\lambda$ - From Empirical equation of Drain Current.
4. $V_{THO}$ - From Empirical equation of threshold voltage.
5. $\gamma$ - From Empirical equation of threshold voltage.
# References:

