# THE ESSENTIALS AND BEYOND (Continued)

# SUGGESTED EXERCISES

+   - On a small private network that you control or in a lab environment under the supervision of an instructor, reconfigure a computer that uses DHCP to use its assigned IP address in a static fashion. Test the connection and switch back to DHCP. Do not perform this test on a work or school network that's used for normal purposes; misconfiguration of a computer's IP address can cause problems for other computers.
- Back up your /etc/resolv.conf file, and then edit the original so that its nameserver points to computers that don't run DNS servers. Test your network configuration by attempting to access remote servers via ping, a web browser, and other utilities. Observe the types of failures that result. When you're done, restore the original file.

# REVIEW QUESTIONS

+   1. You want to set up a computer on a local network via a static TCP/IP configuration, but you lack a gateway address. Which of the following is true?
   A. Because the gateway address is necessary, no TCP/IP networking functions will work.
   B. TCP/IP networking will function, but you'll be unable to convert hostnames to IP addresses, and vice versa.
   C. You'll be able to communicate with machines on your local network segment but not with other systems.
   D. The computer will not be able to tell which other computers are local and which remote.
   E. You'll be able to use the computer as a network server system but not as a client.
2. Which of the following types of information are returned by typing ifconfig eth0? (Select all that apply).
   A. The names of programs that are using eth0
   B. The IP address assigned to eth0
   C. The hardware address of eth0
   D. The hostname associated with eth0
   E. The gateway with which eth0 communicates