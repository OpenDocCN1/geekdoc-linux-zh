![](bbox=[0.12, 0.04, 0.3, 0.09])

# 15.1.7.1 Exercises

+   1. Fix the overflow buffer such that the EIP register will be overwritten by your chosen return address instruction.
+   2. Install the ASX to MP3 Converter application located under the C:\Tools\fixing_exploits directory; download the exploit for ASX to MP3 Converter from EDB391 and edit it in order to get a shell on your dedicated Windows machine.

# 15.2 Fixing Web Exploits

Web application vulnerabilities do not often result in memory corruption. This means that they are not affected by protections provided by the operating system such as DEP and ASLR and they are significantly easier to re-purpose.

# 15.2.1 Considerations and Overview

Even though we might not have to deal with hex-encoded payloads in web exploits, it is important that we properly read the code to understand what considerations must be taken in our editing process.

When modifying web exploits, there are several key questions we generally need to ask while approaching the code:

+   • Does it initiate an HTTP or HTTPS connection?
+   • Does it access a web application specific path or route?
+   • Does the exploit leverage a pre-authentication vulnerability?
+   • If not, how does the exploit authenticate to the web application?
+   • How are the GET or POST requests crafted to trigger and exploit the vulnerability?
+   • Does it rely on default application settings (such as the web path of the application) that may have been changed after installation?
+   • Will oddities such as self-signed certificates disrupt the exploit?

In addition, we must remember that public web application exploits do not take into account additional protections such as .htaccess. This is mainly because the exploit author can not possibly know about these protections during the development process and they are outside the exploit’s scope.

# 15.2.2 Selecting the Vulnerability

Let’s consider the following scenario. During an assessment we discover a Linux host that has an apache2 server exposed. After enumerating the web server, we find an installation of CMS Made Simple version 2.2.5 listening on TCP port 443. This version appears to be vulnerable to remote code execution and a public exploit is available on Exploit-DB.392

+   391 (Offensive Security, 2015), https://www.exploit-db.com/exploits/38457/  
+   392 (Offensive Security, 2018), https://www.exploit-db.com/exploits/44976