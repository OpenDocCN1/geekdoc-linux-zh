# OffSec Penetration Testing with Kali Linux

Canvas,725 made by Immunity, is another exploit framework. Once the product is paid for, exploits are regularly updated every.

The Browser Exploitation Framework (BeEF)726 is a penetration testing tool focused on client-side attacks executed within a web browser.

We covered some popular frameworks for penetration testing. Although we briefly detailed each one, it is valuable to know the resources available in exploit frameworks.

# 15.3.2 SearchSploit

The Exploit Database provides a downloadable archived copy of all the hosted exploit code. This archive is included by default in Kali in the exploitdb package. We recommend updating the package before any assessment to ensure the latest exploits are installed. The package can be updated using the following commands:

```
kali@kali:~$ sudo apt update && sudo apt install exploitdb
[sudo] password for kali:
```

The following packages will be upgraded:
exploitdb

```
Setting up exploitdb (20220526-kali1) ...
```

> Listing 353 - Updating the Exploit Database archive from the Kali repositories

The above command updates the copy of the Exploit Database archive under /usr/share/exploitdb/. This directory splits into two sections, exploits and shellcodes. The /usr/share/exploitdb/ directory contains CSV files for each of the exploits and shellcodes directories. Each CSV file contains information of all files within their respective subdirectories. These CSV files contain similar information to the Exploit DB website, such as the EDB-ID, title, author, platform, and other information we covered previously.

```
kali@kali:~$ ls -1 /usr/share/exploitdb/
exploits
files.csv
files_shellcodes.csv
shellcodes
```

> Listing 354 - Listing the two major sections in the main directory with the database reference files

When we redirect to the exploits directory, we will find many subdirectories containing all of the exploits. These sub-directories are separated based on operating system, architecture, scripting language. For example, the linux subdirectory contains all Linux-related exploits.

```
kali@kali:~$ ls -1 /usr/share/exploitdb/exploits
ix
alpha
android
arm
ashx
```

725 (Immunity, 2022), http://immunityinc.com/products/canvas/index.html
726 (BeEF, 2022), http://beefproject.com

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.