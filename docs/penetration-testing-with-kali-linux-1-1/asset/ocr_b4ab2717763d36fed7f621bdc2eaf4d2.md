![](bbox=[0.1, 0.04, 0.26, 0.1])



written in Lua $ ^{236} $ and range in functionality from brute force and authentication to detecting and exploiting vulnerabilities. For these purposes we will focus on the scripts in the "vuln" and "exploit" categories, as the former detects a vulnerability and the latter attempts to exploit it.

However, there is overlap between these categories and some "vuln" scripts may essentially run stripped-down exploits. For this reason, scripts are also further categorized as "safe" or "intrusive" and we should take great care when executing the latter because they may crash a remote service or take down the target.

> **_Never run NSE scripts blindly. Take time to inspect them to understand what they do before running them, and test on your own targets whenever possible._**

On Kali, the NSE scripts can be found in the /usr/share/nmap/scripts/ directory. Opening any of the *.nse files in a text editor shows the source of each script in a simple human-readable format. Take time to review some of the NSE scripts to get familiar with the format and the types of checks these scripts perform.

This folder also contains a **script.db** file that serves as an index to all of the scripts. It also categorizes each of the Nmap scripts. We could, for example, use the file to **grep** for scripts in the "vuln" and "exploit" categories, as shown in Listing 278:

```
kali@kali:~$ cd /usr/share/nmap/scripts/

kali@kali:/usr/share/nmap/scripts$ head -n 5 script.db
Entry { filename = "acarsd-info.nse", categories = { "discovery", "safe", } }
Entry { filename = "address-info.nse", categories = { "default", "safe", } }
Entry { filename = "afp-brute.nse", categories = { "brute", "intrusive", } }
Entry { filename = "afp-ls.nse", categories = { "discovery", "safe", } }
Entry { filename = "afp-path-vuln.nse", categories = { "exploit", "intrusive", "vuln", }

kali@kali:/usr/share/nmap/scripts$ cat script.db | grep "vuln"\|"exploit""
Entry { filename = "afp-path-vuln.nse", categories = { "exploit", "intrusive", "vuln", }
Entry { filename = "clamav-exec.nse", categories = { "exploit", "vuln", } }
Entry { filename = "discc-ccve2004-2687.nse", categories = { "exploit", "intrusive", }
Entry { filename = "ftp-proftpd-backdoor.nse", categories = { "exploit", "intrusive", }
Entry { filename = "ftp-vsftpd-backdoor.nse", categories = { "exploit", "intrusive", "
..."
```

*Listing 278 - The Nmap script database*

Let’s try to use the NSE to detect a vulnerability. For this example, we will use --**script** **vuln** to run all scripts in the \`vuln\` category against a target in the PWK labs:

```
kali@kali:~$ sudo nmap --script vuln 10.11.1.10
[sudo] password for kali:
Starting Nmap 7.70 ( https://nmap.org )
Pre-scan script results:
| broadcast-avahi-dos:
|   Discovered hosts:
```

$ ^{236} $ (Nmap, 2019). https://nmap.org/book/nse-language.html