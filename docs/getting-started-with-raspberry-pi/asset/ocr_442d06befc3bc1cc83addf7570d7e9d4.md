![](bbox=[0.15, 0.05, 0.78, 0.58])

The *Point-to-Point Protocol* (PPP) allows networking protocols such as TCP/IP to run over a serial link. In the context of Figure 9.5, PPP gets TCP/IP applications running over GPRS and GSM dialup. The PPP daemon, *pppd*, attaches over virtual serial ports emulated by *serial_cs*. The PPP kernel modules—*ppp_generic*, *ppp_async*, and *slhc*—have to be loaded for pppd to work. Invoke pppd as follows:

```
```
bash> pppd ttySx call connection-script
```
```

where *connection-script* is a file containing command sequences that pppd exchanges with the service provider to establish a link. The connection script depends on the particular card that is being used. A GPRS card would need a context string to be sent as part of the connection script, whereas a GSM card might need an exchange of passwords. An example connection script is described in the section “GPRS” in Chapter 16.