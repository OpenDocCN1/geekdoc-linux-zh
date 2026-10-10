bility attacks discussed in Chapter 9? These exploits can be practical assessments for potential Web page hacking.

Let’s continue with target IP address and port scans. Assuming a Class C network block, we’ll use the TigerSuite TigerBox Toolkit/Scanners/IP Range Scan to verify our active addresses and possibly to uncover other listening nodes (see Figure 12.37).

With these findings, a hacker would consider our target administrator to be a “lamer,” basically an ignorant or inexperienced IS technician—whose job may be in jeopardy if these potentially vulnerable nodes contain security breaches. More important, we’ll carefully note the following:

Host IP DNS Resolution
Address
206.0.139.8 mtapel.xyzinc.net
206.0.139.89 kflippel.xyzinc.net

Chances are that these are usernames, possibly those belonging to IS technicians who opened some firewall test ports for their nodes. This leads to the conclusion that two additional email addresses have been uncovered: mtapel@xyzinc.net and kflippel@xyzinc.net. The most obvious step a hacker would take next would be to invoke this TigerSuite module: TigerBox

![](bbox=[0.14, 0.425, 0.785, 0.755])

**Figure 12.37** Searching for more clues.

Toolkit/Scanners/IP Port Scanner. For conciseness, only pertinent extractions from each scan are shown in Figure 12.38.

Clearly, the network administrators responsible for the security of this particular network have overlooked monumental, gaping holes. Let’s see what the next step, some social engineering, reveals.

# *Step 3: Social Engineering*