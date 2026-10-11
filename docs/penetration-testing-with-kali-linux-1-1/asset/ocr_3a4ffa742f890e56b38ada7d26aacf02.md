Listing 608 - SSH attack using Hydra

In this output, we can see that hydra discovered a valid login against the local SSH server.

THC-Hydra supports a number of standard protocols and services as shown in Listing 609:

```
kali@kali:~$ hydra
Hydra v8.8 (c) 2019 by van Hauser/THC - Please do not use in military or secret servic

Syntax: hydra [[[-L LOGIN|-L FILE] [-P PASS|-P FILE] | [-C FILE]] [-e nsr] [-o FILE]
[-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-W TIME] [-z] [-s PORT] [-x MIN:MAX:CHARSET
] [-c TIME] [-IS0uVd46] [service://server::PORT][/OPT]]
...
Supported services: adams6500 asterisk cisco cisco-enable cvs firebird ftp tftp http[s]
-[head|get|post] http[s]--[get|post] -form http-proxy http-proxy-urlenum icq imap[s] irc
ldapt[s] ldapt[s]-[cram|digest]md5[s] mssql mysql nntp oracle-listener oracle-sid pcany
where pcfw pop3[s] postgres radmin2 rdp redis rexec rlogin rproxy rsync s7-300 sip
smb smtp[s] smtp-enam snmp sock5 ssh sstkey svn teamspeak telnet[s] vmauthd vnc xnxp
...
```

Listing 609 - Supported modules by THC-Hydra

# 19.3.3.1 Exercise

+   (Reporting is not required for these exercises)
+   
+   1. Recreate the Hydra SSH attack against your Kali VM.

# 19.3.4 HTTP POST Attack with THC-Hydra

As an additional example, we will perform an HTTP POST attack against our Windows Apache server using Hydra. When a HTTP POST request is used for user login, it is most often through the use of a web form, which means we should use the "http-form-post" service module. We can supply the service name followed by -u to obtain additional information about the required arguments:

```
kali@kali:~$ hydra http-form-post -u

Help for module http-post-form:

Module http-post-form requires the page and the parameters for the web form.

By default this module is configured to follow a maximum of 5 redirecations in a row. It always gathers a new cookie from the same URL without variables
The parameters take three ":" separated values, plus optional values.
(Note: if you need a colon in the option string as value, escape it with "\\", but do

Syntax: <url>::<form parameters>[:<condition string>[:<optional>[:<optional>]
First is the page on the server to GET or POST to (URL).
Second is the POST/GET variables (taken from either the browser, proxy, etc,
with url-encoded (resp, base64-encoded) usernames and passwords being replaced in the
"^USERA^" (resp. "^USER64^") and "^PASSA^" (resp. "^PASS64^") placeholders (FORM PARAME
Third is the string that it checks for an ^invalid^ login (by default)
Invalid condition login check can be preceded by "F=^", successful condition
login check must be preceded by "S=".
This is where most people get it wrong. You have to check the webapp what a
failed string looks like and put it in this parameter!
```