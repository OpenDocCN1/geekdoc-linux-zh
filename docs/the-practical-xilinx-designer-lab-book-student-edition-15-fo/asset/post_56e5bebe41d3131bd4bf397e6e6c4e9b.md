
## Listing 7.6 VHDL code for the revised drink dispenser controller. (Cont’d.)

```vhdl
044- CONSTANT st_cents20: STD_LOGIC_VECTOR (6 DOWNTO 0) := "0010000";
045- CONSTANT st_cents25: STD_LOGIC_VECTOR (6 DOWNTO 0) := "0100000";
046- CONSTANT st_armed:  STD_LOGIC_VECTOR (6 DOWNTO 0) := "1000000";

048- BEGIN
049- cents0  <= curr_drink_state(0);  -- connect the components of
050- cents5  <= curr_drink_state(1);  -- the current state vector
051- cents10 <= curr_drink_state(2);  -- to the state outputs
052- cents15 <= curr_drink_state(3);
053- cents20 <= curr_drink_state(4);
054- cents25 <= curr_drink_state(5);
055- armed   <= curr_drink_state(6);

057- -- this process sets both the outputs and the next state
058- -- given the current state and inputs
059- PROCESS (curr_drink_state,nickel,dime,coin_ret,swill,krunk)
060- BEGIN
061- ret_nick    <= '0';  -- first set the default values
062- ret_dime    <= '0';  -- for the combinational outputs
063- disp_swill  <= '0';
064- disp_krunk  <= '0';
065- next_drink_state <= st_cents0; -- set default next state

067- IF curr_drink_state=st_cents0 THEN
068-   IF nickel='1'       THEN next_drink_state <= st_cents5;
069-   ELSIF dime='1'      THEN next_drink_state <= st_cents10;
070-   ELSE                      next_drink_state <= st_cents0;
071-   END IF;
072- ELSIF curr_drink_state=st_cents5 THEN
073-   IF nickel='1'       THEN next_drink_state <= st_cents10;
074-   ELSIF dime='1'      THEN next_drink_state <= st_cents15;
075-   ELSIF coin_ret='1'  THEN next_drink_state <= st_cents0; ret_nick<='1';
076-   ELSE                      next_drink_state <= st_cents5;
077-   END IF;
078- ELSIF curr_drink_state=st_cents10 THEN
079-   IF nickel='1'       THEN next_drink_state <= st_cents15;
080-   ELSIF dime='1'      THEN next_drink_state <= st_cents20;
081-   ELSIF coin_ret='1'  THEN next_drink_state <= st_cents0; ret_dime<='1';
082-   ELSE                      next_drink_state <= st_cents10;
083-   END IF;
084- ELSIF curr_drink_state=st_cents15 THEN
085-   IF nickel='1'       THEN next_drink_state <= st_cents20;
086-   ELSIF dime='1'      THEN next_drink_state <= st_cents25;
087-   ELSIF coin_ret='1' THEN next_drink_state<=st_cents5; ret_dime<='1';
088-   ELSE next_drink_state <= st_cents15;
089-   END IF;
090- ELSIF curr_drink_state=st_cents20 THEN
091-   IF nickel='1' THEN next_drink_state <= st_cents25;
092-   ELSIF dime='1' THEN next_drink_state<=st_cents25; ret_nick<='1';
093-   ELSIF coin_ret='1' THEN next_drink_state <=st_cents10; ret_dime<='1';
094-   ELSE next_drink_state <= st_cents20;
095-   END IF;
096- ELSIF curr_drink_state=st_cents25 THEN
097-   IF nickel='1' THEN next_drink_state <= st_cents25;
098-   ELSIF dime='1' THEN next_drink_state <= st_cents25;
099-   ELSIF coin_ret='1' THEN next_drink_state <= st_cents25;
100-   ELSIF swill='1' THEN next_drink_state <= st_cents25;
101-   ELSIF krunk='1' THEN next_drink_state <= st_cents25;
102-   ELSE next_drink_state <= st_armed;
103-   END IF;
104- ELSIF curr_drink_state=st_armed THEN
105-   IF nickel='1' THEN next_drink_state<=st_armed; ret_nick<='1';
106-   ELSIF dime='1' THEN next_drink_state<=st_armed; ret_dime<='1';
107-   ELSIF coin_ret='1' THEN next_drink_state<=st_cents15; ret_dime<='1';
108-   ELSIF swill='1' THEN next_drink_state<=st_cents0; disp_swill<='1';
109-   ELSIF krunk='1' THEN next_drink_state<=st_cents0; disp_krunk<='1';
110-   ELSE next_drink_state <= st_armed;
111-   END IF;
112- END IF;
113- END PROCESS;
114-
115- u0: IBUF PORT MAP(i=>c, O=>in_c);
116- u1: BUFG PORT MAP(i=>in_c, O=>buf_c);
117-
118- -- this process for the current state with the next state
119- PROCESS (buf_c,nickel,dime,coin_ret,swill,krunk)
120- BEGIN
121-   -- asynchronously reset the state when all inputs are high
122-   IF (nickel AND dime AND coin_ret AND swill AND krunk)='1' THEN
123-     curr_drink_state <= st_cents0;
124-   ELSIF (buf_c'event AND buf_c='1') THEN
125-     curr_drink_state <= next_drink_state;
126-   END IF;
127- END PROCESS;
128- END drink2_arch;
129-
```
