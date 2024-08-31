26-08-2024 15:03

Status:

Tag:


# Complimentary Logic

#concept An NMOS can **charge** a capacitor only till $V_{DD} - V_{TH}$. So NMOS is used as an Active High switch, as it can pass logic 0 nicely. 
#concept A PMOS can **discharge** a capacitor only till $|V_{TH}|$. So PMOS is used as an Active Low switch, as it can pass logic 1 nicely.
### NMOS Transistor limitation
![[Pasted image 20240826154950.png]]

When Gate and Drain are at $V_{DD}$, and we charge the output capacitor, the Capacitor can only charge up to $V_{DD} - V_{TH}$. The reason is, if the got charged more than that, it'd be a short circuit situation due to Drain and Source being at the same voltage level and also we won't be able to distinguish between Drain and Source. 
#concept For the current to flow through Drain to Source, the Output capacitor voltage has to be less than $V_{DD}-V_{TH}$. 

The NMOS can only charge the capacitor until $V_{DD}-V_{C}(t)$ approaches $V_{DD} - V_T$​, where $V_T$​ is the threshold voltage. Beyond this point, $V_{GS}$​ is not sufficient to keep the NMOS in the conductive state, and the charging process slows down significantly.

###### When Discharging:
The source terminal of NMOS, was fixed at the GND, i.e. $V_{GS}$ was fixed.
###### When Charging:
The source terminal of NMOS, was not fixed but dependent on the Capacitor voltage.

### PMOS Transistor limitation

![[Pasted image 20240827105620.png]]



# Inverter

![[Pasted image 20240827113854.png]]

|      | $V_{GS}$          | $V_{DS}$         |
| ---- | ----------------- | ---------------- |
| PMOS | $V_{in} - V_{DD}$ | $V_{o} - V_{DD}$ |
| NMOS | $V_{in}$          | $V_o$            |

At all times, the current in PMOS should be same as current in NMOS, but in reverse direction. 
$$
\begin{align}
&I_{Dsn} = -I_{Dsp} \\
\end{align}
$$
##### When input is 0 i.e. $V_{in}= 0$:
- The NMOS turns off i.e. $I_{Dsn} = 0 A$. That means the current in PMOS must also be 0. 
- PMOS's $V_{DSp}$ must adjust itself such that the current through PMOS becomes 0 as well.
- To do that, if $V_{DSp}$ becomes 0, then the current, $I_{Dsp}$, will also become 0.
- so, For PMOS $$
\begin{align}
&V_{DSp} = V_{o}- V_{DD} \\
& 0 = V_{o}- V_{DD} \\
& V_{o} = V_{DD} \\
\end{align}
$$
- That means, capacitor voltage becomes $V_{DD}$ to maintain the same current in NMOS as well as PMOS.

##### When input is 0 i.e. $V_{in}=V_{DD}$:
- The PMOS turns off i.e. $I_{Dsp} = 0 A$. That means the current in NMOS must also be 0. 
- NMOS's $V_{DS}$ must adjust itself such that the current through NMOS becomes 0 as well.
- To do that, if $V_{DSn}$ becomes 0, then the current, $I_{Dsn}$, will also become 0.
- so, For NMOS $$
\begin{align}
&V_{DSn} = V_{o} \\
& 0 = V_{o} \\
& V_{o} = 0 \\
\end{align}
$$
- That means, capacitor voltage becomes $0V$ to maintain the same current in NMOS as well as PMOS.


# Voltage Transfer Characteristics (VTC)

#concept $V_{Tp}$ is -ve and $V_{Tn}$ is +ve, but they have same magnitude.
Input is swept from Low to High and the output voltage is observed.
Keep in mind, these 5 relations
$$
\begin{align}
& I_{Dsp} = - I_{Dsn} \\
& V_{GSn} = V_{in}\\
& V_{DSn} = V_{o}\\
& V_{SGp} = V_{DD} - V_{in} \\
& V_{SDp} = V_{o} - V_{DD}\\
\end{align}
$$
After the input voltage crosses $V_{Tn}$ , the NMOS starts to conduct slowly. This means that there must be some decrement in $V_{DS}$ across the NMOS, since the current is now flowing through it. Since $V_{DSn}=V_{o}$ , the output voltage starts to decrease.  

After the input voltage crosses $V_{DD} - V_{Tp}$ , the NMOS is fully ON and PMOS turns OFF.
# References:

