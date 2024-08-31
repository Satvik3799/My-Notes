25-08-2024 17:58

Status:

Tag:


# Architectural Synthesis

Done in two stages.
1. Placing the operation in time and in space - 
	Determining their time interval of execution and which resource they will use and when.
		![[Pasted image 20240825180137.png]]
2. Determining detailed interconnection - 
		Relate the data-path and logic-level specifications of the control unit.



# Temporal Domain: (Scheduling)

Scheduling is the task of determining the start timing, subject to previous constraints specified by the sequencing graph. For ex. Multiplication in step 2 must only start after the multiplication in step 1 has finished. 

![[Pasted image 20240825175153.png]]
![[Pasted image 20240825183854.png]]



After it is decided that when an operation should take place, we must decide which resource will perform that operation. That is done by Binding (Spatial domain)


# Spatial Domain: Binding

- Necessary condition to produce a valid circuit: 
	Operations that share resources, should not execute concurrently.
![[Pasted image 20240825184735.png]]
![[Pasted image 20240825184750.png]]



# Area/Performance Estimation

Accurate estimation is very difficult task.

- Schedule provides latency.
- Binding provides information about area.

# ASAP Scheduling

- We want to schedule a node as soon as possible.
- Based on dependency between operations, decide when an operation can be performed as early as possible. For ex., Node 3 cannot start computing unless Node 1 and Node 2 has given an output.
![[Pasted image 20240825185208.png]]
![[Pasted image 20240825185250.png]]
# References:

