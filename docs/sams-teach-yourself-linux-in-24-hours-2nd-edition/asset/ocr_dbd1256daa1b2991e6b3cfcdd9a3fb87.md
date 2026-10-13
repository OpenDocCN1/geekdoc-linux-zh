# Information You Need from Your ISP

In order to connect to the Internet using PPP through your ISP, you need to first, obviously, have a PPP account. When you sign up for your service, your ISP account representative most likely assumes you want a setup and software for either a Windows or Macintosh computer system. If you say “Neither. I’m using Caldera’s OpenLinux,” and the response you get is either a blank stare, dead air on the phone, or “What’s Linux?” don’t panic!

You might get lucky. Linux is growing in popularity, and many ISPs in the U.S. and around the world recognize and support Linux users. If your ISP is aware of Linux, ask for the minimum system requirements, any setup guides, or install tips. This book’s CD-ROM contains the latest, stable releases of the software you need, so you don’t have to worry anyway.

Assuming your ISP doesn’t know about Linux, here’s what you need from your ISP:

+   - Your account information, meaning your username (login name) and password, so you can log in to your ISP’s computer.
+   - Your ISP’s modem connect number(s), so you can dial out and connect.
+   - Whether your ISP assigns you a static Internet Protocol (IP) address or assigns your IP address dynamically (the examples in this hour assume dynamic addresses, but I show you where you can make changes for a static IP address).
+   - The IP addresses and names of your ISP’s primary Domain Name Server and secondary Domain Name Server. This information goes into the /etc/resolv.conf file (as explained in this chapter’s section “Editing the resolv.conf File”) in the first example.

![](bbox=[0.22, 0.8, 0.3, 0.88])

The DNS IP addresses are in the form of four 8-bit numbers, and look something like 205.198.114.1 or 205.198.114.20. These are the address or addresses of the servers used or maintained by your ISP that translate hostnames, such as metalab.unc.edu, into numeric IP addresses, so you can connect, query, or address other computers and users around the world. This section doesn’t go into the details about the mechanics of IP addressing, and this book does not cover all aspects of networking under Linux. If you want more complete details, see the Linux Network Administrators Guide under the /usr/doc/LDP/nag directory.