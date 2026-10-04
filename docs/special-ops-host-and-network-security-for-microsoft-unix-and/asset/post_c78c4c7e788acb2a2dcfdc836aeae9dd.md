
# Hunting for High Severity Vulnerabilities (HSV) • Chapter 3

variable with the strings that are known to cause SQL injection, buffer overflows, or the other problems. The auditor can also modify each request he sends, allowing him to send negative values for prices, or otherwise play with submitted entries.

Although SPIKE itself is an advanced tool, requiring knowledge of C and protocols on the part of the user to be effective, SPIKE Proxy is accessible to advanced and novice users. Although SPIKE itself is primarily used on Linux or other Unixes, SPIKE Proxy is fully supported on Windows and Linux.

## Figure 3.10 Using SPIKE Proxy

![](img/729efc56f204a2ebffb8295c3a2dfdfb_95_0.png)

Each header can be modified, new headers can be added, and so on, before the request is sent out. SPIKE Proxy is used entirely through the browser, and is compatible with both Mozilla and Internet Explorer.

Figure 3.11 shows an example of SPIKE being used to analyze a form post. This is commonly done to look for SQL injection or other issues. For each of the arguments shown, the user will look for SQL injection vulnerabilities, or PASSWORD, which will launch a dictionary attack against that field.

SPIKE Proxy stores each HTTP request and response as the requests are sent out (Figure 3.12). This page allows crawling, argument scanning (for example, SQL injection attempts), directory scanning, and buffer overflow checks to use a single initiated on any stored request. Additionally, multiple users can use instance of SPIKE Proxy, allowing them to cooperate in the process of testing a Web application.

### ### Figure 3.11 Analyzing a Form Post

![](img/729efc56f204a2ebffb8295c3a2dfdfb_96_0.png)

### ### Figure 3.12 Interactive Snapshots of SPIKE HTTP Requests

![](img/729efc56f204a2ebffb8295c3a2dfdfb_96_1.png)

www.syngress.com

# Hunting for High Severity Vulnerabilities (HSV) • Chapter 3

Together, SPIKE and SPIKE Proxy allow for a full run of application testing using HSV. SPIKE Proxy is focused on Web applications, whereas SPIKE is aimed at the more generic problem of testing arbitrary protocols.

Dave Aitel and Immunity, Inc. also offer an exciting new tool called CANVAS for a nominal fee. CANVAS is essentially an exploit engine that can be used to verify the implementation and effectiveness of patches. Figure 3.13 shows CANVAS launching an unauthenticated attack against 192.168.1.100 using the SQL Server "Hello" discovered by Dave Aitel. This vulnerability, if exploited properly, will provide the attacker with remote System privileges.

## Figure 3.13 CANVAS for Exploitation

![](img/729efc56f204a2ebffb8295c3a2dfdfb_97_0.png)

# Other Miscellaneous Resources

A large number of freeware tools hit the market every week in this busy industry; this section lists only the most popular ones. A few resources for finding and downloading HSV tools are the following:

- Special Ops Security, (www.SpecialOpsSecurity.com)
- Secure Item (www.secureitemteam.com)
- PacketStorm Security (www.packetstormsecurity.com)
- Security Focus (www.securityfocus.com)
- InfoSysSec (www.infosecsec.com)
- Next Generation Security Software (www.nextgenss.com)
- Immunity, Inc. (www.immunity.com)
- SQLSecurity (www.sqlsecurity.com)
- Arne Vidstrom (www.NTSecurity.nu)

## Case Study: Attacking Windows Domains

This case study will profile a domain escalation attack. First, I review what the targets are in a Windows domain and why they are vulnerable.

Windows 2000 domains, simply put, are Windows systems connected to facilitate the sharing of resources and ease of administration. The glue that binds a domain together is centralized administration of users and their access/restriction to domain resources. This administration is achieved through domain controllers (DCs). Domain controllers contain all the domain accounts and provide access/restriction to domain resources based on these accounts. Additionally, Windows 2000 systems also have local accounts that provide access to local resources. Depending on the role and configuration of the server, these resources can be exploited to gain administrative domain access (see Figure 3.14). With that said, an attacker's goal of penetrating a 2000 domain is achieved by compromising an administrative-level domain account.

## Figure 3.14 Impact of Local and Domain Account Compromises

![](img/729efc56f204a2ebffb8295c3a2dfdfb_98_0.png)

# Hunting for High Severity Vulnerabilities (HSV) • Chapter 3

## Target Selection in the Windows Domain

Domain Controllers are the "treasure chest" for Windows 2000 accounts and passwords. If a DC is compromised at an administrative level, all usernames and encrypted password hashes for that domain (including Domain Admins) will be likely stolen and cracked offline on the attacker's system, since DCs are the foundation of any Microsoft 2000 domain. A compromise at this level also ensures compromise of application servers and member servers. Additionally, due to password reuse, it is feasible that an attacker could compromise 2000 domains and stand-alone servers, as well non-Windows operating systems.

## Domain Controllers

Domain controllers must be single function servers. This means they should not perform or offer any other functions to the domain. The user account database is their critical resource and must be protected at all costs. Provided the server is locked-down as a single function server, offering no services beyond what is required, an attacker will need to compromise a username/password that is a member of the local Administrators group or one with administrative-level privileges (such the Domain Admins group). This can be achieved by guessing or password reuse from other sources. With said, the compromise of an account that has administrative domain privileges usually "game over" for the domain, its systems and its resources. These accounts are stored on DCs and must be protected with the strongest password controls allowable by corporate policies.

## Application Servers

Application servers on the network provide access to services such as IIS, SQL, Exchange, and Common Internet File System (CIFS). These servers are usually the secondary target of an attack against a domain. General, vulnerabilities in these services will be attacked with exploits that in many cases result in a complete compromise of the system. Unnecessary services should not be run on application servers because these exposures must be kept up to date with vendor-issued patches.

## Member Servers

Member servers (workstations, test systems, backup servers, and so on) are usually tertiary targets of an attack against a domain. Common targets of this type are

![](img/729efc56f204a2ebffb8295c3a2dfdfb_99_0.png)

workstations of administrators, supervisors, and executives. Accounts should not exist on these systems that would allow an attacker to gain domain-level access via password reuse. An attacker who compromises a member server will have full access to all data on the system (personal and corporate) and may have access to systems administered from this system. Be sure to never run services in the context of domain accounts (especially Domain Admins).

# The Simple (But Effective) Windows HSV Attack

The domain for this is InternalNetworkSFU. The first step is to find one or more systems in the domain with the very common blank administrator password. This vulnerability is listed as "General Windows Authentication – Accounts with No Passwords or Weak Passwords" in the SANS/FBI Top 20. I wrote this script to help out the process of finding these accounts in a Windows domain:

```
@echo off
REM HSVAdmin.bat -- simple HSV script for Windows Domains created for
Special Ops book
REM e.p. birkhholz

REM syntax: HSVAdmin.bat DOMAIN
REM HSVAdmin requires these applications: NetView.exe, ipc$crack.exe

if [%1]==" goto :FAILURE
echo.Blank && echo.>Blank
netview -d%1 -Tnt -Onv %1_hosts.txt
for /P "delims=,tokens=1" %i in (%1_hosts.txt) do (
set e%%%i
echo >> %1_HostsAlreadyChecked.txt
echo ...testing %e%%...
call :BLANKCHECK
)
del %1_hosts.txt
del %1_HostsAlreadyChecked.txt
del Blank
goto :EOF

:BLANKCHECK
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_100_0.png)
