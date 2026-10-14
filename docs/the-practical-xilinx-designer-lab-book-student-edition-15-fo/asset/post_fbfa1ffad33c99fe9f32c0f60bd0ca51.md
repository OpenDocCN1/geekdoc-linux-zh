
## Listing 7.2 VHDL code for a 3-state up/down counter.

```
001- -- 3-state up/down counter
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY cnt3 IS
007- PORT
008- (
009- c: IN STD_LOGIC; -- clock input
010- reset: IN STD_LOGIC; -- active-high reset
011- up: IN STD_LOGIC; -- up/down control input
012- outp0, outp1: OUT STD_LOGIC;-- outputs
013- q0,q1: OUT STD_LOGIC -- state outputs
014- );
015- END cnt3;
016-
017- ARCHITECTURE cnt3_arch OF cnt3 IS
018- COMPONENT IBUF PORT(I: IN STD_LOGIC;
019- O: OUT STD_LOGIC); END COMPONENT;
020- COMPONENT BUFG PORT(I: IN STD_LOGIC;
021- O: OUT STD_LOGIC); END COMPONENT;
022- SIGNAL in_c, buf_c: STD_LOGIC;
023- SIGNAL curr_state, next_state: STD_LOGIC_VECTOR(1 DOWNTO 0);
024- BEGIN
025-
026- u0: IBUF PORT MAP(I=>c, O=>in_c);-- connect clock to
027- u1: BUFG PORT MAP(I=>in_c, O=>buf_c);-- clock buffer
028-
029- outp0 <= curr_state(0); -- connect outputs to current state
030- outp1 <= curr_state(1)
031- q0 <= curr_state(0); -- connect state outputs to current state
032- q1 <= curr_state(1);
033-
034- PROCESS(reset,up,curr_state)-- compute next state from current
035- BEGIN
036- IF reset='1' THEN
037- next_state <= "00";
038- ELSIF curr_state="00" THEN
039- IF up='1' THEN next_state <= "01";
040- ELSE next_state <= "10";
041- END IF;
042- ELSIF curr_state="01" THEN
043- IF up='1' THEN next_state <= "10";
044- ELSE next_state <= "00";
045- END IF;
046- ELSIF curr_state="10" THEN
047- IF up='1' THEN next_state <= "00";
048- ELSE next_state <= "01";
049- END IF;
050- ELSE
051- next_state <= "00";
052- END IF;
053- END PROCESS;
054-
055- PROCESS(buf_c,next_state)-- update the current state vector
056- BEGIN
057- IF (buf_c'event AND buf_c='1') THEN
058- curr_state <= next_state;
059- END IF;
060- END PROCESS;
061-
062- END cnt3_arch;
```

![](img/5124daf79d2807d81e49f49c22f1f8c1_230_0.png)

## Figure 7.10 Simulated waveforms for the 3-state up/down counter.

After downloading your circuit to the XS40 or XS95 Board, you can use the following command sequences to move the state machine between its various states. Each set of commands activates a particular input and then sends a rising clock edge to the state machine. You can read off the current state by observing the S0 and S1 LED segments.

| Action | XSPORT Command Sequence |
|---|---|
| Reset the counter | XSPORT 010<br>XSPORT 011<br>XSPORT 000 |
| Increment by one | XSPORT 100<br>XSPORT 101<br>XSPORT 000 |
| Decrement by one | XSPORT 000<br>XSPORT 001<br>XSPORT 000 |

## A Drink Dispenser Controller

This example will show you how to design a state machine to solve an actual problem: dispensing soft-drinks.

You have been contracted to design the logic for a soft-drink machine that dispenses two brands of cola: Swill and Krunk. The dispenser should accept nickels and dimes and should allow the buyer to select one of the soft-drinks after he or she has put in 25¢. That is the extent of the requirements.

The first step is to get some idea of the inputs and outputs of the logic circuitry. From the requirements, you know that the logic must receive inputs that indicate whether the buyer has put in a nickel or a dime. You also know that there have to be two inputs for indicating whether the buyer wants to enjoy a can of refreshing Swill or Krunk. Finally, what if the buyer changes his or her mind in the middle of a transaction? There should be an input to return the buyer’s money.

What about the outputs from the logic? There should be outputs to control the individual dispensers for Swill and Krunk so that a can is dispensed whenever a high logic level is present. There should also be two outputs to control the return of change: one that causes a nickel to be dropped into the change return slot, and another that drops a dime.

OK, you seem to have an initial idea of what the I/O looks like. The next step is to determine the states of your state machine (i.e., what your logic has to remember). The obvious thing to remember is how much money the buyer has put into the dispenser. This machine dispenses a soft-drink after it receives 25¢ in either nickels or dimes, so the possible states for the machine are that it has received 0¢, 5¢, 10¢, 15¢, 20¢, or 25¢. That is a total of 6 states. At this point, the drink dispenser controller looks like Figure 7.11.
