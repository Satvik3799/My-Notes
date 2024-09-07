28-08-2024 18:27

Status:

Tag:


# Trip Point

![[Pasted image 20240907162956.png]]


#### Noise margin

$V_{M}$ is the trip point. Idealy we consider it to be $V_{DD}/2$. 
#formula 
$$
\begin{align}
&V_{IH}= V_{M} \bigg ( 1-\frac{1}{g} \bigg) \\
&V_{IH}= V_{M} + \bigg (\frac{V_{DD}-V_{M}}{g} \bigg)\\
\end{align}
$$

From the noise margin relations: 
#formula 
$$
\begin{align}
& (NM)_{H}= V_{OH} - V_{IH} \\
& (NM)_{L}= V_{IL} - V_{OL} \\
\end{align}
$$
If trip point voltage ($V_M$) is increased, then $V_{IH}$ and $V_{IL}$ will increase. 
So we can say that, the High logic noise margin will decrease whereas the Low level noise margin will increase.



# References:

