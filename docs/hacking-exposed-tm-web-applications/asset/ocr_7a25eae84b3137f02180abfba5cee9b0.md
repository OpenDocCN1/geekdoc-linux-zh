# 72 Hacking Exposed Web Applications

described. Use the dumpbin tool included with Win32 developer tools to assist in this, as shown in the following example using IsapiEpt.dll:

```
dumpbin /imports IsapiEpt.dll find "RevertToSelf"
```

# Netscape Enterprise Server

Netscape Enterprise Server (NES) is a popular e-commerce and intranet Web platform with a handful of published vulnerabilities. In this section we'll discuss the most severe of these vulnerabilities, including a known with NES used as a reverse proxy.

The issues cited below pertain mostly to NES, although some may affect a product called iPlanet Web Server Edition. The relationship of Netscape and iPlanet is confusing, but there's a little history to clear things up. Netscape was acquired by America Online (AOL) in March 1999. Following the acquisition, AOL continued to develop the Netscape products and brand them under a new division of the company called AOL-SBS (AOL Strategic Business Solutions). Also in 1999, AOL and Microsystems created a joint venture business called iPlanet with the goal of marketing the companies' various Web software technologies. The iPlanet alliance was officially dissolved in March 2002, and AOL retained "Netscape" branded products and returned "iPlanet" branded products. Whatever their past history, NES and iPlanet Web are now marketed as entirely separate products by their respective owners.

# Netscape Enterprise Buffer Overflows

| Popularity: |
|---||
| Simplicity: | 7 |
| Impact: | 10 |
| Risk Rating: | 8 |

Two recently announced buffer overflows in Netscape Enterprise Server reminded the world that Isn't the only high-profile Web server platform to suffer from such problems. With any buffer overflow allows execution of arbitrary code as a privileged user, these are the most devastating types of attacks against a Web application.

The first buffer overflow affects NES 3.6 with Service Pack 2 and Netscape FastTrack 2.0.1. It is fairly straightforward to exploit—simply send any arbitrary request comprised of 4,080 characters plus the appropriate shellcode:

```
GET /[buffer][shellcode] HTTP/1.0
```

The commands contained in the shellcode will execute as LocalSystem on Windows.
The second buffer overflow condition is exploited by sending a GETPROPERTIES request with the appropriate buffer and shellcode:

![](bbox=[0.05, 0.477, 0.126, 0.545])