# Chapter 4 · Attacking and Defending Windows Professional

may be automatically reused in the future for repeatable logons or access to secured network-based resources. It saves time and repetitive energy from end users who must consistently re-enter usernames and passwords for resource access. Currently, there are no published vulnerabilities that exploit the credential manager allowing malicious users or processes the ability to retrieve credentials. This feature is XP-specific.

+   * Internet Connection Firewall (ICF) The ICF feature is a good utility considering that it is freely bundled with the OS for Windows XP. It protects against Transmission Control Protocol (TCP)-based attacks and requires only one click to implement. It is a good tool that adequately protects unsolicited network-based attacks. It is easy to use, and is free! In terms of security impact, ICF provides adequate protection for unsolicited attacks, network probes, and port scans. However, it should not be confused with BlackICE or Tiny because it does not have a detail-oriented intrusion detection technology nor not protect against session hijacking, some protocol or bandwidth attacks, and all application-layer attacks. This feature is XP-specific.

+   * Set of Policy (RSoP) The RSoP administration tool allows administrators to verify the effects of a Group Policy configuration on a system before it is implemented on such system. The feature provides an excellent interface for troubleshooting. Administrators can view potentially unexpected or undesired policy effects before being pushed to production status. There is no security impact from this feature. It is not XP-specific.

# Attacking XP Professional

Attacking Windows XP Professional is similar to attacking other operating systems—and yes, some of the same attacks work. However, a few arise when you are attacking a system that has implemented some of the key security features within the XP Professional environment. In the following section, you will learn to identify the OS in an organizational environment in addition to learning to identify a system with the XP Internet Connection Firewall implemented.You will also learn the details for the most critical attacks that currently exist specifically for the XP Professional platform.

![](bbox=[0.065, 0.94, 0.295, 0.97])