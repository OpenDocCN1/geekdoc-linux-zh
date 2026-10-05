# OffSec

Once launched, the image of the process is removed from memory and replaced with a malicious executable image. Finally, the process is resumed and malicious code is executed instead of the legitimate process.

Ultimately, Inline hooking, as the name suggests, involves modifying memory and introducing a hook (an instruction that redirects the code execution) into a function to point to our malicious code. Upon executing our malicious code, the flow will return back to the modified function and resume execution, as if only the original code had executed.

Hooking is a technique often employed by rootkits,⁵⁷⁵ more stealthy kind of malware. Rootkits aim to provide the malware author dedicated and persistent access to the target system through modification of system components in user space, kernel, or over OS protection rings⁵⁷⁶ such as boot or hypervisor. Since rootkits need administrative privileges to implant its hooks, it is often installed from an elevated shell or by exploiting a privilege-escalation vulnerability.

# 12.3 Evasion in Practice

This Learning Unit covers the following Learning Objectives:

+   - Understand antivirus evasion testing practices
- Manually evade AV solutions
- Leverage automated tools for AV evasion

Depending on the kind of AV we are facing during an engagement, we might want to resort to automated or manual AV evasion. Either way, first need to understand the pros and cons associated with these strategies. In this Learning Unit, we are going to understand the best practices related to AV evasion and how to perform a real AV bypass using basic manual memory evasion through PowerShell. Finally, we are going to rely on third-party tools to automate on-disk and in-memory evasion techniques.

# 12.3.1 Testing for AV Evasion

The term SecOps defines the joint collaboration between the enterprise IT department and the Security Operations Center (SOC). The goal of the SecOps team is to provide continuous protection and defense against both well-known and novel threats.

As penetration tester, we want to develop a realistic understanding of the considerations facing SecOps teams when dealing with AV products. For this reason we should start considering a few implications regarding antivirus evasion development that could help us on our engagements.

As an initial example, VirusTotal gives us a good glimpse of how stealthy our malware could, once scanned, the platform rewards our sample to every antivirus vendor that has an active membership.

⁵⁷⁴ (Mantydas Baranauskas, 2019), https://ired.team/offensive-security/code-injection/process-hollowing-and-image-reports
⁵⁷⁵ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Rootkit
⁵⁷⁶ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Protection_ring

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

359