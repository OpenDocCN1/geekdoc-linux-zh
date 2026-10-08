# Chapter 3: Hacking Web Servers

script execution, content indexing, Web-based printing, and so on). The functionality embodied in these various DLLs can be invoked simply by requesting a file with the appropriate extension of IIS. For example, requesting a file with the .printer (whether that file actually exists or not) will invoke the DLL to handle Web-based printing.

This architecture, termed the Internet Server Application Programming Interface (ISAPI) by Microsoft, provides extensible for hackers with a myriad of different functionality to exploit malicious input. They simply need to construct a URL that calls for a specific file, and then provide malformed input to the ISAPI DLL that is invoked by that request. The results of such attacks have proven disastrous for servers IIS over the last few years, and is a primary example of the old security adage that leads to insecurity. Stated another way, the more functionality provided out of the box by your Web server, the greater your exposure to attack. Let's take a look at how ISAPI functionality can be exploited in the real world

# ISAPI DLL Bufferflows

| Popularity: | 10 |
| Simplicity: | 9 |
| Impact: | 10 |
| Risk Rating: | |

One of the most extreme vulnerabilities associated with ISAPI DLLs is the buffer overflow. In Late 2001 and into 2002, IIS servers on the Internet were ravaged by versions of the Code Red and Nimid worms, which were both based on buffer overflow exploits of published ISAPI DLL vulnerabilities. In April 2002, another fairly severe buffer overflow in the Active Server Pages (ASP) ISAPI DLL was announced. We will discuss one example of such a vulnerability in this section.

In May 2001, eDigital Security announced discovery of a buffer overflow within the ISAPI filter that handles .printer files (C:\WINNT\System32\msw3pr.dll) that provides support for the Internet Printing Protocol (IPP). IPP extends the Web-based control of various aspects of networked printers.

The vulnerability arises when a buffer of approximately 420 bytes is sent within the HTTP Header: for a .printer ISAPI request, as shown in the following where [buffer] is approximately 420 characters.

```
GET /NULL.printer HTTP/1.0
Host: [buffer]
```

This simple request causes the buffer overflow and would normally halt IIS; however, Windows 2000 automatically restarts IIS (inetinfo.exe) following such crashes to provide greater resiliency for Web services. This, this exploit produces no visible effects from a remote perspective (unless looped continuously to deny service). While the resiliency