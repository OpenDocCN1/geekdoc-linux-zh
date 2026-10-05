# # OffSec

Penetration Testing with Kali Linux

To improve its security, the user's password is stored in the authentication_string field as a Caching-SHA-256 algorithm.453

A password hash is a ciphered representation of the original plain-text password. In later Modules, we'll learn how password hashing is performed and how a hash can be reversed or cracked to obtain the original password.

Having covered the basics of MySQL, let's explore MSSQL. MSSQL454 is a database management system that natively integrates into the Windows ecosystem.

A built-in command-line tool SQLCMD455 allows SQL queries to be run through the Windows command prompt or even from another machine.

Kali Linux introduces Impacket,456 a Python framework that enables network protocol interactions. Among many other protocols, it supports Tabular Data Stream (TDS).457 the protocol adopted by MSSQL that is implemented in the impacket-mssqlclient

We can run impacket-mssqlclient to connect to the remote Windows machine running MSSQL by providing a username, password, and the remote IP, together with the -windows-auth keyword. This forces NTLM authentication (as opposed to Kerberos). We'll explore authentication in depth in upcoming Modules.

```
kalikal@i$: impacket-mssqlclient Administrator:Lab123@192.168.0.18 -windows-auth
Impacket v0.9.24 - Copyright 2021 SecureAuthCorp
[+] Encryption required, switching to TLS
[ENCHANGE(DATABASE)] Old Value; New Value: master
[ENCHANGE(LANGUAGE)] Old Value; New Value: us english
[ENCHANGE(PACKETSIZE)] Old Value: 4096; New Value: 16192
[INFO(SQL01SQPRESS)] Line 1: Changed database context to 'master'.
[INFO(SQL01SQPRESS)] Line 1: Changed language setting to us english.
[ACK] Result: 1 - Microsoft SQL Server (150 7208)
SQL>
```

Listing 184 - Connecting to the Remote MSSQL instance via Impacket

To begin, let's identify the current version of the underlying operating system by selecting the @@version.

> Every database management system has its own syntax that we should take into consideration when enumerating a target during a penetration test.

453 (Oracle, 2022), https://dev.microsoft.com/doc/refman/8.0/en/caching-sha-2-pluggable-authentication.html
454 (Microsoft, 2022), https://docs.microsoft.com/sqlserver
455 (Microsoft, 2022), https://docs.microsoft.com/en-us/tools/sqlcmd-utility
456 (SecureAuth, 2022), https://github.com/SecureAuthCorp/impacket
457 (Microsoft, 2022), https://docs.microsoft.com/en-us/windows/protocols/ms-tds/893fcc7e8-33a9-4b3c-815a-773b7b982c50/

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

289