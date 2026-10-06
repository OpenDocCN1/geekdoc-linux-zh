
# Probing the Network 327

![](img/b9022ea8d49ef539d37d0ec09f73f71c_348_0.png)
FIGURE 12-4 NetBrute main screen

![](img/b9022ea8d49ef539d37d0ec09f73f71c_348_1.png)
FIGURE 12-5 Shared drives

## CHAPTER 12 Assessing System Security

Shared folders and drives are important to security because they provide one possible way for a hacker to get into a system. If the hacker can gain access to that shared folder, she can use that area to upload a Trojan horse, virus, key logger, or other device. The rule on shared drives is simple: If you don't absolutely need them, then don't have them. Any drive or folder can be shared or not shared. Unless there is a compelling reason to share a drive, you should not. And if you decide to share it, then the details of shared drive—including content and reason for sharing it—should be in your security documentation.

With the PortScan tab, you can find ports. It works exactly like the first tab except that giving you a list of shared folders/drives, it gives you a list of open ports. Thus, with NetBrute, you get a port scanner and a folder scanner. In essence the second tab contains the most pertinent information you might obtain from other products such as NetCop.

When scanning your network, these first two tabs will be the most important. However, if you wish to check the security of your web server you would want to use the WebBrute tab. The WebBrute tab allows you to scan a target website and obtain information similar to what you would get from Netcraft. This scan gives you information such as the target system's operating system and web server software.

NetBrute is easy to use and provides most of the basic information you might need. The ability to track shared folders and drives in addition to open ports is of particular use. This tool is widely used by hackers as well as security professionals.

## Cerberus

One of the most widely used scanning utilities, and a personal favorite of this author, is the Cerberus Internet Scanner, available as a free download from https://www.cerberusftp.com/download/ (you can simply do a web search for Cerberus with your favorite search engine). This tool is remarkably simple to use and very informative. When you launch this tool, you will see a screen like the one shown in Figure 12-6.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_349_0.png)
FIGURE 12-6 The Cerberus Internet Scanner

From this screen you can click on the button on the far left that has an icon of a house. Or you can go to File and select Host. Then you simply enter key either the URL or the IP address of the machine that you wish to scan. Click either the button with the "S" on it or go to File and select Start Scan. Cerberus will then scan and give you a wealth of information. You can see in Figure 12-7 all the various categories of information that you get from this scan.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_350_0.png)
FIGURE 12-7 Cerberus scan results

Click on the third button to review the report. The report will launch Hypertext Markup Language (HTML) document (thus the document is easy to save for future reference) with links to each category. Click the category you wish to see. As a rule you should save all security reports for future audits. In the event of litigation it may be necessary for you to verify that you are practicing diligence in implementing and auditing security. It is also important to document these activities as a part of record of precautions you take. This documentation could be crucial in the case of any external audit or even in helping a new IT security professional get to speed on what actions have been taken. This information should be stored in a secure location, as it is of great value to someone wishing to compromise your system security. An example of the report is shown in Figure 12-8.

One of the most interesting sections to review, particularly for a security administrator, is the NT Registry report. This report will examine the Windows Registry and inform you of any security flaws found there and how to correct them. This report is shown in Figure 12-9.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_351_0.png)
FIGURE 12-8 The Cerberus Report

![](img/b9022ea8d49ef539d37d0ec09f73f71c_351_1.png)
FIGURE 12-9 The NT Registry Report

## Probing the Network
## 331

This list shows specific Windows Registry settings, why those settings are not particularly secure, and what you can do to secure them. For obvious reasons, this tool is very popular with hackers. Cerberus can provide a great map of all system's potential vulnerabilities including, but not limited to, shared drives, insecure registry settings, services running, and known flaws.

## Probing the Network

## 331

This list shows specific Windows Registry settings, why those settings are not particularly secure, and what you can do to secure them. For obvious reasons, this tool is very popular with hackers. Cerberus can provide a great map of all system's potential vulnerabilities including, but not limited to, shared drives, insecure registry settings, services running, and known flaws.

(Wait, the OCR text contains repeated sections. Processing unique flow:)

One of the most widely used scanning utilities, and a personal favorite of this author, is the Cerberus Internet Scanner, available as a free download from https://www.cerberusftp.com/download/ (you can simply do a web search for Cerberus with your favorite search engine). This tool is remarkably simple to use and very informative. When you launch this tool, you will see a screen like the one shown in Figure 12-6.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_349_0.png)
FIGURE 12-6 The Cerberus Internet Scanner

From this screen you can click on the button on the far left that has an icon of a house. Or you can go to File and select Host. Then you simply enter key either the URL or the IP address of the machine that you wish to scan. Click either the button with the "S" on it or go to File and select Start Scan. Cerberus will then scan and give you a wealth of information. You can see in Figure 12-7 all the various categories of information that you get from this scan.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_350_0.png)
FIGURE 12-7 Cerberus scan results

Click on the third button to review the report. The report will launch Hypertext Markup Language (HTML) document (thus the document is easy to save for future reference) with links to each category. Click the category you wish to see. As a rule you should save all security reports for future audits. In the event of litigation it may be necessary for you to verify that you are practicing diligence in implementing and auditing security. It is also important to document these activities as a part of record of precautions you take. This documentation could be crucial in the case of any external audit or even in helping a new IT security professional get to speed on what actions have been taken. This information should be stored in a secure location, as it is of great value to someone wishing to compromise your system security. An example of the report is shown in Figure 12-8.

One of the most interesting sections to review, particularly for a security administrator, is the NT Registry report. This report will examine the Windows Registry and inform you of any security flaws found there and how to correct them. This report is shown in Figure 12-9.

![](img/b9022ea8d49ef539d37d0ec09f73f71c_351_0.png)
FIGURE 12-8 The Cerberus Report

![](img/b9022ea8d49ef539d37d0ec09f73f71c_351_1.png)
FIGURE 12-9 The NT Registry Report

This list shows specific Windows Registry settings, why those settings are not particularly secure, and what you can do to secure them. For obvious reasons, this tool is very popular with hackers. Cerberus can provide a great map of all system's potential vulnerabilities including, but not limited to, shared drives, insecure registry settings, services running, and known flaws.

(Note: The provided OCR text contained significant repetitions of headers and pages. I have merged the unique content flow based on the provided text.)
