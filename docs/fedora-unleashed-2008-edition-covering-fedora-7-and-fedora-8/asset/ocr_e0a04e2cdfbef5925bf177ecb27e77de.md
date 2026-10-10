![](bbox=[0.1, 0.12, 0.47, 0.42])

**FIGURE 30.2** Fedora's system-config-securitylevel client can also be used to quickly generate and implement standard or simple custom firewall rules for Linux.

You can use Fedora to create a custom firewall, perhaps supporting IP masquerading (also known as NAT) by using either ipchains or iptables. You'll find two sample scripts under the /usr/share/doc/rp-pppoe/configs directory; these are used when a digital subscriber line (DSL) is used for Internet connection.

# ## Forming a Disaster Recovery Plan

No one likes planning for the worst, which is why two-thirds of the population do not have a will. It is a scary thing to have your systems hacked: One or more criminals have broken through your carefully laid blocks and caused untold damage to the machine. Your boss, if you have one, will want a full report of what happened and why, and your users will want their email when they sit down at their desks in the morning. What to do?

If you ever do get hacked, nothing will take the stress away entirely. However, if you take the time to prepare a proper response in advance, you should at least avoid premature aging. Here are some tips to get you started:

+   - **Do not just pull the network cable out**—This alerts the hacker that he has been detected, which rules out any opportunities for security experts to monitor for that hacker returning and actually catch him.
+   - **Inform only the people that need to know**—Your boss and other IT people are at the top of the list; other employees are not. Keep in mind that it could be one of the employees behind the attack, and this tips them off.
+   - **If the machine is not required and you do not want to trace the attack, you can safely remove it from the network**—However, do not switch it off because some backdoors are enabled only when the system is rebooted.