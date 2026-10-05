# OffSec

Penetration Testing with Kali Linux

is everyone's responsibility, and processes that receive feedback from the entire organization well educate employees about how the controls are typically important to a successful security program.

# 3.4 Security Principles, Controls, and Strategies

This Learning Unit covers the following Learning Objectives:

+   - Understand the importance of multiple layers of defense in a security strategy
- Describe threat intelligence and its applications in an organization
- Learn why access and user privileges should be restricted as much as possible
- Understand why security should not depend on secrecy
- Identify policies that can mitigate threats to an organization
- Determine which controls an organization can use to mitigate security threats

# 3.4.1 Security Principles

During this Learning Unit, we will begin to explore a few security⁶⁷ principles⁶⁸ we might encounter throughout our OffSec Learning Journey. This subject could be an in-depth Module, for now, we'll cover a few high-level descriptions.

The Principle of Least Privilege⁹ expresses the idea that each part within a system should only be granted the least possible privileges needed to achieve its task. Whether referring to users on a machine or lines of code in a program, strictly adhering to this discipline can greatly narrow the attack surface.

Earlier we the 2019 Capital One Attack. We will recall that this attack was facilitated by leveraging a Web Application Firewall with permissions that were too high for its required functions. It is important to understand that the Principle of Least Privilege does not only apply to human individuals or groups, but any entity (including machines, routers, and firewalls) that can read, write, or modify data.

The Zero Trust¹⁰ model takes the Principle of Least Privilege and carries it to its ultimate conclusion. This model advocates for removing implicit trust of networks and has a goal of protecting access to resources, with granular authorization processes for every resource request.

Open Security,¹¹ a somewhat counter-intuitive principle, states that the security of a system should not depend on its secrecy. In other words, if an attacker knows exactly how the system's security is implemented, the attacker should be thwarted. This isn't to say that nothing should be secret. Credentials are a clear case when the security of a password depends

> ⁶⁷ (Wheeler, 2021), https://dw.com/secure-Programs/Secure-Programs-HOWTO/follow-good-principles.html
⁶⁸ (Patchstack, 2021), https://blog.threatpress.com/security-design-principles-owasp/
⁶⁹ (Wikipedia, 2021), https://en.wikipedia.org/wiki/Principle_of_least_privilege
¹⁰ (Wikipedia, 2021), https://en.wikipedia.org/wiki/Zero_trust_security_model
¹¹ (Wikipedia, 2021), https://en.wikipedia.org/wiki/Open_security

PWK - © 2023 OffSec Services Limited. All rights reserved.

44