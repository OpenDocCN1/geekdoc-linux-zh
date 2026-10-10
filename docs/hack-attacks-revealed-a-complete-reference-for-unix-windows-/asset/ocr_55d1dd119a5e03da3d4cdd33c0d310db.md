![](bbox=[0.31, 0.06, 0.77, 0.21])

![](bbox=[0.11, 0.23, 0.64, 0.43])

![](bbox=[0.64, 0.23, 0.85, 0.43])

**Figure 9.2** Visual Basic forms for Crash.bas.

# Pipeline Password Congestion

**Synopsis:** Challenging remote telnet sessions can congest the Ascend router session limit and cause the system to refuse further attempts.

**Hack State:** Severe congestion.

**Vulnerabilities:** Ascend Pipeline products.

**Breach:** Continuous remote telnet authentication attempts can max out system session limits, causing the router to refuse legitimate sessions.

# MAX Attack

**Synopsis:** Attackers have been able to remotely reboot Ascend MAX units by telnetting to Port 150 while sending nonzero-length TCP Offset packets with *TCPOffset.c*, shown later.

**Hack State:** System restart.

**Vulnerabilities:** Ascend MAX 5x products.

# TCP Offset Harassment

**Synopsis:** A hacker can crash an Ascend terminal server by sending a packet with nonzero-length TCP offsets.

**Hack State:** System crash.

**Vulnerabilities:** Ascend terminal servers.