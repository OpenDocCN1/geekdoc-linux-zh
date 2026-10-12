
3. Secure physical access to the server.
4. Create worst-case-scenario policies.
5. Keep up-to-date with security news.

Each of these is covered in the following sections, and each is as important as the others.

### Assessing Your Vulnerability

It is a common mistake for people to assume that switching on a firewall makes them safe. This is not the case and, in fact, has never been the case. Each system has distinct security needs, and taking the time to customize its security layout gives you maximum security and the best performance.

The following list summarizes the most common mistakes:

- **Installing every package**—Do you plan to use the machine as a DNS server? If not, why have BIND installed? Go through the Add/Remove Applications dialog and ensure that you have only the software you need.
- **Enabling unused services**—Do you want to administer the machine remotely? Do you want people to upload files? If not, turn off SSH and FTP because they just add needless attack vectors. This goes for many other services.
- **Disabling the local firewall on the grounds that you already have a firewall at the perimeter**—In security, depth is crucial. The more layers someone has to hack through, the higher the likelihood she will give up or get caught.
- **Letting your machine give out more information than it needs to**—Many machines are configured to give out software names and version numbers by default, which is just giving hackers a helping hand.
- **Placing your server in an unlocked room**—If so, you might as well just turn it off now and save the worry. The exception to this is if all the employees at your company are happy and trustworthy. But why take the risk?
- **Plugging your machine into a wireless network**—Unless you need wireless, avoid it, particularly if your machine is a server. Never plug a server into a wireless network because it is just too fraught with security problems.

After you have ruled out these mistakes, you are onto the real problem: Which attack vectors are open on your server? In Internet terms, this comes down to which services are Internet-facing and which ports they are running on.

Two tools are often used to determine your vulnerabilities: Nmap and Nessus. Nessus scans your machine, queries the services running, checks their version numbers against its list of vulnerabilities, and reports problems.

Although Nessus sounds clever, it does not work well in many modern distributions (Fedora included) because of the way patches are made available to software. For example, if you're running Apache 2.0.52 and a bug is found that's fixed in 2.0.53, Fedora backports that patch to 2.0.52. This is done because the new release probably also includes new features that might break your code, so the Red Hat team takes only what is necessary and applies it into your version. As a result, Nessus will see the version 2.0.52 and think it is vulnerable to a bug that has in fact been backported.

The better solution is to use Nmap, which scans your machine and reports on any open TCP/IP ports it finds. Any service you have installed that responds to Nmap's query is pointed out, which enables you to ensure that you have locked everything down as much as possible.

To install Nmap, select System Settings, Add/Remove Applications. Near the bottom of the list of applications is System Tools, where you can select Nmap-frontend and Nmap. Although you can use Nmap from a command line, it is easier to use with the front end—at least until you become proficient. To run the front end, select Actions, Run Application and run nmapfe. If you want to enable all Nmap's options, you need to switch to root and run nmapfe from the console.

The best way to run Nmap is to use the SYN Stealth scan, with OS Detection and Version Probe turned on. You need to be root to enable the first two options (they are on by default when you are root), but it is well worth it. When you run Nmap (click the Scan button), it tests every port on your machine and checks whether it responds. If it does respond, Nmap queries it for version information and then prints its results onscreen.

The output lists the port numbers, service name (what usually occupies that port), and version number for every open port on your system. Hopefully, the information Nmap shows you will not be a surprise. If there is something open that you do not recognize, a hacker might have placed a backdoor on your system to allow her easy access.

You should use the output from Nmap to help you find and eliminate unwanted services. The fewer services that are open to the outside world, the more secure you are.

## Protecting Your Machine

After you have disabled all the unneeded services on your system, what remains is a core set of connections and programs that you want to keep. However, you are not finished yet: You need to clamp down your wireless network, lock your server physically, and put scanning procedures in place (such as Tripwire and promiscuous mode network monitors).

## Securing a Wireless Network

Because wireless networking has some unique security issues, those issues deserve a separate discussion here.

Wireless networking, although convenient, can be very insecure by its very nature because transmitted data (even encrypted data) can be received by remote devices. Those devices could be in the same room; in the house, apartment, or building next door; or even several blocks away. Extra care must be used to protect the actual frequency used by your network. Great progress has been made in the past couple of years, but the possibility of a security breach is increased when the attacker is in the area and knows the frequency on which to listen. It should also be noted that the encryption method used by most wireless NICs is weaker than other forms of encryption (such as SSH) and should not be considered as part of your security plan.

> **TIP** Always use OpenSSH-related tools, such as ssh or sftp, to conduct business on your wireless LAN. Passwords are not transmitted as plain text, and your sessions are encrypted. Refer to Chapter 19, “Remote Access with SSH and Telnet,” to see how to connect to remote systems using ssh.

The better the physical security is around your network, the more secure it will be (this applies to wired networks as well). Keep wireless transmitters (routers, switches, and so on) as close to the center of your building as possible. Note or monitor the range of transmitted signals to determine whether your network is open to mobile network sniffing—now a geek sport known as *war driving*. (Linux software is available at http://sourceforge.net/project/showfiles.php?group_id=57253.) An occasional walk around your building not only gives you a break from work, but can also give you a chance to notice any people or equipment that should not be in the area.

Keep in mind that it takes only a single rogue wireless access point hooked up to a legitimate network hub to open access to your entire system. These access points can be smaller than a pack of cigarettes, so the only way to spot them is to scan for them with another wireless device.

## Passwords and Physical Security

The next step toward better security is to use secure passwords on your network and ensure that users use them as well, especially the root password. If the root password on just one machine is cracked, the whole network is in trouble. For somewhat more physical security, you can force the use of a password with the LILO or GRUB bootloaders, remove bootable devices such as floppy and CD-ROM drives, or configure a network-booting server for Fedora. This approach is not well supported or documented at the time of this writing, but you can read about one way to do this in Brieuc Jeunhomme’s Network Boot and Exotic Root HOWTO, available at http://www.tldp.org/HOWTO/Network-boot-HOWTO/. You can also read more about GRUB and LILO in Chapter 39, “Kernel and Module Management.”

Also, keep in mind that some studies show that as many as 90% of network break-ins are by current or former employees. If a person no longer requires access to your network, lock out access or, even better, remove the account immediately. A good security policy
