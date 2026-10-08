**Post-Exploitation Capabilities Once we are inside the system, our capabilities will depend, in part, upon several factors. These factors include the following:**
1. Do we have system admin privileges?

2. What payload did we place inside the system?

3. What service or application did we exploit?

In Chapter 9, we exploited the SMB service on the Windows 7 system. We were able to get the system administrator privileges and placed the windows/meterpreter/reverse_http payload inside the system.

**Search for Post-Exploitation Modules When using Metasploit for postexploitation, we have numerous options. We can view all the post-**
expliotation modules in Metasploit by using the search command and entering: `msf5 > search type:post` As you can see, there are over 300 post-exploitation modules.

We can narrow this search by just looking for those that can be used on Windows systems (in our case, we will be using a Windows 7 system).

`msf5 > search type:post platform:windows 198 | P a g e`

```
```text
msf5 > search type:post platform:windows
Matching Modules

#   Name                                          Disclosure  Date  Rank    Check  Description
-   ----                                          ----------  ----  ----    -----  -----------
    post/multi/gather/apple_iap_backup                            normal  No     Windows Gather- Apple iOS MobileSync Backup File Collection
    post/multi/gather/checkMalware                              normal  No     Multi Gather Malware verify!
    post/multi/gather/chrome_cookies                            normal  No     Chrome Gather Cookies
    post/multi/gather/dkim_enum                                 normal  No     Multi Gather DNSImailer Connections Settings
    post/multi/gather/dns_bruteforce                            normal  No     Multi Gather DNS Forward Lookup BruteForce
    post/multi/gather/dns_reverse_lookup                        normal  No     Multi Gather DNS Reverse Lookup Scan
    post/multi/gather/dns_srv_lookup                            normal  No     Multi Gather DNS Service Record Lookup Scan
    post/multi/gather/env                                       normal  No     Multi Gather VirtuaBox VM Enumeration
    post/multi/gather/ftp                                         normal  No     Multi Gather Generic Operating System Environment Settings
    post/multi/gather/filezilla_client_cred                     normal  No     Multi Gather FileZilla FTP Client Credential Collection
    post/multi/gather/ireda_web                                 normal  No     Multi Gather Ireda Web Identification
    post/multi/gather/jenkins_cred                              normal  No     Multi Gather PireFox Client Credential Collection
    post/multi/gather/jboss_gather                              normal  No     JBoss Credential Collector
    post/multi/gather/ldap_gather                               normal  No     JeeJiis Credential Collector
    post/multi/gather/lanpass_vault_decrypter                   normal  No     LanPass Vault Decrypter
    post/multi/gather/maven_cred                                normal  No     Multi Gather Maven Credentials Collection
    post/multi/gather/multi_command                             normal  No     Multi Gather PIP Shell Common Resource File
    post/multi/gather/ppass_cred                                normal  No     Multi Gather Ppass Credentials
    post/multi/gather/pigp_cred                                 normal  No     Multi Gather Pigp Instant Messenger Credential Collection
    post/multi/gather/sip_sweep                                 normal  No     Multi Gather SIP Sweep
    post/multi/gather/ssh_sweep                                 normal  No     Multi Gather SSH Sweep
    post/multi/gather/virtualbox_guests                         normal  No     Multi Gather VirtualBox Guest Resource File
    post/multi/gather/run_console_rc_file                       normal  No     Multi Gather Run Console Resource File
```
```