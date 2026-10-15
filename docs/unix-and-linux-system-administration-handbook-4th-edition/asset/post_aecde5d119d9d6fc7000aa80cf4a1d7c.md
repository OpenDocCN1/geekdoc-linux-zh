
## 11.7 EXERCISES

E11.1 What are the main reasons for keeping old log files?

E11.2 What is the difference between lastlog and wtmp? What is a reasonable rotation policy for each?

E11.3 Dissect and understand the following syslog.conf line:

```
*.notice;kern.debug;lpr.info;mail.crit;news.err /var/log/messages
```

Does it seem sensible?

E11.4 Look through your log files for entries from the SSH service. What events are logged when a login attempt is successful? What if a login attempt fails? What steps would you take to increase the logging verbosity of the SSH daemon?

E11.5 Many IT industry standards and regulations impose logging or auditing requirements. Choose one of these standards and discuss how you might tune a syslog configuration to achieve compliance.

★ E11.6 Where would you find the boot log for your Linux machine? What issues affect logging at boot time? How does klogd solve these issues?

★ E11.7 Investigate the logging policy in use at your site, including the log file rotation policy. How much disk space is dedicated to logging? How long are log files kept? Can you foresee circumstances in which your site's policy would not be adequate? What solution would you recommend? (Requires root access.)

★ E11.8 Some log messages are extremely important and should be reviewed by an administrator immediately. What system could you set up to make sure that this happens as quickly as possible?

## 12.1 INSTALLING LINUX AND OPENSOLARIS

Current Linux distributions all have straightforward procedures for basic installation. OpenSolaris has adopted many of the same conventions, so its installation process is similar, especially on PC hardware.

Installation typically involves booting from a DVD, answering a few basic questions, optionally configuring disk partitions, and then telling the installer which software packages to install. Some systems, such as Ubuntu and OpenSolaris, include a "live" option on the installation media that lets you run the operating system without actually installing it on a local disk. This used to be a big deal, but these days it's becoming a standard feature of most distributions.

Installing the base operating system from local media is fairly trivial thanks to the GUI applications that shepherd you through the process. Table 12.1 lists pointers to detailed installation instructions for each of our example distributions.

### Table 12.1 Installation documentation for Linux and OpenSolaris

| Distribution | Documentation source |
|---|---|
| Red Hat Enterprise Linux | redhat.com/docs/manuals/enterprise |
| SUSE | en.opensuse.org/Installation |
| Ubuntu | help.ubuntu.com/community/Installation |
| OpenSolaris | dlc.sun.com/osol/docs/content/dev/getstart |

### Netbooting PCs

If you have to install the operating system on more than one computer, you will quickly reach the limits of interactive installation. It's time consuming, error prone, and boring to repeat the standard installation process on hundreds of systems. You can minimize human errors by using a localization checklist, but even this measure does not remove all potential sources of variation.

To alleviate some of these problems, most systems include network installation options that simplify large-scale deployments. The most common methods use DHCP and TFTP to boot the system sans physical media, then retrieve the installation files from a network server through HTTP, NFS, or FTP. Network installations are appropriate for sites with more than ten or so systems.

The Preboot eXecution Environment, also known as PXE, is a standard from Intel that allows systems to boot from a network interface. PXE acts like a miniature OS sitting in a ROM on your network card. It exposes its network capabilities through a standardized API for the system BIOS to use. This cooperation makes it possible for a single boot loader to netboot any PXE-enabled PC without the need to supply special drivers for each network card.
