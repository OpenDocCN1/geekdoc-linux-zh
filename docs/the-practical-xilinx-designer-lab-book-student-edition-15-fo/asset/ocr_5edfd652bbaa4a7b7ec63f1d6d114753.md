# Listing 7.6 VHDL code for the revised drink dispenser controller. (Cont'd.)

```
087- ELSIF coin_ret='1' THEN next_drink_state<=st_cents5; ret_dime<='1';
088- ELSE next_drink_state <= st_cents15;
089- END IF;
090- ELSIF curr_drink_state=st_cents20 THEN
091- IF nickel='1' THEN next_drink_state <= st_cents25;
092- ELSIF dime='1' THEN next_drink_state<=st_cents25; ret_nick<='1';
093- ELSIF coin_ret='1' THEN next_drink_state <=st_cents10; ret_dime<='1';
094- ELSE next_drink_state <= st_cents20;
095- END IF;
096- ELSIF curr_drink_state=st_cents25 THEN
097- IF nickel='1' THEN next_drink_state <= st_cents25;
098- ELSIF dime='1' THEN next_drink_state <= st_cents25;
099- ELSIF coin_ret='1' THEN next_drink_state <= st_cents25;
100- ELSIF swill='1' THEN next_drink_state <= st_cents25;
101- ELSIF krunk='1' THEN next_drink_state <= st_cents25;
102- ELSE next_drink_state <= st_armed;
103- END IF;
104- ELSIF curr_drink_state=st_armed THEN
105- IF nickel='1' THEN next_drink_state<=st_armed; ret_nick<='1';
106- ELSIF dime='1' THEN next_drink_state<=st_armed; ret_dime<='1';
107- ELSIF coin_ret='1' THEN next_drink_state<=st_cents15; ret_dime<='1';
108- ELSIF swill='1' THEN next_drink_state<=st_cents0; disp_swill<='1';
109- ELSIF krunk='1' THEN next_drink_state<=st_cents0; disp_krunk<='1';
110- ELSE next_drink_state <= st_armed;
111- END IF;
112- END IF;
113- END PROCESS;
114-
115- u0: IBUF PORT MAP(i=>c, O=>in_c);
116- u1: BUFG PORT MAP(i=>in_c, O=>buf_c);
117-
118- -- this process for the current state with the next state
119- PROCESS (buf_c,nickel,dime,coin_ret,swill,krunk)
120- BEGIN
121- -- asynchronously reset the state when all inputs are high
122- IF (nickel AND dime AND coin_ret AND swill AND krunk)='1' THEN
123- curr_drink_state <= st_cents0;
124- ELSIF (buf_c'event AND buf_c='1') THEN
125- curr_drink_state <= next_drink_state;
126- END IF;
127- END PROCESS;
128- END drink2_arch;
129-
```