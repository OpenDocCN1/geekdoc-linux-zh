# FIGURE 2.9
A ping flood.

![](bbox=[0.06, 0.16, 0.98, 0.51])

The Ping of Death exploit gives an idea of how the simplest protocols and message interac-\ntions can be used by the creative hacker. Not all attacks are attempts to break into your com-\npater. Some are merely destructive. In this case, the goal is to crash the machine. (System\ncrashes also might be an indicator that you need to check your system for installed trojan pro-\ngrams. You might have been duped into loading a trojan program, but the program itself\nmight require a system reboot to activate.)

*ping* is a very useful basic networking tool. You might not want to disable *ping* altogether. In\ntoday's Internet environment, conservative folks recommend disabling incoming *ping* or at\nleast severely limiting from whom you accept echo requests. Because of *ping*'s history of\nInvolvement in DoS attacks, many sites no longer respond to external *ping* requests from any\nbut selected sources. This has always seemed to be an overreaction to the relatively small\nthreat of a DoS based on ICMP when compared to the more ubiquitous and dangerous threats\nagainst applications and other protocols within the stack.

Dropping *ping* requests isn't a solution for the victim host, however. Regardless of how the\nrecipient of the flood still reacts to the packets, the system (or network) can still be over-\nwhelmed in the process of inspecting and dropping a flood of requests.