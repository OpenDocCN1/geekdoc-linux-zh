# **BIND Attack**

In a BIND attack, an intruder can erase your system logs and install tools to gain administrative access. In addition, once the attacker has gained access, he or she uses the attacked system to scan for and attack other network systems running vulnerable versions of BIND. In effect, the intruder uses the compromised system to attack hundreds of remote systems, resulting in additional successful compromises.

# **Sendmail Flaws**

Flaws have been found in Sendmail over the years. In one of the most common intrusions, the attacker sends a crafted mail message to a machine running Sendmail. Sendmail, in turn, interprets the message as instructions requiring it to send the password file to the attacker’s machine.

# **SNMP Flaws**

SNMP uses an unencrypted community string as an authentication mechanism, and the default community string used by many SNMP devices is public. Sniffed SNMP traffic can reveal information about the structure of your network, as well as the systems and devices attached to it.

# # Honeypot System

A system designed to attract attackers is known as a *honeypot*. If an attacker managed to get past your packet filter and starts scanning for options, the honeypot should be the system configured to look like it is vulnerable to known attacks. A honeypot system should not be too easy to spot because a savvy intruder will be tempted to look further on the network.

![](bbox=[0.235, 0.51, 0.94, 0.74])

# **Goals of a Honeypot**

There are several goals for a honeypot:

+   - To provide a lure so that attackers stay away from other equipment. You want the attackers to see a vulnerable system that they know they can exploit and gain access to. This system needs to be such that the attacker focuses his or her energy on exploiting the system, as opposed to the server with important data that is sitting right next to it.

+   - To know that the honeypot system will be attacked, so you can take extra measures when logging in to it. These logs should be moved off the system frequently—perhaps hourly or daily if your network is a high-profile target.