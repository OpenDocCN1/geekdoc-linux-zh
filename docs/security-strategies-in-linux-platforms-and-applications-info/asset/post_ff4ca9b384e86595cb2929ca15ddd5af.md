
One issue related to the OpenOffice.org suite is updates. When updates are required, they can be substantial, easily involving the transfer of hundreds of megabytes of data to each Linux desktop system. For some networks, the cost of an Internet connection depends on the bandwidth. A local repository as described in Chapter 11 can help minimize the bandwidth required from OpenOffice.org downloads. It can also help you retain configuration control. For example, if your data has not yet been tested with OpenOffice.org version 3.x, a local repository can help you limit the choice available to your users.

## E-mail

Linux includes as many options for e-mail clients as it does for browsers. Some just de-mail, others are more fully featured personal information managers (PIMs). For example, with the right plug-in, the Evolution groupware can work as a client to Microsoft Exchange servers. (Of course, Linux includes its own PIM server equivalent, known as Novell Groove. But that's a server application.)

More straightforward e-mail clients include the following:

- Mozilla Thunderbird—A secure e-mail client and Really Simple Syndication (RSS) feed reader. Thunderbird's companion to the Firefox Web browser.
- Balsa—An e-mail client for the GNOME desktop environment, without the groupware features (or overhead) associated with Evolution.
- Kmail—An e-mail client for the KDE desktop environment.
- Sylpheed—A lightweight GUI e-mail client with excellent Japanese language support.

## Best Practices: Service Deployment

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

## CHAPTER 6 | Every Service Is a Potential Risk

The minimal installations of many distributions, including RHEL 5, include many more services than is desirable on a bastion host. Ideally, you should uninstall unneeded services. But that is not always realistic, as critical software may not work unless some services that appear to be unnecessary are also installed. But you can at least make sure unnecessary service is not active. Opinions vary on some software; for example Red Hat and the NSA have varying conclusions on some services.

When bastions are configured on a virtual machine, generally you should set up something other than a bridged network. A combination of NAT and port forwarding can be used to direct desired traffic to bastion servers.

In general, administrators will take care to remove development tools from every active system. If a black-hat hacker breaks into a system with development tools, then a black-hat hacker could use those tools to build more dangerous malware.

Other services are controlled through the regular and extended internet servers. Some services may be made more secure with the use of a chroot jail.

You should avoid the installation of a GUI where possible. Many users will require a GUI, however. Most Linux distributions have disabled the xauth and xhost commands because of security risks. If possible, you should also disable access via the XDMCP protocol.

Most Linux administrators work without a GUI. That is made possible courtesy of some important and sometimes useful tools. Surprisingly, the ssh service ensures remote administration. The telnet command with the right port number can be used to verify activity in a number of services. Other text tools.

When bastions are configured on a virtual machine, generally you should set up something other than a bridged network. A combination of NAT and port forwarding can be used to direct desired traffic to bastion servers.

In general, administrators will take care to remove development tools from every active system. If a black-hat hacker breaks into a system with development tools, then a black-hat hacker could use those tools to build more dangerous malware.

Other services are controlled through the regular and extended internet servers. Some services may be made more secure with the use of a chroot jail.

You should avoid the installation of a GUI where possible. Many users will require a GUI, however. Most Linux distributions have disabled the xauth and xhost commands because of security risks. If possible, you should also disable access via the XDMCP protocol.

Most Linux administrators work without a GUI. That is made possible courtesy of some important and sometimes useful tools. Surprisingly, the ssh service ensures remote administration. The telnet command with the right port number can be used to verify activity in a number of services. Other text tools.

## SUMMARY

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

## CHAPTER 6 | Every Service Is a Potential Risk

The minimal installations of many distributions, including RHEL 5, include many more services than is desirable on a bastion host. Ideally, you should uninstall unneeded services. But that is not always realistic, as critical software may not work unless some services that appear to be unnecessary are also installed. But you can at least make sure unnecessary service is not active. Opinions vary on some software; for example Red Hat and the NSA have varying conclusions on some services.

When bastions are configured on a virtual machine, generally you should set up something other than a bridged network. A combination of NAT and port forwarding can be used to direct desired traffic to bastion servers.

In general, administrators will take care to remove development tools from every active system. If a black-hat hacker breaks into a system with development tools, then a black-hat hacker could use those tools to build more dangerous malware.

Other services are controlled through the regular and extended internet servers. Some services may be made more secure with the use of a chroot jail.

You should avoid the installation of a GUI where possible. Many users will require a GUI, however. Most Linux distributions have disabled the xauth and xhost commands because of security risks. If possible, you should also disable access via the XDMCP protocol.

Most Linux administrators work without a GUI. That is made possible courtesy of some important and sometimes useful tools. Surprisingly, the ssh service ensures remote administration. The telnet command with the right port number can be used to verify activity in a number of services. Other text tools.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

## KEYCEPTS AND TERMS

| Term | Description |
| :--- | :--- |
| apt-cache | A tool for retrieving and caching packages. |
| chroot | Changes the root directory. |
| DMZ | Demilitarized Zone. |
| GCC | GNU Compiler Collection. |
| DHCP | Dynamic Host Configuration Protocol. |
| GUI | Graphical User Interface. |
| NFS | Network File System. |
| PID | Process ID |
| RHEL | Red Hat Enterprise Linux. |
| SSH | Secure Shell. |
| Tarball | An archive file. |
| Upstart | Init system. |
| XDMCP | X Desktop Management Control Protocol. |
| yum | Package manager. |

## ASSESSMENT

1. What part of the network is best?
- A DMZ
- B protected network
- C virtual machines
- D Internet network

2. Which of the following directories contain scripts?
- A /etc/default/
- B /etc/sysconfig/
- C /etc/xinetd/
- D /etc/init.d/

3. Which of the following commands lists installed packages?
- A rpm -qi
- B rpm -qa
- C rpm -qf
- D rpm -ql

## CHAPTER 6 | Every Service Is a Potential Risk 

The minimal installations of many distributions, including RHEL 5, include many more services than is desirable on a bastion host. Ideally, you should uninstall unneeded services. But that is not always realistic, as critical software may not work unless some services that appear to be unnecessary are also installed. But you can at least make sure unnecessary service is not active. Opinions vary on some software; for example Red Hat and the NSA have varying conclusions on some services.

When bastions are configured on a virtual machine, generally you should set up something other than a bridged network. A combination of NAT and port forwarding can be used to direct desired traffic to bastion servers.

In general, administrators will take care to remove development tools from every active system. If a black-hat hacker breaks into a system with development tools, then a black-hat hacker could use those tools to build more dangerous malware.

Other services are controlled through the regular and extended internet servers. Some services may be made more secure with the use of a chroot jail.

You should avoid the installation of a GUI where possible. Many users will require a GUI, however. Most Linux distributions have disabled the xauth and xhost commands because of security risks. If possible, you should also disable access via the XDMCP protocol.

Most Linux administrators work without a GUI. That is made possible courtesy of some important and sometimes useful tools. Surprisingly, the ssh service ensures remote administration. The telnet command with the right port number can be used to verify activity in a number of services. Other text tools.

## SUMMARY

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as possible on any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.

Every service is a potential risk. For this reason, it's best to configure as few services as any system.

The ideal bastion server is configured with a single purpose in mind. It'll have two open ports: for the purpose of the server, one for the SSH connection to administer over. Bastions are more practical to configure today, given the availability of virtual machines. Fortunately, Linux in a virtual machine does not require a lot of resources. In fact, you do not need to include all standard physical hardware in a virtual machine.

Generally, bastions should be configured in the DMZ portion of a network. While the DMZ is protected in part from an outside network such as the Internet, it is not as well protected from the remainder of the private network. Bastions are typically configured from a minimal installation of Linux. This chapter examined how you can create such minimal installation for both RHEL and Ubuntu Server Edition.
