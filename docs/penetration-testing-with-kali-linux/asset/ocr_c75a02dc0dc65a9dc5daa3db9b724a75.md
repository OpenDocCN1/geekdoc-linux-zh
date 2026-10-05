# OffSec

Penetration Testing with Kali Linux

![](bbox=[0.168, 0.093, 0.823, 0.473])

Figure 204: List of payloads available in shellter

Note that in order to restore the execution flow through the Stealth Mode option, payloads needs to terminate by exiting the current thread.

After testing, it seems that any non-Metpreter payload fails to be executed correctly on Windows 11, and we will need to resort to Metpreter-based payloads.

At this stage, we should not worry too much about the differences between standard and Metpreter payloads we are going to learn about those in an uncommon Module.

In order to test Shellter's bypass capabilities, we will use the Metpreter version of the reverse shell payload that Avira detected at the beginning of this Module. After submitting L for listed payloads, we will select the first payload. We are then presented with the default options from Metasploit, such as the reverse shell host (LHOST) and port (LPORT), which we should fill with our local Kali's IP address and listening port.