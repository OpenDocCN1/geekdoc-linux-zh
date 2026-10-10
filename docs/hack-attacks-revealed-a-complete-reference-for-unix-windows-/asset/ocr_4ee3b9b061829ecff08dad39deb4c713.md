Microsoft Internet Service Manager, Internet/intranet service daemon configuration is just a click away.

![](bbox=[0.1, 0.1, 0.95, 0.46])

Figure 9.8 Microsoft Internet Information Server Manager.

# **Liabilities**

Denial-of-Service Attacks

**Synopsis:** Malformed GET requests can cause service interruption.

**Hack State:** Service obstruction.

**Vulnerabilities:** IIS v.3/4.

**Breach:** An HTTP GET is comparable to a command-line file-grabbing technique, but through a standard browser. An attacker can intentionally launch malformed GET requests to cause an IIS DoS situation, which consumes all server resources, and therefore “hangs” the service daemon.

**Synopsis:** The Sioux DoS penetration can cause immediate CPU congestion.

**Hack State:** Severe congestion.

**Vulnerabilities:** IIS v.3/4.

**Breach:** *Sioux.c* (available on this book’s CD), by Dag-Erling Coidan Smørgrav, DoS penetration causes an immediate increase of CPU utilization to 85 percent. Multiple DoS attacks cause sustained