
With your new knowledge of the ABEL state machine syntax, you should be able to interpret each line of Listing 7.5 and relate it back to the original state transition table. In fact, the ABEL compiler which you use to synthesize netlists does the same thing. The compiler parses the STATE_DIAGRAM statements and constructs its own state transition table. Then the compiler can derive the circuitry for generating the next state and the outputs just as you did in the previous sections. So the software tools are not doing anything magical.

We can also re-do the VHDL version of the drink dispenser state machine as shown in Listing 7.6. Like the 3-state counter VHDL example (Listing 7.2), this code uses two processes: one for computing the outputs and the next state based upon the values of the current state and inputs (lines 59–113), and another process which just updates the current state with the new next state value (lines 119–127). For this reason, we declare two arrays for holding the current and next state on lines 37 and 38, respectively.

The new armed output is added to the interface description on line 25, and the current and next state arrays and state definitions are expanded to handle this extra bit on lines 37 through 46. The state outputs for this design are attached to the elements of the current state array on lines 49 through 55.

The first process starts by assigning a low logic level to all the combinational outputs of the state machine (lines 61–64). This ensures that these outputs are set to some value if none of the following conditional statements does so. If we did not perform this initialization step, then these outputs would become implied latches. The next state array is also initialized to the reset state (with 0c) on line 65. This will cause the state machine to restart if it ever gets into an illegal state.

A large IF...THEN...ELSE statement follows on lines 67–112 that uses the current state and inputs to compute the next state and the outputs. As an example of how the VHDL code works, consider the case when the current state is 20c. Then the cents20 flip-flop should be on so the curr_drink_state array should be 0010000. This matches the st_cents20 constant so the statement on line 90 is executed. This activates the nested IF...THEN...ELSE statement on lines 91–95. If a dime is inserted, then execution falls through to line 92. The statement on line 92 assigns a logic 1 to the ret_nick output. So a nickel will be returned to the customer. At the same time, the next_drink_state array is loaded with st_cents25. The st_cents25 constant is 0100000, so the next_drink_state(5) element is set and the other elements are cleared.

Continuing the example, the second process transfers the next_drink_state array into the curr_drink_state array when a rising edge occur on the clock input. This loads curr_drink_state with st_cents25 which is 0100000. This sets the curr_drink_state(5) element and resets all the others. The curr_drink_state(5) element is connected to the cents25 state output on line

### Listing 7.5 ABEL code for the revised drink dispenser controller.

```
001- MODULE DRINK2;
002- TITLE 'drink dispenser controller (2nd version)'
003-
004- DECLARATIONS
005- C PIN;                      *clock input
006- NICKEL PIN;                 *nickel inserted input
007- DIME PIN;                   *dime inserted input
008- COIN_RET PIN;               *coin-return input
009- SWILL PIN;                  *Swill selection
010- KRUNK PIN;                  *Krunk selection
011- RET_NICK PIN ISTYPE 'COM';  *return nickel output
012- RET_DIME PIN ISTYPE 'COM';  *return dime output
013- DISP_SWILL PIN ISTYPE 'COM'; *dispense swill output
014- DISP_KRUNK PIN ISTYPE 'COM'; *dispense krunk output
015- CENTS0 PIN ISTYPE 'REG';    *DFF for 0-cents state
016- CENTS5 PIN ISTYPE 'REG';    *DFF for 5-cents state
017- CENTS10 PIN ISTYPE 'REG';   *DFF for 10-cents state
018- CENTS15 PIN ISTYPE 'REG';   *DFF for 15-cents state
019- CENTS20 PIN ISTYPE 'REG';   *DFF for 20-cents state
020- CENTS25 PIN ISTYPE 'REG';   *DFF for 25-cents state
021- ARMED PIN ISTYPE 'REG';     *DFF for armed state
022- RESET = NICKEL & DIME & COIN_RET & SWILL & KRUNK; *reset trigger
023-
024- *now make some state assignments
025-
026- ARMED CENTS25 CENTS20 CENTS15 CENTS10 CENTS5 CENTS0
027- ST_CENTS0 = [0, 0, 0, 0, 0, 0, 1];
028- ST_CENTS5 = [0, 0, 0, 0, 0, 1, 0];
029- ST_CENTS10 = [0, 0, 0, 0, 1, 0, 0];
030- ST_CENTS15 = [0, 0, 0, 1, 0, 0, 0];
031- ST_CENTS20 = [0, 0, 1, 0, 0, 0, 0];
032- ST_CENTS25 = [0, 1, 0, 0, 0, 0, 0];
033- ST_ARMED = [1, 0, 0, 0, 0, 0, 0];
034-
035- EQUATIONS
036-
037- *clock controller state DFFs
038- [CENTS0,CENTS5,CENTS10,CENTS15,CENTS20,CENTS25,ARMED].CLK = C;
039- *next two statements asynchronously reset controller
040- *to the cents0 state (0000001)
041- CENTS0.ASET = RESET;
042- [CENTS5,CENTS10,CENTS15,CENTS20,CENTS25,ARMED].ACLR = RESET;
```
