layer of combinational logic feeding flip-flops in another CLB and ignoring routing-dependent wiring delays, the inequality for the XC4005XL-3 FPGA is

1.9 ns + 3.2 ns + 1.2 ns ≤ T_cycle

So our clock frequency cannot exceed 1/T_cycle = 159 MHz. That seems pretty fast, but wiring delay can easily add another 5 to 10 ns, which would bring the speed below 100 MHz.

We also have to make sure the inputs to the flip-flops hang around after the clock edge for a duration longer than the minimum hold time. This requirement is expressed by this inequality:

T_co + T_wd1 + T_pd + T_wd2 ≥ T_h

The hold-time requirement is easy to satisfy since T_h is 0 ns for both the XC95108 and the XC4005XL devices.

Our timing analysis is valid but it is based on the assumption that all the flip-flops get the clock edge at exactly the same time. But the wiring to the clock inputs of different flip-flops can introduce different delays, so all the clock edges will not stay lined up (Figure 7.8). The difference in time between the clock edges is termed clock skew, and we will denote it by T_skew. Now we can modify our inequalities to account for the clock skew:

T_co + T_wd1 + T_pd + T_wd2 + T_su + T_skew ≤ T_cycle
T_co + T_wd1 + T_pd + T_wd2 - T_skew ≥ T_h

In general, we cannot be sure if the clock skew will be positive or negative for a given pair of flip-flops. But we assume clock skew will always going to make

![](bbox=[0.25, 0.82, 0.85, 0.95])

# Figure 7.8 Clock skew.