# Attacking and Defending Unix • Chapter 14

For our own attack we do not need to be quiet, the same methods apply. Scanning the target system, identifying and gathering information about services, and creating a plan of attack are all necessary for our attack. And if the whim strikes us, we can be quiet to see how easily network defenses can be evaded.

When an attacker making a directed attack at a host has finally gathered enough information to proceed, a plan for attack will have been formulated. This involves finding a service that is known to be vulnerable to an issue, or attempting to find a vulnerability in a service on the target. Once the plan has been made, the attack begins.

# Gaining Remote Access

Gaining remote access is the objective of most attacks against a Unix system. Remote access to a host allows an attacker to access the resources of the compromised host, and turn in the system being used as a platform for the launch of other attacks. Remote access attempts are launched through exploitation of services executing on a Unix host.

In the case of a service executing with minimal privileges, remote access can result in unprivileged access. In the case of a service executing with elevated privileges, gaining remote access through the service results in a catastrophic compromise of administrative privileges. In the case of unprivileged remote access, it is merely a matter of time before the attacker finds a way to gain elevated privileges.

Remote access is often gained through one of a few methods. One such method is the exploitation of a programming error such as a buffer overrun or format string vulnerability. Another is the use of an input validation bug, such as that of a PHP vulnerability. A brute force attack may also be used. The following sections examine each type of attack in detail.

# Exploiting Programming Errors

Programming errors are one of the more commonly exploited types of vulnerabilities in software. Programming errors are broad, and often obscure bugs that exist in software. Their occurrence is common, and their exploitation usually catastrophic.

Two of the most commonly exploited programming errors are buffer overflows and format string vulnerabilities. In the case of an exploitable instance of either these types of vulnerabilities, it is possible for an attacker to execute arbitrary code. The code executed by the attacker is run on the vulnerable host in

![](bbox=[0.708, 0.946, 0.928, 0.966])