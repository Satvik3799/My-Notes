09-08-2024 15:40

Status:

Tag:


# Drain Induced Barrier Lowering (DIBL)

In a [[Short-Channel MOS Device]] because of the depletion region eating into the channel due to the Drain voltage, the threshold voltage also changes.


$$
\begin{align}
& V_{DS1} = 0.1V_{DD} \rightarrow V_{TH}=V_{T_{lin}} \\
& V_{DS2} = V_{DD} \rightarrow V_{TH}=V_{T_{sat}} \\
\end{align}
$$

For the transistor with $V_{DS1}$, the channel will not get eaten more than the device with $V_{DS2}$. So the device with $V_{DS1}$ will have to "work more"  in order to invert the channel and state conducting i.e. the threshold voltage will be more.
For a Long Channel MOS Device ([[MOS Transistor]]), $V_{T_{lin}}$ and $V_{T_{sat}}$ will be the same.
So the drain voltage causes the $V_{TH}$ to reduce and hence it is called **Drain Induced Barrier Lowering (DIBL)**.

$$
\eta =DIBL=\frac{Vt_{lin}-Vt_{sat}}{V_{DD}-0.1V_{DD}}
$$
Now the threshold voltage becomes:

$$
\begin{align}
& V_{TH}=V_{THO}+\gamma (\sqrt{|V_{SB}+\psi_{s}|} - \sqrt{|\psi_{s}|}) - \eta V_{DS}\\
\end{align}
$$
As $V_{DS}$ increases, the Threshold voltage reduces; hence the negative sign.

For a long-channel device, the $\eta$ coefficient will be small enough to be neglected. 

#concept Intuitively DIBL feels like a good thing that we are able to get more current out of the transistor for a relatively low threshold voltage, but this is not a controlled way of getting the current. This also increases the leakage current.


## P+ halo implant for NMOS

Since the terminals are made of N+ regions, when more $V_{DS}$ is applied the depletion region eats more of P substrate than the N+ region of the terminal. We want that it doesn't get more into the P substrate but it is okay if it goes into the N+ region. So we put a P+ halo implant after the N+ region. Now when $V_{DS}$ is applied, the depletion barrier will move more into N+ region and less into the P substrate. We put it at the both terminals of the transistor because where we apply the more potential decides the drain an source of the transistor device.
![[Pasted image 20240809163112.png]]

With channel length being less, the $V_{TH}$ will reduce due to Short-channel effects (SCE), but due to the P+ halo implant we will see an increment in the $V_{TH}$ which will lead to the bump shown in the following graph. This is AKA **Reverse Short Channel Effect**.
![[Pasted image 20240809163530.png]]


# References:

