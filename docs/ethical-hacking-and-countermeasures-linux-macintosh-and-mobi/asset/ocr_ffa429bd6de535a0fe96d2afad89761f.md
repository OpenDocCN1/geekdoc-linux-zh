+   • StackGuard is a compiler that hardens programs against stack-smashing attacks. Programs compiled with StackGuard do not require any source code changes. It works by placing a "canary" word next to the return pointer. Alteration of the canary word indicates an attack and terminates the program.

+   • Libsafe is a dynamically loadable library that checks all calls made to vulnerable library functions. It works by substituting the vulnerable function with a functionally equivalent one. It does not have a high performance overhead and has been known to avert even unknown buffer overflow attacks.

+   • Openwall Project's nonexecutable stack kernel patch is a collection of security features for the Linux kernel that makes the stack nonexecutable. While it does not prevent all buffer overflow attacks, it can alert the user to a simple attempt.

Buffer overflows are a common cause of vulnerabilities. Some safety measures must be taken to guard the Linux operating system from being exploited due to known or unknown buffer overflows.

# How to Apply Patches to Vulnerable Programs

Users can audit open-source programs for vulnerabilities and security flaws. Users can check the home page of their Linux distribution for updates. They can also check the Web sites of software vendors and look for patches. These include the following:

+   • LCLint checks for flaws in C programs, such as memory management errors, inconsistent data sharing, improper liaisoning, dereferencing null pointers, and so on.

+   • Cqual allows a coder to define type qualifiers. It is a type checker that will perform qualifier inference to check annotations.

+   • Rough Auditing Tool for Security (RATS) verifies and audits C, C++, Perl, Python, and PHP code. It serves as a preliminary check at best and cannot be used as a replacement for code checking.

+   • Flawfinder audits code for security flaws in functions found to be especially vulnerable to buffer overflows (strcpy()), format bugs (printf()), race conditions (chmod()), shell metacharacter problems (system()), random number generation (random()), and others.

+   • Spike is used for protocol analysis and as a reproduction tool, and sharefuzz is a program used to analyze suid programs for buffer overflows using LD_PRELOAD.

Users can also make use of system scanners that run on local system security and identify potential security vulnerabilities. These include sXid, COPS, TAMU's Tiger, GNU Tiger, Nabou, and LSAT.

# Scanning Networks

Once the IP address of a target system is known, an attacker can begin the process of port scanning, or looking for holes in the system. A typical system has 216 − 1 port numbers, with one TCP port and one UDP port for each number. Each one of these ports is a potential way into the system. The most popular scanning tool for Linux is Nmap. Other tools include nescat and strobe.

Nescat can be used to scan up to port 2024. Nescat scans each port and waits 10 seconds for timeout. Then it displays the results. Nescat can be started with the following command:

```
nc −v −w 10 −z www.example.com 1−2024
```

Strobe scans ports in parallel, using maximum bandwidth while consuming minimal resources. Strobe is capable of scanning TCP ports alone. However, its developer no longer maintains strobe.

# Nmap in Linux

Nmap is undoubtedly the best port scanner available, apart from having the added functionality of OS detection, RPC identification, and ping sweeping. Nmap also comes with a front end, Nmapfe, which gives it a GUI. Nmap can also be a valuable diagnostic tool for network administrators.