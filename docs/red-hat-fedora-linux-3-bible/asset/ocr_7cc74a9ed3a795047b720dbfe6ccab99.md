# Appendix C

# Running Network Services

Because Fedora can provide so many different kinds of services (serving Web pages, printers, files, and other resources), it’s easy to lose track of them. Let’s say you install all server software packages with Fedora. How do you know which servers will start up automatically and which will need special configuration to work? Where do you start to look for configuration files, start-up scripts, and daemon processes? How do you know if your firewall configuration is blocking access to the services?

This appendix provides a quick reference to the network services that come with Fedora. It offers an overview of the services described in detail in other chapters. You can use this appendix to help you remember how to get services working or as a guide to help you debug a service that needs fixing.

> **CAUTION:** Any services your computer offers to users who can reach it over a network pose a potential security threat. Refer to Chapter 14 for information on security, as well as the sections in the book that describe configuration of each feature in detail.

# Checklist for Running Networking Services

As computer security issues increase with the rising onslaught of computer crackers and viruses, operating systems (such as Fedora or Red Hat Linux) are moving toward more security rather than more ease-of-use. Simply installing server software isn’t enough to get the service up and running.

If a service isn’t working, check the following items to hunt down the problem:

+   1. **Is the software package(s) installed?** Each network service is represented by one or more software packages. Use the command `rpm -qc _packagename` to find configuration files, and the command `rpm -qd _packagename` to find documentation. If you did a personal desktop or workstation install, most network server software may not be installed on your computer at all. Check Table C-1 to see which package(s) is needed for a service to work. (There might be other package dependencies as well, to which you will be alerted when you try to install the package.) Then use the `rpm` command to install the software from the installation DVD.