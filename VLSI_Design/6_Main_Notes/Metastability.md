01-08-2024 12:31

Status:

Tag:


# Metastability


We know SR Latch has the following truth table and the circuitry.
![[Pasted image 20240801223847.png]]

If Reset(R)) is 0, the latch will take the value of Set(S) else it will output a 0.
#### No Change (Memory)
Once we give the inputs, either SR = 01 or SR = 10, then only we can go to the memory state.
When the input is S=0, R=0, and assuming Q=0. The Q is another input of NOR gate with R input. That 0 input will put that NOR gate's output to be 1, since R=0 too. NOR-2's output is another input to NOR-1 input. NOR-1 has one input 1, so it outputs a 0. 

#### From NAND SR-latch to NOT latch
If we look at the NAND gate implementation of SR-latch. We can see that it behaves like a NOT gate only, except for the inputs S=1, R=1
Notice, when $\overline{reset} = 0$, it outputs the inverse of the input $\overline{Set}$. (Only for inputs SR = 01 and 10)

We can re draw the circuit as,
![[Drawing 2024-08-01 22.51.13.excalidraw]]

When we draw the behaviour of this circuit on Graph.

As V1 increases, V2 should decrease, for inverter 1
As V2 increases, V1 should decrease, for inverter 2. (To see it, Rotate the image $90^\circ$ counter clock-wise and flip it horizontally.)

| Image 1                              | Image 2                              |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20240801225457.png]] | ![[Pasted image 20240801230336.png]] |

There are 3 points where the curves meet. 
1. The left most point - V2 = Vdd and V1 = 0
2. The right most point - V2 = 0 and V1 = Vdd
3. The middle point - Unstable point (**Metastability point**)

![[Pasted image 20240801230938.png]]


Assume that V1 is at p1. So for V1=p1 input, we get output of inv-1 as V2 = p2.
Now, For this V2=p2 input for inv-2, we get V1=p3, which is almost 0.
With this new input V1=p3 for inv-1, the output of inv-1 V2=p4. Which is almost Vdd.
So when we move left from the metastability-point, the output of inv-1 (V2) quickly goes to Vdd, i.e. When V1 is decreased from metastability-point, then output will quickly rise to Vdd. 
So when we move right from the metastability-point, the output of inv-1 (V2) quickly goes to 0, i.e. When V1 is increased from metastability-point, then output will quickly rise to 0. 

### Some common Questions


### 1. Is the metastability point behaviour same as that of the stable points?


### 2. What is the effect of metastability?

What happens if the FF or latch stays at the metastability point and it is driving an output?
- The output could be a non-logical voltage level between $V_{OL_{max}}$ and $V_{OH_{max}}$.  So the output driving any combinational circuit, the transistor's gate voltage could be such that it puts the transistor into Active Region, causing them to switch outputs (Oscillations), which would amplify small noise at the inputs.
- It could also drive another FF into metastability.
- It could be logical '0' or '1', but it may not represent the correct output value that was sampled at the input.
This is the effect of metastability of a Latch or FF.
![[Drawing 2024-08-02 01.18.53.excalidraw]]
### 3. Under what conditions, an SR latch or an SR FF can get into metastability?

- When an input is applied, it can be removed only when the same gate's second input gets the eventual input value. 
$$
input\;is\;given \rightarrow Gate1\;delay \rightarrow second\;input\; ready\;for \;Gate2 \rightarrow Gate2\;delay \rightarrow second\;input\; ready\;for \;Gate1   
$$
If it is removed before this loop delay. then the latch or FF can get into metastability.
We cannot say it for sure that for this condition the FF or latch will get into metastability, but we can say that for which condition the FF or latch will not get into metastability.
Think of it as this ball being pushed to the hill, if the force is too small, it won't climb the hill. If it is too much, the ball will cross the hill. The force has to be just perfect, in order to stop at the top of the hill. The hill is the metastability point.
![[Drawing 2024-08-02 02.07.48.excalidraw]]
### 4. How to reduce the probability of a FF entering the metastable state?




# Metastability behaviour

![[Pasted image 20240805133558.png]]
 
Case 1. D changes before the setup window. We get Output Q after $t_{cq}$ time period after clk edge.
Case 2. D changes during the setup window, but the FF goes into metastability but it will take longer time to get output reflected to the Q
Case 3. There is a timing window $T_0$ , in which the FF can get into metastability. This window is not fixed and it can vary depending on various things, such as Input to the FF, the Setup-hold time of FFs, if the change occurred very close to the rising edge of clk.

So we work with the probability of data changing within the time window $T_{0}$.  We are concerned about an Asynchronous input, coming in the time window $T_{0}$.
Assuming inputs are statistically independent of clk, i.e. it is not sure when the input will come during $T_{clk}$
The probability of the input changing in $T_{0}$ time window is $$ P_{meta}=\frac{T_{0}}{T_{clk}}$$
If the average rate of change of input is "$a$", then the frequency of metastable entry is: $T_{0} \times f \times a$

### Mean Time to Metastable Entry (MTTME)

How often the metastable entry is happening per unit time.


$$
\begin{align}
& MTTE = \frac{1}{Frequnecy \; of \; metastable \; entry}\\
& MTTE = \frac{1}{T_{0}\times f \times a}\\
\end{align}
$$
The metastable state reduces exponentially with time, i.e. FF can get out of metastability state to a stable state if given enough time, aka $t_{r}$ - the resolution time of Metastability.. It depends on the technology used to manufacture the FF. 
![[Pasted image 20240805135207.png]]

The probability of metastable FF remaining in metastability after time $t_{r}$ is - $$e^{-\frac{t_{r}}{\tau}}$$
#### Frequency of failure = $T_{0}\times f \times a \times e^{-\frac{t_{r}}{\tau}}$
This much times the FF is supposed to not get out of the metastable state after $t_{r}$ time.

#### Mean Time Between Failure (MTBF) = $\frac{1}{Frequency \;of \;failure} = \frac{1}{T_{0}\times f \times a \times e^{-\frac{t_{r}}{\tau}}}$  
Intuition - Essentially, if a system has a failure rate of X failures per hour, then on average, you can expect a failure every $\frac{1}{X}$ hours. This average time between failures is what we call the MTBF.
![[Pasted image 20240805141656.png]]

![[Pasted image 20240805142132.png]]

1st FF after input

| If Low frequency                     | If High frequency                    |
| ------------------------------------ | ------------------------------------ |
| ![[Pasted image 20240805142059.png]] | ![[Pasted image 20240805142109.png]] |

It means that on average, you can expect one instance of metastability that fails to resolve within the specified resolution time every 4.5 hours.
- **High Clock Frequency**: At a higher clock frequency (200 MHz), the MTBF is shorter (4.5 hours) because the flip-flop has less time to resolve metastability before the next clock edge.
- **Lower Clock Frequency**: At a lower clock frequency (100 MHz), the MTBF is significantly longer (7,451,801 years) because there is more time between clock edges for the flip-flop to resolve metastability.

The huge difference is due to the exponential term in the numerator. 

#Doubt We used 2 FFs. But analysed with only one. How does second FF help?
# References:


