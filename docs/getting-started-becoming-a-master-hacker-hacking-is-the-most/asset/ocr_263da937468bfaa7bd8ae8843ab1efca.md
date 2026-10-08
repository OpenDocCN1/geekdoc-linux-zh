locked. If the hacker knows that this vulnerability exists, then they can often exploit it.

# ### What is Vulnerability Scanning?

Vulnerability scanning is the process of looking for **known** vulnerabilities. We usually use a tool known as a vulnerability scanner, which sends probes to operating systems, services, and applications to determine whether a known vulnerability exists. These scanners are neither perfect nor stealthy.

Although penetration testers often use vulnerability scanners, hackers who must remain stealthy seldom get the opportunity because these vulnerability scanners are very “noisy” and can be easily detected.

Nevertheless, if the attacker is in a position to use a vulnerability scanner, they can save hours, days, or weeks of work.

In addition, vulnerability scanners tend to generate a large number of false positives (see below). It is the job of the pentester to determine whether a potential vulnerability found by the scanner is a real vulnerability or not by attempting to exploit it.

# ### How Does a Vulnerability Scanner Work?

Vulnerability scanners such as Nessus, Nexpose, Qualys, and Acunetix (there are any others) maintain databases of known vulnerabilities. These vulnerabilities have telltale signs or signatures that the scanners can probe to see whether they exist. For instance, the EternalBlue vulnerability that was exploited by such ransomware as WannaCry and Petya takes advantage of a flaw in the Windows driver file $s v r . s y s .$