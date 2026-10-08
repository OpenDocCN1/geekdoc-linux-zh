
# Security tools

Ensure ne'er-do-wells don't get their hands on your system and files.

## ZULUCRYPT

While you can control access to the data on your computer using user accounts and file permissions, they aren't enough to prevent a determined intruder from gaining access to your private files. The only reliable mechanism to keep your personal data to yourself is to encrypt it. Sure, working with encrypted data is an involved process, but it'll go a long way in reinforcing your security and insulating your data.

*zuluCrypt* is a graphical encryption tool that has an intuitive, easy-to-follow interface. Using the program you can create an encrypted disk within a file, a partition and even USB disks. It can also encrypt individual files with GPG. *ZuluCrypt* can perform block device encryption, which means that it can encrypt everything written to a certain block device. The block device can be a whole disk, a partition or even a file mounted as a loopback device. With block device encryption, the user creates the file system on the block device, and the encryption layer transparently encrypts the data before writing it to the actual lower block device. While encrypted, the storage areas just appears like a large blob of random data and doesn't even reveal its directory structure. All these functions and more are accessed via the excellent user interface. [http://mhgomchangu.github.io/zuluCrypt](http://mhgomchangu.github.io/zuluCrypt)

## GUFW

*Gufw* is the graphical front end for *UFW*, the uncomplicated firewall, which is one of the easiest front-end for *iptables*. The tool has a simple interface and includes predefined profiles to regulate incoming and outgoing traffic. You can alter the incoming and outgoing policies of the profiles as per your requirements. You can also use *Gufw* to define specific rules for allowing traffic for individual apps and services. [http://gufw.org](http://gufw.org)

![](img/7a0a282248f9658f0c87e55744c797b6_175_0.png)

Switch to the Report tab to get the live network traffic report.

## BITWARDEN

The *BitWarden* password manager does end-to-end encryption and uses AES 256-bit as well as PBKDF2 to secure your data. It goes through this trouble because unlike its peers it stores your encrypted passwords in a remote Microsoft Azure cloud. The app can also import passwords from over 24 sources. [https://bitwarden.com](https://bitwarden.com)

## OQUERY

You can keep an eye on your network using the *oquery* CLI tool that enables you to query your devices just like a database. You can use the tool to check logged in users, keep an eye on the firewall, identify outdated kernels and keep an eye on the loaded kernel modules and the running processes. [https://oquery.io](https://oquery.io)

## STEGOSUITE

Steganography is the art of concealing data inside another seemingly harmless message or image. The most common mechanism for implementing it is by replacing unused data in regular computer files with bits of information that aren't visible when viewing the original piece of data. Steganography is mostly used to complement encryption.

*Stegosuite* is a graphical tool that can hide text messages as well as any type of file inside an image. Fire up the tool, select an image, point it to the files you want to hide inside it and enter a secret key to burn it in the image. To get the secret files from the image load it once again and use the Extract button along with the secret key to grab the hidden files and message from the image. [https://stegosuite.org](https://stegosuite.org)

### MTR

*MTR* is a simple CLI network diagnostic tool that combines the functionality of the *traceroute* and *ping* utilities. So along with the path of the packet it displays a wealth of other relevant information. [www.bitwizard.nl/mtr](www.bitwizard.nl/mtr)

### AIDE

You can use *AIDE* to help spot intrusions by checking the integrity of the files by comparing their properties such as permissions against a baseline database created on the initial run. [http://aide.sourceforge.net](http://aide.sourceforge.net)

### NIKTO2

A CLI web server scanner that hunts for potential problems like server misconfigurations and outdated versions and version-specific issues. It can also perform automated tests against security vulnerabilities. [https://cirt.net/Nikto2](https://cirt.net/Nikto2)

### JOHN THE RIPPER

A password cracker. *John The Ripper* is used for exposing weak Unix passwords. It's a CLI tool but also has a graphical interface called *Johny* that exposes its various command line options. [www.openwall.com/john](www.openwall.com/john)

### MALTRAIL

*MalTrail* is a malicious-traffic detection system that uses publicly accessible blocklists, custom user-defined lists and more to detect and log any malicious traffic. [https://github.com/stamparm/maltrail](https://github.com/stamparm/maltrail)

# Developer tools

Make your coding life easier with this collection of capable utilities.

## ATOM

Atom describes itself as a hackable text editor. Developed by GitHub, the tool has a built-in package manager that enables users to search and install plugins from within it. About 80 plugins ship with the utility by default. One of its more interesting features is the find and replace function that can also modify text across multiple files as you type.

Atom can also be used as an IDE and one of its highlights is the smart autocomplete feature. There's also a bracket matcher feature that highlights the line-number of the closing bracket corresponding to the one under your cursor. You can also define custom key bindings and add more functionality with packages for items such as minimaps and syntax-specific snippet libraries. [https://atom.io](https://atom.io)

## BPYTHON

A Python shell that provides modern IDE-like features inside a terminal window. You can start using it with the default settings and then customise it by editing its config file. The shell does code completion and will also display a list of expected parameters. It highlights syntax as you type and the Rewind feature checks the entire code, which is kept in memory.

[https://bpython-interpreter.org](https://bpython-interpreter.org)

![](img/7a0a282248f9658f0c87e55744c797b6_176_0.png)

BPython enables you to save a session to a file, or even send it to pastebin.

## ETHERPAD

Collaboration is key to any project. The Etherpad text editor enables users to collaborate on text in real-time. It runs inside the web browser and enables participants to interact via a text-based chat. It's full of features and you can take it for a spin on its website. [http://etherpad.org](http://etherpad.org)

## VIRT-MANAGER

The Virtual Machine Manager is the open source graphical frontend for creating KVM-based VMs. It uses the qemu-kvm hypervisor, which is a version of the qemu machine emulator, and includes a VNC and SPICE client that displays a graphical console to the running VM. [https://virt-manager.org](https://virt-manager.org)

## TURKEY APPLIANCES

Installing network accessible software or web applications on a server can be quite a task because they require a lot of infrastructure software, which might take you hours to put together. From database servers to basic libraries, you'll have to spend quite a while to assemble a fully functional web server before you can deploy an application on the network.

Furthermore, if you plan to serve users from outside the network, you need to thoroughly examine your web server for any security leaks. This is a major undertaking in itself.

This is where Turkey Linux shines. Using its virtual appliances you can deploy a new server app in no time. Put simply, a Turkey virtual appliance is a self-contained system that packs in a fully functional instance of a web app with just enough components of an operating system to power that tool. The system works straight out of the box and can be deployed on either bare metal or on top of virtual hardware.

Turkey Linux appliances are available in several formats depending on the hardware you want to deploy them on, from bare metal to OpenStack clouds. Importantly though, once they're up and running, irrespective of the platform, they all give you the same interface to administer and manage the web app. [www.turnkeylinux.org](www.turnkeylinux.org)

## OCELOT GUI

The database client can connect and interact with a MySQL or MariaDB server. You can use it to create queries and it can highlight syntax and can fetch and display results from the database. [https://github.com/ocelot-inc/ocelotgui](https://github.com/ocelot-inc/ocelotgui)

## DOXYGEN

Use this CLI tool to generate HTML documentation from the comments in your code. The tool supports many programming languages and can cross-reference the documentation with the code for referrals. [www.doxgen.nl](www.doxgen.nl)

## INFERENCE

If you work with Java, C, C++ or Objective C, use Infer to weed out bugs. The tool includes various analysis and its most interesting feature is that it can work across several procedures across various files. [https://fbinfer.com](https://fbinfer.com)

## MARK TEXT

The markdown editor supports the GitHub markdown spec and the CommonMark spec. It has a live preview, several editing modes and inline Math support and can export documents. [https://github.com/marktext/marktext](https://github.com/marktext/marktext)

## MANTA

When you've completed a project, use Manta to generate invoices and receipts. The invoicing app has a clean interface and several templates that you can customise as per your requirements. [https://github.com/hq1287/Manta](https://github.com/hq1287/Manta)
