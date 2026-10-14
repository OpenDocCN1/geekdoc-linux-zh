![](bbox=[0.3, 0.12, 0.94, 0.38])

# Figure 4.18 Waveforms from the simulation of the 8-bit adder.

```
NET A<1>      LOC=P48;
NET A<2>      LOC=P50;
NET B<0>      LOC=P51;
NET B<1>      LOC=P52;
NET B<2>      LOC=P81;
NET SUM<0>    LOC=P21; # LED segment S0
NET SUM<1>    LOC=P23; # LED segment S1
NET SUM<2>    LOC=P19; # LED segment S2
# the following constraints assign unused ADDB terminals to out-of-the-way pins
NET COUT      LOC=P7;
NET A<3>      LOC=P75;
NET A<4>      LOC=P79;
NET A<5>      LOC=P82;
NET A<6>      LOC=P84;
NET A<7>      LOC=P1;
NET B<3>      LOC=P61;
NET B<4>      LOC=P55;
NET B<5>      LOC=P57;
NET B<6>      LOC=P58;
NET B<7>      LOC=P83;
NET SUM<3>    LOC=P2;
NET SUM<4>    LOC=P53;
NET SUM<5>    LOC=P56;
NET SUM<6>    LOC=P54;
NET SUM<7>    LOC=P6;
```

The PC's parallel port is limited to driving 8 of the 8-bit adder inputs. I allocated one bit to the carry input, and 3 bits to each of the A and B buses. The remainder of the A and B input bits were assigned to pins on the XS95 Board