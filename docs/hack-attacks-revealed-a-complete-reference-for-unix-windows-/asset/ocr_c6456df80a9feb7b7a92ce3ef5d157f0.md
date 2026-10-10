Johannes Erdfelt, a security specialist and hacker enthusiast, has divided DNS spoofing into three conventional techniques:

+   - **Technique 1: DNS caching with additional unrelated data.** This is the original and most widely used attack for DNS spoofing on IRC servers. The attacker runs a hacked DNS server in order to get a victim domain delegated to him or her. A query sent about the victim domain is sent to the DNS server being hacked. When the query eventually traverses to the hacked DNS server, it replies, placing bogus data to be cached in the Answer, Authority, or Additional sections.
+   - **Technique 2: DNS caching by related data.** With this variation, hackers use the methodology in technique 1, but modify the reply information to be related to the original query (e.g., if the original query was my.antispoof.site.com, pointing to bogus information to be cached).
+   - **Technique 3: DNS ID prediction.** Each DNS packet has a 16-bit ID number associated with it, used to determine what the original query was. In the case of the renowned DNS daemon, BIND, this number increases by 1 for each query. A prediction attack can be initiated here— basically a race condition to respond before the correct DNS server does.

# Trojan Infection

Trojan can be defined as a malicious, security-breaking program that is typically disguised as something useful, such as a utility program, joke, or game download. As described in earlier chapters, Trojans are often used to integrate a backdoor, or “hole,” in a system’s security countenance. Currently, the spread of Trojan infections is the result of technological necessity to use ports. Table 8.1 lists the most popular extant Trojans and ports they use. Note that the lower ports are often used by Trojans that steal passwords, either by emailing them to attackers or by hiding them in FTP-directories. The higher ports are often used by remote-access Trojans that can be reached over the Internet, network, VPN, or dial-up access.

**Table 8.1 Common Ports and Trojans**

| PORT NUMBER | TROJAN NAME |
| :--- | :--- |
| port 21 | Back Construction, Blade Runner, Doly Trojan, Fore, FTP Trojan, Invisible FTP, Larva, WebEx, WinCrash, lamer_FTP |
| port 25 | Ajan, Antigen, Email Password Sender, Haebu Coceda (= Naebi), Happy 99, Kuang2, ProMail Trojan, Shritizi, lamer_SMTP, Stealth, Tapiras, Terminator, WinPC, WinSpy |
| port 31 | Agent 31, Hackers Paradise, Masters Paradise |
| port 41 | DeepThroat 1.0-3.1 + Mod (Foreplay) |
| port 48 | DRAT v 1.0-3.0b |
| port 50 | DRAT |
| port 59 | DMSetup |
| port 79 | Firehotker |