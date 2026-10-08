
## 7. Finding Vulnerabilities to Exploit

Every adversary--no matter how strong and powerful--always has a weakness. Master OTW

Now that we have a good idea of the ports, services, operating system, and technologies from our passive and active reconnaissance of the potential target system, our next step is to find vulnerabilities that might be exploited by the attacker. According to Wikipedia, a vulnerability is: a weakness which can be exploited by a threat actor, such as an attacker; to perform unauthorized actions within a computer system.

I like to think of a vulnerability as a window or door to the computer system that hasn't been properly closed or locked. If the hacker knows that this vulnerability exists, then they can often exploit it.

### What is Vulnerability Scanning?

Vulnerability scanning is the process of looking for known vulnerabilities. We usually use a tool known as a vulnerability scanner, which sends probes to operating systems, services, and applications to determine whether a known vulnerability exists. These scanners are neither perfect nor stealthy.

Although penetration testers often use vulnerability scanners, hackers who must remain stealthy seldom get the opportunity because these vulnerability scanners are very “noisy” and can be easily detected.

Nevertheless, if the attacker is in a position to use a vulnerability scanner, they can save hours, days, or weeks of work.

In addition, vulnerability scanners tend to generate a large number of false positives (see below). It is the job of the pentester to determine whether a potential vulnerability found by the scanner is a real vulnerability or not by attempting to exploit it.

### How Does a Vulnerability Scanner Work?

Vulnerability scanners such as Nessus, Nexpose, Qualys, and Acunetix (and others) maintain databases of known vulnerabilities. These vulnerabilities have telltale signs or signatures that the scanners can probe to see whether they exist. For instance, the EternalBlue vulnerability that was exploited by such ransomware as WannaCry and Petya takes advantage of a flaw in the Windows driver file srv.sys.

The vulnerability scanner simply checks to see whether that file at **C:\Windows\system32\drivers** has been updated to srv2.sys. If it has been updated, the system is not vulnerable to the EternalBlue exploit and all the malware that uses it.

In addition, vulnerability scanners check to see whether operating systems and applications are up to date on their patches.

### What are False Positives?

False positives are generated when a system such as a vulnerability scanner says something exists, but it does not. For instance, if your system vulnerability scanner says that your system is vulnerable to EternalBlue and it is not, that is a **false positive**. Unfortunately, vulnerability scanners are far from perfect and generate a lot of false positives.

- **False Positive**
  - The scanner indicates the vulnerability exists (positive) and it doesn’t exist (false).
- **False Negative**
  - The scanner indicates the vulnerability doesn’t exist (negative) and it does exist (true).
- **True Positive**
  - The scanner indicates the vulnerability exists (positive) and it does exist (true).
- **True Negative**
  - The scanner indicates the vulnerability doesn’t exist (negative) and it doesn’t exist (true).

Although false negatives can be frustrating, given a choice between a system that produces false positives or false negatives, we certainly prefer the false positive.

### EternalBlue nmap Vulnerability Scanner

Let’s test our Windows 7 system for the presence of the EternalBlue vulnerability. As I mentioned earlier in **Chapter 6**, nmap’s capabilities have expanded dramatically in recent years. Nmap can now run specialized scripts written in Lua. One of those scripts is a **EternalBlue vulnerability scanner**. Note that this script only tests for this single vulnerability.

To run this vulnerability scanning script, we simply need to point our nmap scanner at the IP of the Windows system and its SMB port (445) and then include the option **-script** followed by the name of the script, in this case **smb-vuln-ms17-010**.

```
kali > nmap 192.168.0.157 -p445 -script smb-vuln-ms17-010
```
