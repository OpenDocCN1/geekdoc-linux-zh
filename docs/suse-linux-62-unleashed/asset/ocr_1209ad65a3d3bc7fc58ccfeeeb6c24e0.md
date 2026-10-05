# Networking and Internet Services
PART II

Connections from a SuSE system to an ISP are usually made through a modem using the new common PPP (Point-to-Point Protocol), or more infrequently, using SLIP (Serial Line Interface Protocol). Both PPP and SLIP allow you to transfer mail, surf the World Web, using FTP, and access all the other features of the Internet. Both PPP and SLIP use the TCP/IP network protocol, and because TCP/IP and UNIX evolved together, Linux is particularly adept at handling PPP and SLIP.

In this chapter, you learn how to easily set up your SuSE system to use PPP using manual scripts and the wdia1 PPP client. You will also learn one way to set up your Linux system for dial-in PPP. You will probably not want to use both PPP and SLIP because most ISPs use PPP only, and SLIP seems to be “slipping” into obscurity. PPP is the faster of the two protocols, but you may sometimes need to use SLIP with older systems or legacy software. Before setting up either PPP or SLIP, you will need to create a dummy interface so your machine knows about itself in a networking sense and because most protocols require this dummy interface to work properly.

# Setting Up the Dummy Interface

Fortunately, setting up a dummy interface is simple. All that is required is a couple of commands to create the interface and a couple more commands to test that the interface is working, and you're done. The file that Linux uses to store all network IP address information is called /etc/hosts, and every system should have one (even if it is empty).

The /etc/hosts file is an ASCII file that provides two pieces of information to the TCP/IP drivers and applications: an IP address and the names associated with that IP address. Usually, you will find the /etc/hosts file has a single line in it when you install Linux without network support:

```
127.0.0.1    localhost
```