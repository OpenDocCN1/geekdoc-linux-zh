# OffSec

Instead of WPScan vulnerability database, let's use searchploit to find possible exploits for vulnerabilities in the installed plugins. For a majority of the identified plugins, WPScan provided us the detected versions. Because most of the plugins are up to date and no version could be detected for asterisk, let's start with Duplicator.

```
kali@kali:~/beyond$ searchploit duplicator

Exploit Title
| Path

WordPress Plugin Duplicator - Cross-Site Scripting
| /php/webpages/38676.txt
WordPress Plugin Duplicator 0.5.14 - SQL Injection / Cross-Site Request Forgery
| /php/webpages/36735.txt
WordPress Plugin Duplicator 0.5.8 - Privilege Escalation
| /php/webpages/36112.txt
WordPress Plugin Duplicator 1.2.32 - Cross-Site Scripting
| /php/webpages/44228.txt
WordPress Duplicator 1.3.26 - Unauthenticated Arbitrary File Read
| /php/webpages/50928.py
WordPress Duplicator 1.3.26 - Unauthenticated Arbitrary File Read (Metasploit)
| /php/webpages/49298.rb
WordPress Plugin Duplicator 1.4.6 - Unauthenticated Backup Download
| /php/webpages/50992.txt
Plugin Duplicator 1.4.7 - Information Disclosure
| /php/webpages/50993.txt
WordPress Plugin Multisite Post Duplicator 0.9.5.1 - Cross-Site Request Forgery
| /php/webpages/40908.html
```

Shellcodes: No Results Listing 872 - Searchploit results for the Duplicator WordPress plugin

The output shows that there are two exploits matching the version of the Duplicator plugin on WE1. One is tagged with Metasploit, indicating that this exploit was developed for The Metasploit Framework. We'll review this in the next Learning Unit.

Let's summarize what information we obtained about WEBSRV1 in this section. We learned that the target machine is an Ubuntu 22.04 with two open ports: 22 and 80. A WordPress instance runs on port 80 with active plugins. A plugin named Duplicator is outdated and a Searchploit query we provided with two vulnerability entries matching the version.

# 24.2 Attacking a Public Machine

This Learning Unit covers the following Learning Objectives:

+   - Use vulnerabilities in WordPress Plugins
- Crack the passphrase of an SSH private key
- Elevate privileges using sudo commands
- Leverage developer artifacts to obtain sensitive information