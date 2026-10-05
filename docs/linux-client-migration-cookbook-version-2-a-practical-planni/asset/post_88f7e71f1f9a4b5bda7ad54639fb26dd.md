
illustrates this concept by showing the combination of one IBM IntelliStation Pro workstation and two dual-head graphics cards providing a platform that supports four separate client workstations.

![](img/23b949da14ff7bab8762f0f0361af394_191_0.png)

Figure 7-8 IntelliStation A Pro workstation supporting four workstations using two dual-head video cards

## 7.5.2 What is multi-station computing

The concept of a single computer providing independent desktop environments to multiple users is not new. Many solutions enable desktops to be remotely served to one or more client computers over a network using a single powerful computer such as a mainframe or terminal server.

Traditional terminal server-based solutions require a PC or proprietary thin-client hardware system to be deployed at each user's physical desktop. However, traditional networked thin client solutions are often limited in display and computing performance, and their deployment typically requires additional network bandwidth along with a powerful server system and uses much power infrastructure as regular desktop PCs.

Multi-station computing, in contrast, is based on standard desktop PC hardware to serve each user's monitor, and is designed to overcome many of the challenges and limitations of networked-based client solutions. For new users, there are potential cost savings and management advantages in deploying additional screens and keyboards into existing multi-user platforms, instead of complete stand-alone computer systems.

## A basic multi-station configuration

In a multi-station configuration, multiple client workstations simultaneously share the resources of a single computer. Each user's desktop environment and application processes are supported independently. See Figure 7-9.

![](img/23b949da14ff7bab8762f0f0361af394_192_0.png)

Figure 7-9 IntelliStation A Pro showing VGA and USB connections supporting two client workstations

Each station has an independent set of input and output devices, consisting of a monitor, mouse, and keyboard, which are configured to work together as a set. Figure 7-9 illustrates connections to support two client workstations. Each user is provided with an independent private desktop environment from which the user can access fixed and removed input, output, and storage devices. These devices are directly connected to the workstation through the use of extension cables, USB hubs, and other devices as necessary to provide stations at almost any distance from the shared workstation. You can configure each user's desktop to consist of a single desktop on a single display, or more advanced setups such as multiple virtualized desktops on a single display, or even multiple desktops on multiple displays.

## 7.5.3 Approaches to desktop consolidation and deployment

Desktop virtualization is one of several approaches to desktop consolidation and deployment. Multi-station platforms use virtualization software to manage each user's desktop similar to the way a terminal server or virtual machine operates, however multi-station systems provide each user with a direct connection to their virtual desktop, eliminating the client altogether and consolidating many computer systems into one single shared workstation. In this section, we compare and contrast popular desktop deployment scenarios with a multi-station computing approach.

## Comparison with thin client systems

Thin client technology relies on small footprint client workstations that facilitate user interaction between a server and a remote user via a standard data network. PCs contain both the hardware and software to function independently of any other device, while thin clients require connections to servers to provide a of remotely hosted terminal services: login, session management, hosted applications, and so forth.

Multi-station computing solutions share the advantages of thin client systems such as centralized management and minimal hardware at the physical desktop. However, multi-station client architectures differ from thin client architectures in some key aspects: they can be less dependent on network connection availability, or network bandwidth limitations, and do not require one-to-one deployment of complete client systems for each user.

> Tip: As soon as you move above hardware level considerations, multi-station and thin client architectures can become complimentary instead of competing design strategies. This is illustrated in the following section.

## Comparison with remote desktop systems (RDP, VNC, and XDMCP)

The Remote Desktop Protocol (RDP), X Display Manager Control Protocol (XDMCP), and Virtual Network Computing (VNC) protocol are industry-standard methods of connecting to desktops on remote computer systems through a local area network or Internet.

A user of a PC or thin client system runs an RDP, VNC, or XDMCP client locally, which captures user input from the local keyboard and mouse, sending it to the remote server through a network connection. All of the processing for applications displayed on the remote desktop is performed on the server, which means that the server hardware and configuration sets the hard limit on the number of simultaneous users who can connect to the host server.

In to this physical limit, remote desktop-capable operating systems (including Windows) might require a license for each connecting client, which imposes a software limit to the number of concurrent users on that server. You should consult with your terminal services vendor as to whether client access licensing savings can be realized through a multi-station approach. See Figure 7-10.

![](img/23b949da14ff7bab8762f0f0361af394_194_0.png)

Figure 7-10 On a multi-station system, each client can run a different remote desktop, terminal, or virtual machine

each computer serves multiple users, each of whom could operate one or more remote desktops through local RDP, VNC, or XDMCP client applications. This is illustrated in Figure 7-10 on page remote desktop software, each user on a multi-station system can connect to almost any remote Windows, NIX, or Apple desktop. All of the processing for applications displayed on the remote desktop is done on the host system, with minimal load placed on the multi-station client system. Multi-station configurations also support a variety of ANSI text environments, such as IBM 3270, 5250; VT52, VT100, and many other terminal applications, running in parallel with each other, and with local applications.

Remote desktop clients and servers are available for most popular operating systems, including Windows, Linux, and Mac OS X.

## 7.5.4 Where and when to deploy multi-station systems

There are many factors that you should consider when planning a multi-station deployment. This section discusses deployment considerations pertaining to multi-station Linux desktops and reviews several options for minimizing disruptions and maximizing the value derived from leveraging a shared computing platform. See also Chapter 6, "Migration best practices" on page 131.

### New deployments

Always deploying multi-station systems whenever two or more users are in close proximity and their primary computer usage patterns do not involve frequent CPU or memory intensive application demands. Multi-station deployments make the most sense as a simple management and cost reduction enhancement when a desktop Linux migration or deployment is already being considered. Multi-station desktops based on Linux pose few, if additional challenges over those of single-user desktop Linux deployments. As with single-station workstation deployments, a multi-station Linux deployment benefits from an existing technical infrastructure and expertise capable of supporting workstations and users.

A few factors should be noted when considering multi-station deployments:

- IT partners considering multi-station deployments into open plan offices should ensure that USB and VGA extension cables from monitors and peripherals in work areas to the multi-station computers. In the typical deployment scenario, a cluster of four to six users share one multi-station computer located at a centrally-accessible cubicle. This configuration minimizes the use of extension cables, and all cabling can be run along or within partitions without crossing floor traffic.

- Although costly than extension cables, add-ons that carry keyboard, video, and mouse (KVM) over standard category 5 network cable

168 Linux Client Migration Cookbook, Version 2
