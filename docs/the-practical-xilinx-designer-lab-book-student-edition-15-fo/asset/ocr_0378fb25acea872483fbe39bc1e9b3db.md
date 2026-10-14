```
NET CLK      LOC=P46;   # B0 argument of XSPORT
NET RESET    LOC=P47;   # B1 argument of XSPORT
NET UP       LOC=P48;   # B2 argument of XSPORT
NET OUTPUT0  LOC=P21;   # S0 LED segment
NET OUTPUT1  LOC=P23;   # S1 LED segment
```

After downloading your circuit to the XS40 or XS95 Board, you can use the following command sequences to move the state machine between its various states. Each set of commands activates a particular input and then sends a rising clock edge to the state machine. You can see the output for each state by observing the S0 and S1 LED segments.

| Action | XSPORT Command Sequence |
|---|---|
| Reset the counter | XSPORT 010
XSPORT 011
XSPORT 000 |
| Increment by one | XSPORT 100
XSPORT 101
XSPORT 000 |
| Decrement by one | XSPORT 000
XSPORT 001
XSPORT 000 |

# Projects

+   1. Design a circuit that counts in the following sequence:
+   7,6,5,4,3,4,5,6,7,6,5,4,3,4,5,6,7,...
+   The circuit should change states on the falling edge of the clock. The circuit should have a reset input that forces it into the 3 state on the next falling clock edge. The output of the circuit should drive an LED digit and display the appropriate digit as it operates.

+   2. Design a 4-bit counter that will count up when a control signal is at logic 0, and will count down when the control signal is logic 1. The output of the circuit should drive an LED digit and display the appropriate digit as it operates.

+   3. Add a new 20¢ drink selection to the DRINK2.ABL or DRINK2.VHD design.

+   4. Modify DRINK2.ABL or DRINK2.VHD so that multiple simultaneous button presses are ignored.