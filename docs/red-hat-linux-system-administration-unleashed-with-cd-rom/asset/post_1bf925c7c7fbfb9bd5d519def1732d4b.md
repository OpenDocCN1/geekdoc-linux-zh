
Centennial made the trade-off because of the sensitive nature of the data involved in the productivity suite. The application integrity of the productivity suite facility required the best security possible. This ensured that the data would not be compromised.

Centennial reduced administrative duties by defining groups of users as well as users themselves. By managing sets of users, the system administrator defined a group file for use with Apache. This eliminated defining individual access rights by placing users in a group definition.

## Network Authentication, Access, and User Administration with Samba

For authentication services and network management, Centennial needed to use smb protocol. Samba is an Open Source software package available for Linux that provides support for the protocols used by Windows 95/98 and Windows NT.

Samba allows Windows clients to access the file and print capabilities of the Linux system in a manner similar to how those clients would access a Windows NT server.

Choosing the Samba package included with Red Hat 6.0 allowed Centennial to save money. The District did not have to pay license fees based on users or seats to provide basic NT services. Advantages of using Samba include

- A stable and reliable solution. Samba running on Linux provided the District with the default services it would have deployed with Windows NT. Again, the Linux solution does not require user license fees.
- Less administrative time.

On Centennial’s main authentication server, the technical department installed the Samba and sambas rpms from Red Hat 6.0. Under version 2.05, Samba can act as a domain controller. In previous versions, Samba did not authenticate users as a domain controller. Red Hat improved Red Hat 6.0’s functionality by adding this application to Red Hat 6.0.

## Samba in Centennial’s Heterogeneous Environment

The developers of Samba created a set of programs that allows UNIX and UNIX-like operating systems like Linux to communicate with Microsoft hosts. Microsoft uses a protocol known as NetBEUI, which implements server message blocks for network communication. Since many of Centennial’s workstations ran Windows 95/98, implementing Samba became necessary in order to use Linux.

## Training the Centennial Team

To provide an example of how Bynari coached the Centennial team, we’ll use the Samba configuration to demonstrate Bynari’s methodology. Mike Caron explains:

> > We began the samba install initially without setting up the server as an NT domain server. We learned how to create Linux users, and how to make samba users from existing Linux users. We then edited the /etc/hosts file to include the ip numbers of our samba client boxes. This was done because we were not ready to implement DNS services in our test lan. The smb.conf was then edited to set up disk shares.

> > The following steps are a general guideline we used for installing Samba and creating an NT Domain on a Linux Server.

- The very first step is to download the most current stable RPM for Samba and then install it. `rpm -Uvh <rpm name>` (The "U" is for "upgrade")
- Next create a public directory, and use chmod to give all users full access.
- We mkdir /home/pub and then chmod /home/pub 777.
- We edited /etc/hosts and created a public share for the /home/pub directory.
- We copied a template smb.conf file to the /etc directory and edited it to the specific server, domain name and any other specific settings.
- Now run linuxconf to edit some specific network settings for the server.
- Select Browse Master=yes, Local Master=yes, os level=65 (Later Domain Master=yes, os level=255)
- Select Synchronize Linux from SMB passwords (yes)
- Create Linux user, adduser if necessary and then create the Samba user smbadduser for any users that want access to this samba server.

> "Now configure the Windows workstation. Change Network Neighborhood properties to the following:"

- Identification Tab to the new workgroup (csd28)
- Access Control to Share level access control
- Client for Microsoft Networks properties to new workgroup (csd28)
- TCP/IP properties
  - IP Number: 192.168.3.10 (Initially, any static number)
  - DNS Configuration:
    - Domain: mtc.net
    - Host:
    - DNS Search Order: Initially Disabled Later added 192.168.3.15 (MTC proxy server, it was the ESD server)
    - Gateway: 198.236.3.1
- Turn on File & print sharing
- Add to the end of the c:/Windows/LM Hosts file 192.168.3.15 CSD28 (ip & workgroup)
- Reboot"

The Bynari approach uses gradients to teach the administrators how to configure any service. In the beginning of the samba process, the Centennial team only performed one function. They created a user called "guest" and added the user to both the Linux password file and the smbpasswd file. They also configured a Windows 98 system to log on to the Samba server. They added the Windows information to the Linux "hosts" file and made entries to the smb.conf.

Once the team experienced success with a simple guest share, they added functionality until the test LAN had domain authentication, Dynamic Host Configuration Protocol (DHCP), mail, and the ability to browse the Internet through a Linux firewall.

## Back to Samba

Samba 2.0 introduced a program to assist in setting up and administering Samba via a Web browser. People know the program as SWAT, for Samba Web Administration Tool. With Centennial's scarce resources, the technical department needed a simple way to provide administration for Microsoft workstations. Red Hat 6.0 provides SWAT on its distribution.

To enable SWAT in Red Hat 6.0, the technology department used the “inetd” method, which doesn’t require a Web server. Under this method, the various components of Samba can be configured and maintained via a Web browser. Though Red Hat 6.0 provides Samba and SWAT, the system administrator must configure it.

The Samba Web Administration Tool provided considerable challenges to the relatively new Linux network managers. When installing Samba 2.05, the installation program automatically puts an entry in the system’s inetd.conf file.

When configuring Samba, the administrator must open the configuration file and remove the comment symbol (#) in front of the SWAT entry in this file. Removing the comment allows Samba to be called during the system initiation process.

Next, the administrator must enter swat as a service in the system services file. The name of this file is simply services and it lives in the /etc directory. Using a text editor, the administrator opens the files and locates a section where the port numbers allow for a “900” series entry. The entry that SWAT requires in this configuration file is swat 901/tcp #swat.

Once the entry is made, the administrators must restart the services for the changes to take effect. By using the command /etc/rc.d/inet.d/inetd restart the system enables SWAT for use. On execution of this command at the root user’s command-line prompt, he or she will see a series of entries similar to those seen on booting the computer. Then the administrator can open his Web browser and access the SWAT interface.

The administrators typed http://localhost:901 and the SWAT interface opened in the browser. A sense of astonishment usually accompanies the first sight of the SWAT interface and in Centennial’s case, this occurred.

Suddenly, light could be seen at the end of the proverbial tunnel. The small group consisting of Dave and his team became even more intrigued with the remote administration possibilities when they went to a workstation in another room and accessed SWAT from a remote browser.

Once the administrators configured Samba on Centennial’s Compaq server, they enabled printing services for their Windows workstations.

## Global Printing Services Using Samba

The Linux administrator configured a Public directory on the Samba server. The administrator created a public share and private shares on a per-user basis, and gave all users access to a shared printer controlled by the Samba server. This allowed one computer with the Linux operating system to provide shared Samba printing along with other services, such as secure Web services and user authentication to access the network.
