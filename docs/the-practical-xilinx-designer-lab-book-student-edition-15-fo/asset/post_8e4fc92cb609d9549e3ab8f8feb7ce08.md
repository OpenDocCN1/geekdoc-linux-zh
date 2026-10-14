
### Listing 7.5 ABEL code for the revised drink dispenser controller.

```
043- STATE_DIAGRAM [ST_ARMED, ST_CENTS25, ST_CENTS20, ST_CENTS15,
044-               ST_CENTS10, ST_CENTS5, ST_CENTS0]
046-
STATE ST_CENTS0:
047- IF NICKEL THEN ST_CENTS5
048- ELSE IF DIME THEN ST_CENTS10
049- ELSE ST_CENTS0;
051-
STATE ST_CENTS5:
052- IF NICKEL THEN ST_CENTS10
053- ELSE IF DIME THEN ST_CENTS15
054- ELSE IF COIN_RET THEN ST_CENTS0 WITH RET_NICK=1
055- ELSE ST_CENTS5;
057-
STATE ST_CENTS10:
058- IF NICKEL THEN ST_CENTS15
059- ELSE IF DIME THEN ST_CENTS20
060- ELSE IF COIN_RET THEN ST_CENTS0 WITH RET_DIME=1
061- ELSE ST_CENTS10;
063-
STATE ST_CENTS15:
064- IF NICKEL THEN ST_CENTS20
065- ELSE IF DIME THEN ST_CENTS25
066- ELSE IF COIN_RET THEN ST_CENTS5 WITH RET_DIME=1
067- ELSE ST_CENTS15;
069-
STATE ST_CENTS20:
070- IF NICKEL THEN ST_CENTS25
071- ELSE IF DIME THEN ST_CENTS25 WITH RET_NICK=1
072- ELSE IF COIN_RET THEN ST_CENTS10 WITH RET_DIME=1
073- ELSE ST_CENTS20;
075-
STATE ST_CENTS25:
076- IF NICKEL THEN ST_CENTS25
077- ELSE IF DIME THEN ST_CENTS25
078- ELSE IF COIN_RET THEN ST_CENTS25
079- ELSE IF SWILL THEN ST_CENTS25
080- ELSE IF KRUNK THEN ST_CENTS25
081- ELSE ST_ARMED;
083-
STATE ST_ARMED:
084- IF NICKEL THEN ST_ARMED WITH RET_NICK=1
085- ELSE IF DIME THEN ST_ARMED WITH RET_DIME=1
086- ELSE IF COIN_RET THEN ST_CENTS15 WITH RET_DIME=1
087- ELSE IF SWILL THEN ST_CENTS0 WITH DISP_SWILL=1
088- ELSE IF KRUNK THEN ST_CENTS0 WITH DISP_KRUNK=1
089- ELSE ST_ARMED;
090-
091- END DRINK2
```

54. So the drink dispenser moves into the 25¢ state. The net result is that if a dime is inserted when the dispenser has already received 20¢, then the dispenser will return a nickel and hold a total of 25¢. This replicates the behavior of our previous state machine described by Listing 7.4.

The simulated waveforms for the revised ABEL or VHDL drink dispenser control circuit are shown in Figure 7.14. Notice that our "problem pulse" on the RET_DIME output is no longer present during the 36–40 ns period.

The revised drink dispenser controller circuit can be downloaded and tested in exactly the same manner as the controller from the previous section.

We mentioned earlier that the behavior of our revised controller almost matches the behavior described in Table 7.3. Remember when we created Table 7.3, we specified that none of the inputs could be active simultaneously. For example, if a customer pressed both the Swill and Krunk buttons at the same time, the result would be undefined because there is no listing in the table for such an occurrence. (With 5 inputs, the table would need 32 columns to cover every possibility. I am not going to try writing that out!)

But the circuit as described in Listings 7.5 or 7.6 does handle the cases where multiple inputs are active simultaneously. For example, the IF clause on line 47 of Listing 7.5 (or line 68 of Listing 7.6) is active if NICKEL=1 regardless of the state of the other inputs. So the same clause would also be active if NICKEL=1 and DIME=1. Interpreted in this way, we can see that all 32 possible input combinations are covered for all 7 states in the revised drink dispenser controller. There is no longer any unspecified behavior. Of course, this does not mean that the specified behavior is what we want! To be sure of that, we would have to examine each response to each combination of inputs in each state and ask if that is the most desireable behavior. But that is a job for another day.

## Using the State Editor

At this point we have described state machines using ABEL and VHDL. These are text-based design methods. For those who want a more graphical approach, the Foundation Series software includes a state editor that lets you design a

### Listing 7.6 VHDL code for the revised drink dispenser controller.

```
001- -- Drink Dispenser Controller
002-
003- LIBRARY IEEE;
004- USE IEEE.std_logic_1164.ALL;
005-
006- ENTITY drink2 IS
007- PORT
008- (
009-     c: IN STD_LOGIC;                 -- clock
010-     nickel: IN STD_LOGIC;            -- nickel is inserted
011-     dime: IN STD_LOGIC;              -- dime is inserted
012-     coin_ret: IN STD_LOGIC;          -- coin-return is pressed
013-     swill: IN STD_LOGIC;             -- swill is selected
014-     krunk: IN STD_LOGIC;             -- krunk is selected
015-     ret_nick: OUT STD_LOGIC;         -- nickel is returned
016-     ret_dime: OUT STD_LOGIC;         -- dime is returned
017-     disp_swill: OUT STD_LOGIC;       -- swill is dispensed
018-     disp_krunk: OUT STD_LOGIC;       -- krunk is dispensed
019-     cents0: OUT STD_LOGIC;           -- no money has been inserted
020-     cents5: OUT STD_LOGIC;           -- 5 cents has been inserted
021-     cents10: OUT STD_LOGIC;          -- 10 cents has been inserted
022-     cents15: OUT STD_LOGIC;          -- 15 cents has been inserted
023-     cents20: OUT STD_LOGIC;          -- 20 cents has been inserted
024-     cents25: OUT STD_LOGIC;          -- 25 cents has been inserted
025-     armed: OUT STD_LOGIC
026- );
027- END drink2;
028-
029- ARCHITECTURE drink2_arch OF drink2 IS
030-
031- COMPONENT IBUF PORT(I: IN STD_LOGIC; O: OUT STD_LOGIC); END COMPONENT;
032- COMPONENT BUFG PORT(I: IN STD_LOGIC; O: OUT STD_LOGIC); END COMPONENT;
033- SIGNAL in_c: STD_LOGIC; -- input-buffered clock
034- SIGNAL buf_c: STD_LOGIC; -- global-buffered clock
035-
036- -- declare current and next state vectors for drink machine state
037- SIGNAL curr_drink_state: STD_LOGIC_VECTOR (6 DOWNTO 0);
038- SIGNAL next_drink_state: STD_LOGIC_VECTOR (6 DOWNTO 0);
039- -- the one-hot state definitions for the state machine
040- CONSTANT st_cents0: STD_LOGIC_VECTOR (6 DOWNTO 0) := "0000001";
041- CONSTANT st_cents5: STD_LOGIC_VECTOR (6 DOWNTO 0) := "0000010";
042- CONSTANT st_cents10: STD_LOGIC_VECTOR (6 DOWNTO 0) := "0000100";
043- CONSTANT st_cents15: STD_LOGIC_VECTOR (6 DOWNTO 0) := "0001000";
```
