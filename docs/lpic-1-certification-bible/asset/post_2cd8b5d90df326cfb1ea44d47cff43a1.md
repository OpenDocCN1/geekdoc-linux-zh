
4. `i`
5. Three
6. `export`
7. `PS2`
8. `read`
9. `#!/command/interpreter`
10. `set` and `shopt`

# Assessment Questions

1. **A.** Answer B is invalid. The `/etc/profile` is read whenever a user logs in, and they do not have a custom `profile` file. The `.cshrc` is not used by the bash shell. For more information, see the “Special files” section.
2. **read** `$NAME`. The `read` command takes input from a user and places it in to variables. The `.cshrc` is not used by the bash shell. For more information, see the “Reading user input” section.
3. **D.** The `a` command appends text, and can also insert text to the right of the cursor. The other answers are invalid. For more information, see the “Using vi” section.
4. **A.** The `cdspell` shell option can fix some spelling mistakes when changing directories. The other answers are invalid. For more information, see the “Options” section.
5. `chmod` `u+x` `sortdoc`. You must set the script as executable before a user can run it. For more information, see the “Writing a basic script” section.
6. `dd`. For more information, see the “Deleting lines” section.
7. **D.** The double quotes around the variable cause it to be translated to its value. The forward ticks are displayed literally. Remember that back ticks (`) are used for command substitution. For more information, see the “Quoting variables” section.
8. **B.** The `HISTCMD` variable holds the command number for the current command. All of the other answers are invalid. For more information, see the “Built-in variables” section.
9. **D.** The other answers are invalid. For more information, see the “Prompt variables” section.
10. **A.** The `cd` command will go through each directory in the `CDPATH` variable, and change to the first correct one found. For more information, see the “Search paths” section.
11. `.bash_logout`. This file is executed each time a user logs out. For more information, see the "Special files" section.
12. **B.** By enabling this option, you can prevent accidentally overwriting a file when redirecting text. For more information, see the "Options" section.
13. **D.** Remember that `-o` enables an option, while `+o` disables the option. For more information, see the "Options" section.
14. `#!/bin/bash`. This line specifies the command interpreter to use for the script. For more information, see the "Starting a shell script" section.
15. **A.** The `-n` test checks to see if a string is non-zero in length. The `-s` parameter tests to see if a file exists and has a size greater than 0. There is no `-o` test. For more information, see the "Testing conditions" section.
16. **A.** The `case` clause matches patterns, while the other clauses test expressions for true or false. For more information, see the "Flow control" section.
17. **C.** The command must start with a `$` symbol, and the buffer name is case sensitive. For more information, see the "Yanking and pasting text" section.
18. **A.** The period matches any single character. The `*` will match multiple characters. The other answers are invalid. For more information, see the "Testing conditions" section.
19. **B.** For more information see the "Searching text" section.
20. **D.** The `MAILCHECK` variable defines how often to check for new mail in seconds. The `MAIL` variable stores the filename to check for new mail. For more information, see the "Mail variables" section.

# Scenarios

1. Set the `MAILPATH` variable with a colon-separated list of the files where mail is stored.
2. You should set the `noclobber` option with `set -o noclobber` in the user's `.bash_login`.
3. An example would be the following:

```bash
#!/bin/bash
#  Simple script to add users.
#

echo "Enter a userid to be added:"
read NEWUSER
echo "Adding a new user..."
adduser $NEWUSER
echo "Enter a new password when prompted..."
passwd $NEWUSER
```

4. An example would be the following:

```bash
#!/bin/bash
# Simple script to move files based on extensions.
#
case $filename in
    *.doc )
        mv $1 ~/doc
    ;;
    *.pdf )
        mv $1 ~/pdf
    ;;
    *.txt )
        mv $1 ~/txt
    ;;
    *.ps )
        mv $1 ~/ps
    ;;
esac
```

# Managing the Network

The final part of the book covers managing the network. In this section you are introduced to networking on a Linux system and provided with detailed information on the various networking servers and their configuration. Chapter 15 provides an introduction to networking including configuration of network adapters and basic tools used on a network. Chapter 16 then expands on this by covering the various network services include Web, mail, FTP, and DNS services. Chapter 17 concludes this part with information on securing a networked Linux system.

# PART IV

# In This Part

- **Chapter 15** Networking Fundamentals
- **Chapter 16** Managing Network Services
- **Chapter 17** Managing Security

# Networking Fundamentals

## EXAM OBJECTIVES

**Exam 102 General Linux, Part 2**

- **1.12** Networking Fundamentals
    - **Fundamentals of TCP/IP.** Demonstrate an understanding of network masks and what they mean (i.e. determine a network address for a host based on its subnet mask), understand basic TCP/IP protocols (TCP, UDP, ICMP) and also PPP, demonstrate an understanding of the purpose and use of the more common ports found in `/etc/services` (20, 21, 23, 25, 53, 80, 110, 119, 139, 143, 161), demonstrate a correct understanding of the function and application of a default route. Execute basic TCP/IP tasks: FTP, anonymous FTP, telnet, host, ping, dig, traceroute, whois.

### EXAM OBJECTIVES (CONTINUED)

- **TCP/IP Troubleshooting & Configuration.** Demonstrate an understanding of the techniques required to list, configure and verify the operational status of network interfaces, change, view or configure the routing table, check the existing route table, correct an improperly set default route, manually add/start/stop/restart/delete/reconfigure network interfaces, and configure Linux as a DHCP client and a TCP/IP host and debug associated problems. May involve reviewing or configuring the following files or directories: `/etc/HOSTNAME` | `/etc/hostname`, `/etc/hosts`, `/etc/networks`, `/etc/host.conf`, `/etc/resolv.conf`, and other network configuration files for your distribution. May involve the use of the following commands and programs: `dhcpd`, `host`, `hostname` (`domainname`, `dnsdomainname`), `ifconfig`, `netstat`, `ping`, `route`, `traceroute`, the network scripts run during system initialization.
- **Configure and use PPP.** Define the chat sequence to connect (given a login example), setup commands to be run automatically when a PPP connection is made, initiate or terminate a PPP connection, initiate or terminate an ISDN connection, set PPP to automatically reconnect if disconnected.

## CHAPTER PRE-TEST

1. What is **each host** on the Internet uniquely known by?
2. Which protocol in the TCP/IP suite handles error reporting?
3. What service uses port 139?
4. Which application provides terminal emulation?
5. Which file is used to manually map names to IP addresses?
6. Which tool allows you to view the path a packet takes through a network?
7. What method is used to automatically configure a workstation's IP information?
8. Which tool is used to assign an IP address to a network card?
9. What type of file is used to supply the user name and password when making a PPP connection?
10. Which option is used to automatically initiate the reconnection of a PPP connection that has been terminated?

> ◆ Answers to these questions can be found at the end of the chapter. ◆

**N**etworking is a fundamental part of Linux, as it is with most other UNIX-derived operating systems. This is the major reason that Linux works so well as an Internet server. This chapter covers how to configure and troubleshoot the networking features in Linux. Special attention will be paid to the sometimes overwhelming number of configuration files and the excellent tools available to track down problems. Finally, we cover how to get a Linux system on the Internet via a PPP connection.

## The TCP/IP Protocol Suite

**Objective**

**1.12 Networking Fundamentals**

- **Fundamentals of TCP/IP.** Demonstrate an understanding of network masks and what they mean (i.e. determine a network address for a host based on its subnet mask), understand basic TCP/IP protocols (TCP, UDP, ICMP) and also PPP, demonstrate an understanding of the purpose and use of the more common ports found in `/etc/services` (20, 21, 23, 25, 53, 80, 110, 119, 139, 143, 161), demonstrate a correct understanding of the function and application of a default route. Execute basic TCP/IP tasks: FTP, anonymous FTP, telnet, host, ping, dig, traceroute, whois.

UNIX and TCP/IP have grown up and evolved together over many years. Where once the world was filled with a network protocol for every network vendor, it is now settling on one large suite, TCP/IP. TCP/IP survives because of how well it adapts and because of its scalability, which lets it work on both tiny networks and the enormous Internet.

### Addresses

Every device on a TCP/IP network is known as a *host*. Each host must have a way to be uniquely identified, and that way is by IP address. Computers are connected to the network using network interface adapters. A computer can have multiple network adapters, and each one connected to the network must have at least one IP address.

IP addresses are 32-bit numbers that are usually written as four octets (8 bits) separated by periods. For example, your server may have the IP address of 192.168.100.100. It could also be known by its 32-bit number of 3232261220, and in fact, some TCP/IP applications can take input in this form (http://3232261220). To see how these numbers relate, you need to change the IP address to binary:

```
192 = 1100 0000
168 = 1010 1000
100 = 0110 0100
100 = 0110 0100
```
