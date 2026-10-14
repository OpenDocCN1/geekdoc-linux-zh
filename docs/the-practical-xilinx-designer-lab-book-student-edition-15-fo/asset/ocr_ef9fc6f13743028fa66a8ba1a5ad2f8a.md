# Listing 8.4: VHDL version of a 4-bit wide synchronous memory built from 4 register modules. (Contd.)

```
049- w <= "1110" WHEN (a="00") AND (web='0') ELSE
050-       "1011" WHEN (a="01") AND (web='0') ELSE
051-       "1011" WHEN (a="10") AND (web='0') ELSE
052-       "0111" WHEN (a="11") AND (web='0') ELSE
053-       "1111";
054- w0 <= w(0);
055- w1 <= w(1);
056- w2 <= w(2);
057- w3 <= w(3);
058-
059- -- buffer the input clock
060- u4: IBUF PORT MAP(I=>clk, O=>in_clk);
061- u5: BUFG PORT MAP(I=>in_clk, O=>buf_clk);
062-
063- -- this process loads the selected reg on the rising clock edge
064- PROCESS (buf_clk,w0,w1,w2,w3,inp)
065- BEGIN
066- IF(buf_clk'EVENT AND buf_clk='1') THEN
067-   IF w0='0' THEN
068-     rga <= inbus;
069-   END IF;
070-   IF w1='0' THEN
071-     rgb <= inbus;
072-   END IF;
073-   IF w2='0' THEN
074-     rgc <= inbus;
075-   END IF;
076-   IF w3='0' THEN
077-     rgd <= inbus;
078-   END IF;
079- END IF;
080- END PROCESS;
081-
082- outp <= rga WHEN a="00" ELSE    -- select one of the four
083-         rgb WHEN a="01" ELSE    -- registers and output
084-         rgc WHEN a="10" ELSE    -- its value on the output bus
085-         rgd;
086-
087- -- display the output value on the LED display
088- u6: leddcd PORT MAP (d=>outp,s=>s);
089-
090- END mem2_arch;
091-
```