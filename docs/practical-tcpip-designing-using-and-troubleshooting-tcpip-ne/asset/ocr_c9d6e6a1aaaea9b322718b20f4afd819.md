# ## 3. Terminating the connection

When one end of the connection (Bob, in this case) is finished and has no more data to transmit, it sends a packet with the FIN (“finish”) flag set, shown as “F” in `tcpdump`. Alice ACKs this. Now Alice has to tell Bob that *she* has no more data to transmit to him, so she has to send a FIN packet too. Only when Bob ACKs this is the connection closed completely:

```
```
Bob.telnet > Alice.1067: FP 673:683(10) ack 135 win 16060$
Alice.1067 > Bob.telnet: . ack 684 win 16060 <nop,nop,tim$
Alice.1067 > Bob.telnet: F 135:135(0) ack 684 win 16060 $
Bob.telnet > Alice.1067: . ack 136 win 16060 <nop,nop,tim$
```
```

So it takes four packets to terminate the connection, but only three to establish it. The typical packet flow for a whole session, where the server terminates the connection, is shown in Figure 10.12(a), and Figure 10.12(b) shows the flow where the client terminates it.

![](bbox=[0.07, 0.33, 0.85, 0.65])

![](bbox=[0.07, 0.67, 0.85, 0.98])