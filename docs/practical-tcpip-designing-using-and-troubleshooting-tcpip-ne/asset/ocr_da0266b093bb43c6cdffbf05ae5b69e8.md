# **20.9** Different logon types: terminology (1)

We have included this section because the terms used for different types of logon can be confusing. In Module 20.3 we covered local logon, where you, sitting at AliceNT, log on to AliceNT and not to a domain, or you logon to domain **EX-NTD** while sitting at one of EX-NTD’s domain controllers.

Pass-through authentication is when the local workstation doesn’t complete the logon validation on its own, but passes over it over to a domain controller elsewhere on the network. This occurs in three situations:

+   1. You logon to this PC’s domain

This is an *interactive logon* – i.e. where the system gives you a logon dialog – to a domain, where you logon from a workstation that isn’t a domain controller, to this PC’s domain (e.g. user **Fred Blogo** logs in from PC **AliceNT** to domain **EX-NTD**). As we saw in detail earlier in this chapter, the logon is passed for authentication to one of Ex-NTD’s domain controllers:

![](bbox=[0.3, 0.36, 0.65, 0.62])

+   2. You logon to a different domain

This is an interactive logon from a workstation in one domain to a different domain (e.g. user **Fred Blogo** logs in from PC **AliceNT** to domain **TEST-NTD**). The logon is passed to one of EX-NTD’s domain controllers, which in turn passes it to one of TEST-NTD’s domain controllers:

![](bbox=[0.3, 0.75, 0.7, 0.98])