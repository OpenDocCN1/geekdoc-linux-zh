is set up for you and describes how you can modify the targeted SELinux policies to personalize your SELinux policy settings.

# Understanding Security Enhanced Linux

With traditional UNIX and Linux systems, when a user got root access to your computer, he owned the machine. The root user (or whoever took over as root) could override ownership, read/write/execute permissions, and scheduling priorities. Likewise, an attack on a Web server (http daemon) could allow an attacker full privileges of the apache user account, instead of limiting the attack to a single set of virtual hosts resources.

Organizations such as the United States National Security Agency (NSA) recognize the need to have operating systems in secure environments to be able to protect information in terms of confidentiality and data integrity. The standard security model made Linux and UNIX systems unacceptable for highly secure environments, where the risk of one exploit taking down the whole operating system was unacceptable. The mechanism NSA recommended to implement highly secure systems is referred to as Mandatory Access Control (MAC).

The SELinux project aims at providing MAC functionality to the Linux kernel. By implementing rules for what operating system components can and can't do, an application that security flaws or has been taken over for malicious intent can contain. In other words, gaining control of one component of a system doesn't allow a cracker to take over the entire computer.

Despite the fact that SELinux is complex, many of the bugs have been worked out of it in recent releases and the default settings are quite easy to work with. I would recommend enabling SELinux on a server you are testing, to prepare to one day enable SELinux to protect your Internet servers.

# Types and roles in SELinux

The mechanisms for implementing security policies in SELinux are referred to as policies. Any system that implements SELinux selects a particular policy (strict, targeted, and so on) that results in a constrained set of rules that meet the level of security on the system.

Using policy configuration files, SELinux implements two different security models: Type Enforcement (TE) and Role-Based Access Control (RBAC).

+   - Type Enforcement — Under the TE model, every object in the operating system is bound to a security attribute called a type. Every process is bound to a security attribute called a domain. This approach allows for very tight control of every object in the operating system. Every user is allowed to access objects in the operating system based on the domain in which he or she is allowed to operate.