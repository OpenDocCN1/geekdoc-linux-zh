# Chapter 9 • Attacking and Defending Microsoft Terminal Services

run. Only applications that are required by the TS users should be given access. If used properly, this tool can keep users locked into a specific environment as well as reduce the risk of privilege escalation if they find a way to break-out of it. This tool, however, only limits applications by their filenames. So if you allow explorer.exe to run, any file renamed to explorer.exe will work.

# Limit and Log Access from Older Clients

TSVer.exe is in the Windows 2000 Resource Kit and can be used to restrict older versions of Terminal Server clients from making connections. Additionally, this tool will record an IP as well as a hostname to the system logs when attempted connections fail due to older versions. TSVer should be used to force users to use the current RDC client due to its 128-bit encryption requirements.

# Case Study: Attacking Terminal Server

In this brief case study, I detail each successful step of my internal attack chronology from CorpLAN to FinanceLAN using Terminal Server as an integral part of the attack. The goal was to compromise the production MSSQL database in the FinanceLAN.

My first step was to attempt to enumerate the hosts in the FinanceLAN domain using the net view /domain:FinanceLAN command. I was unable to see any hosts because there was a screening router in the way. So my other option was to attack the CorpLAN to find a server that would allow me to jump into the FinanceLAN.

Using the HSVAdmin.bat script, I was able to discover 24 out of 252 hosts with blank administrator passwords in the CorpLAN domain. Using these credentials, I was able to execute commands interactively on these hosts using a tool called psexec.exe (www.internals.com/ntw2k/freeview/pstools.html).

```
NET USE \VICTIME\admin$ "" /u:VICTIME\administrator
Psexec cmd exe
```

This interactive access allowed me to enumerate and the hosts in the FinanceLAN domain using net view /domain. Next, I used a tool (sqllhf.exe) that checked for blank SA (database administrator) passwords and found a host that contained a blank SA password. Using the xp_cmdshell stored procedure, I was able to execute commands on the server and add myself as an administrator. I connected to the Terminal Server with my new account and began to pillage the server for data to further my attack.

![](bbox=[0.068, 0.945, 0.295, 0.968])