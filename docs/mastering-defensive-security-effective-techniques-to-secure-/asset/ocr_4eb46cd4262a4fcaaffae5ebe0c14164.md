# Finding evidence

As soon as you discover an attack, there are a lot of things that need to be done with the utmost priority, including restoring the systems and services that have been impacted. However, another critical task is to find and secure all the evidence related to the attack. This task is critical as it allows you to do the following:

+   - Determine whether the attack was executed by an insider or outsider.
- Determine whether the insider was a malicious insider or an inadvertent insider.
- Determine the vulnerability exploited by the attacker.
- Determine the impact on business data in terms of the confidentiality, integrity, and availability (CIA) triad.
- Determine the systems or services impacted by the attack.
- Collect evidence to execute legal or corrective actions (from HR).

Now that you know, there are a lot of places that you can harvest to gather digital evidence, let's look at some practices regarding the collection process itself.

# Sources of data

As you may know, there are a lot of places that you can harvest to gather digital information during a forensics process. The most common type of files that you need to find are log files as they normally record all the events on the device (we covered this topic in Chapter 15, Leveraging Pentesting for Defensive Security).

# Non-volatile memory

As we mentioned earlier, it is possible to obtain data from RAM, so in the case of a digital investigation, you may want to do a dump of the RAM to get some extra information before executing other actions or shutting down the server.