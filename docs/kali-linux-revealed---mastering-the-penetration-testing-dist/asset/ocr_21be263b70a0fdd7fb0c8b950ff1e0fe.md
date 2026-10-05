designed to make it harder to exploit vulnerabilities, such as Data Execution Prevention⁵ (DEP) Address Space Layout Randomization⁶ (ASLR). However, just there is no publicly-known exploit for a specific vulnerability, that does not mean one does exist (or one that cannot be created). For example, many organizations sell commercialized exploits that are never made public, so all vulnerabilities must be treated as potentially exploitable.

# 11.2.1. Vulnerability Assessment

A vulnerability is considered a weakness that could be used in some manner to compromise the confidentiality, integrity, or availability of an information system. In a vulnerability assessment, your objective is to create a simple inventory of discovered vulnerabilities within the target environment. Concept of a target environment is extremely important. You must be sure to stay within the scope of your client's network and require objectives. The scope of an assessment can cause an interruption of service, a breach of trust with your client, or legal action against you and your employer.

Due to its relative simplicity, a vulnerability test is often completed in more mature environments on a regular basis as part of demonstrating their due diligence. In most cases, an automated tool, like ones in the Vulnerability Analysis⁷ and Web Applications⁸ categories of the Kali Tools site and Kali desktop Applications, is used to discover live systems in a target environment, identifying signatures, and enumerate them to discover as much as possible as the server software, version, platform, and so on.

This information is then checked for known signatures of potential issues or vulnerabilities. These signatures are made up of data point combinations that are intended to represent known issues. Multiple data points are used, because the more data points you use, the more accurate the identification. A very large number of potential data points exists, including but not limited to:

+   * Operating System Version: It is not uncommon for software to be vulnerable on one operating system version but not on another. Because of this, the scanner will attempt to determine, as accurately as possible, what operating system version is hosting the targeted application.
* Patch Level: Many times, patches for an operating system will be released that do not increase the version information, but still change the way a vulnerability respond, or even eliminate the vulnerability entirely.
* Processor Architecture: Many software applications are available for multiple processor architectures such as Intel x86, Intel x64, versions of ARM, UltraSPARC, and so on.

> ⁵https://en.wikipedia.org/wiki/Executable_space_protection#Windows
⁶https://en.wikipedia.org/wiki/Address_space_layout_randomization
⁷http://tools.kali.org/category/vulnerability-analysis
⁸http://tools.kali.org/category/web-applications