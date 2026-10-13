or more spaces or tabs. It’s a good idea to use white space in such a manner that the items line up in two columns.

> **Note:** Enclose all strings that contain spaces in quotes to ensure the correct parsing of what is an expected string and what is a string to be sent to the modem. For example, to send the string `AT &S1 &C1` to the modem, it must be enclosed in quotes.

The expected string is placed in the left column and the string to be sent is placed in the right column. The first line of the preceding chat script is an exception. The string ABORT is not expected. It is used to identify cases in which the script is to be aborted. In this case, if the modem returns the string BUSY, the chat script aborts. This allows the script to terminate without waiting indefinitely for a string that might never come.

Line two of the script just sends a dial string to the modem without waiting because there is no expected string. The third line causes the script to pause until the string CONNECT is received from the modem, and then continues with any remaining portion of the script; in this case, pppd completes the PPP connection. A more involved chat script might look similar to the following:

```
ABORT       BUSY
ABORT       "NO CARRIER"
ABORT       "NO DIALTONE"
ABORT       VOICE
ABORT       "NO ANSWER"
""          ATZ
OK          "AT S0=0"
OK          ATDT5551234
CONNECT     ""
```

See the online man page for chat for further details and options.

# CONFIGURING THE PPP OPTIONS FILE

The options for pppd are stored in the `/etc/ppp/options` file. When pppd runs, it looks in this file for the runtime parameters, including the method by which it interacts with the modem. The options that are used most frequently with pppd are listed in Table 24.3.

**Table 24.3 — List of Frequently Used Options with PPPD**

| Option | Description |
|---|---|
| `tty device` | Specifies which tty device the modem is connected to. The full pathname to the device that is used is typically specified. For example, the first COM port is `/dev/ttyS0`. |
| `modem speed` | Specifies the baud rate that is to be used. |
| `asyncmap <map>` | Sets the asynchronous character map. This map specifies which control characters cannot be successfully received over the serial line. |
| `auth` | Requires the peer to authenticate itself before allowing network packets to be sent or received. A noauth performs the opposite function. |
| `call <name>` | This parameter reads options from the file `/etc/ppp/peers/<name>`. |