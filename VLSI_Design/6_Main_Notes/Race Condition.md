Race around condition is a phenomenon in digital electronics, particularly in sequential circuits such as flip-flops, where the output oscillates between 0 and 1 within the same clock cycle due to a feedback loop. This condition is prevalent in level-triggered (as opposed to edge-triggered) devices.

- **SR Latch:** An SR (Set-Reset) latch can also experience a race condition when both S (Set) and R (Reset) inputs are activated simultaneously. When both inputs are high, the state of the latch becomes unpredictable because it rapidly toggles between set and reset states.

### Avoiding Race Around Condition in SR Latch

1. **Edge-Triggered Flip-Flops:** Instead of using level-triggered latches, use edge-triggered flip-flops. These devices change their state only on the edge (rising or falling) of the clock pulse, thus avoiding continuous toggling within the clock cycle.
    
2. **Master-Slave Configuration:** Use a master-slave configuration to create a more stable SR latch. This configuration involves two latches in series:
    
    - **Master Latch:** The first latch (master) captures the input state on the clock's leading edge (e.g., rising edge).
    - **Slave Latch:** The second latch (slave) captures the output of the master latch on the clock's trailing edge (e.g., falling edge).
    - This setup ensures that the output changes only once per clock cycle, thus avoiding the race condition.
3. **Clock Gating:** Introduce clock gating to control when the latch can change states. By ensuring that the clock signal only reaches the latch during appropriate times, the chances of race conditions can be reduced.
    
4. **Proper Timing Analysis:** Perform a thorough timing analysis to ensure that the propagation delays and setup times are met. Ensure that the clock pulse width is adequate to prevent the latch from toggling multiple times within a single pulse.
    
5. **Debouncing Circuits:** In mechanical switch applications, use debouncing circuits to eliminate noise and ensure that the latch changes state only once per activation.