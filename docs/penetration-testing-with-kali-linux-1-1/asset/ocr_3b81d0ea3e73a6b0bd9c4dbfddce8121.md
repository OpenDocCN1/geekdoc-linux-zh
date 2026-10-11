# 22. The Metasploit Framework

As we have worked through the preceding modules, it should be clear that working with public exploits is difficult. They must be modified to fit each scenario, they must be tested for malicious code, each uses a unique command-line syntax, and there is no standardization in coding practices or languages. Some exploits are written in Perl, some in C, others in PowerShell, and we've even seen exploit payloads that needed to be deployed by copying and pasting them into a Ncat connection.

In addition, there are a variety of post-exploitation tools, auxiliary tools, and innumerable attack techniques that must be considered in even the most basic attack scenarios.

Exploit frameworks aim to address some or all of these issues. Although they vary somewhat in form and function, each aims to consolidate and streamline the process of exploitation by offering a variety of exploits, simplifying the usage of these exploits, easing lateral movement, and assisting with the management of compromised infrastructure. Most of these frameworks offer dynamic payload capabilities. This means that for each exploit in the framework, we can choose various payloads to deploy.

Over the past few years, several exploit and post-exploitation frameworks have been developed, including Metasploit,705 Core Impact,706 Immunity Canva s,707 Cobalt Strike,708 and PowerShell Empire,709 each offering some or all of these capabilities.

While many of these frameworks are commercial offerings, the Metasploit Framework (MSF, or simply Metasploit) is open-source, is frequently updated, and is the focus of this module.

As described by its authors, the Metasploit Framework, maintained by Rapid7,710 is "an advanced platform for developing, testing, and using exploit code". The project initially started off as a portable network game711 and has evolved into a powerful tool for penetration testing, exploit development, and vulnerability research. The Framework has slowly but surely become the leading free exploit collection and development framework for security auditors. Metasploit is frequently updated with new exploits and is constantly being improved and further developed by Rapid7 and the security community.

Kali Linux includes the metasploit-framework package, which contains the open source elements of the Metasploit project. Newcomers to the Metasploit Framework (MSF) are often overwhelmed by the multitude of features and different use-cases for the tool. The Metasploit Framework is valuable in almost every phase of a penetration test, including information gathering, vulnerability research and development, client-side attacks, post-exploitation, and much more.

+   705 (Rapid7, 2018). https://www.metasploit.com/
+   706 (Core Security, 2018). https://www.coresecurity.com/core-impact
+   707 (Immunity, 2018). https://www.immunityinc.com/products/canvas/
+   708 (Strategic Cyber LLC, 2018). https://blog.cobaltstrike.com/category/cobalt-strike-2/
+   709 (Veris Group, 2015). https://www.powershell.empire.com/
+   710 (Rapid7, 2019). https://www.rapid7.com/
+   711 (ThreatPost, 2010). https://threatpost.com/qa-hd-modeme-metasploit-disclosure-and-ethics-052010/7399/