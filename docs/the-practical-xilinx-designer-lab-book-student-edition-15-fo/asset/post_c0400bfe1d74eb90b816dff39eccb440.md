
![](img/5124daf79d2807d81e49f49c22f1f8c1_218_0.png)

## Generic Design Flow

## State Machine Design Flow

## Figure 7.5 The logic design flow modified for state machine designs.

in which the toner-transfer roller is heated may not need to be expanded further because it just applies current to a heater coil until a time-out occurs.

After you determine what the states are, you have to assign a distinct binary pattern to each state. A set of D flip-flops in the state machine stores these patterns. By examining the contents of the DFFs, we can determine what state the circuit is in. For a counter, the assignment of binary patterns to states is usually simple: Just use the binary value of the counter as the state. For other designs, the binary patterns can be more arbitrary. For the laser printer example, you might use the following state assignment:

| State | Binary Pattern |
| --- | --- |
| Initialization | 000 |
| Diagnostics | 001 |
| Toner-transfer warming | 010 |
| Idle | 011 |
| Data transfer to buffer | 100 |
| Paper feed activation | 101 |
| Write electrostatic pattern | 110 |

If you have N total states, you will need at least n flip-flops such that 2^n ≥ N. For the printer example, N = 7 so n ≥ 3. If we choose n = 3, then we are using a minimal encoding for the states because it uses the smallest possible number of flip-flops.

Once you have the states defined, you have to determine how your machine will move from state to state as the inputs change. You also need to specify what the values on the outputs will be at each state. You can do this with "bubble diagrams," as shown in Figure 7.6, but that soon becomes unmanageable when the number of states and possible transitions gets large.

As an alternative, you can use state transition tables like the one in Table 7.1. State transition tables list all the possible states in the leftmost column and all possible combinations of inputs across the top. The entry at row i and column j within the table lists the next state and the output that will be generated given that the current state is i and the current input pattern is j. For example, when the counter is in state 1 and the reset is not active (reset = 0) and the counter is incrementing (up = 1), then the current output is 01 and the next state is state 2.

The advantage of the state transition table is that it forces you to account for the actions of your state machine for each combination of current state and input pattern. Empty locations in the table immediately make it apparent that there is something you have forgotten to specify. The problem is that the table gets large, especially when the number of inputs increases. Still, it's a reasonable method for the problems we will handle here.

With a completed state transition table in hand, we can proceed to make a truth table that describes how the inputs and current state affect the outputs and next state. The truth table will have a row for each entry in the state transition table. The inputs for each row of the truth table are the current state and

input combination from the row and column containing the state transition table entry. The outputs for each row of the truth table are just the next state and output from the state transition table entry.

![](img/5124daf79d2807d81e49f49c22f1f8c1_220_0.png)

## Figure 7.6 Bubble diagram for a three-state counter with a reset and up/down inputs.

## Table 7.1 State transition table for the 3-state counter with reset and up/down inputs.

| | Inputs | | | | |
|---|---|---|---|---|---|
| Current State | reset = 0 up = 0 | reset = 0 up = 1 | reset = 1 up = 0 | reset = 1 up = 1 |
| state 0 | state2, output = 00 | state1, output = 00 | state0, output = 00 | state0, output = 00 |
| state 1 | state0, output = 01 | state2, output = 01 | state0, output = 01 | state0, output = 01 |
| state 2 | state1, output = 10 | state0, output = 10 | state0, output = 10 | state0, output = 10 |

The complete truth table in Table 7.2 was generated from the state transition table in Table 7.1. The state can be stored using two flip-flops, q1 and q2, and we have used an obvious state assignment (state 0 is 00, state 1 is 01, and state 2 is 10). As an example, on row 6 the machine is in state 1 (q1 = 0, q0 = 1), the
