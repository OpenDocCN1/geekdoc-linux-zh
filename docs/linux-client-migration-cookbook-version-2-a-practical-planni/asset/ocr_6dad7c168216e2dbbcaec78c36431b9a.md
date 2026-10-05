system. All of the processing for applications displayed on the remote desktop is done on the host system, with minimal load placed on the multi-station client system. Multi-station systems can support multiple client and terminal emulation sessions running concurrently with graphical desktop environments such as Windows Terminal Services using Remote Desktop Protocol (RDP), Virtual Network Computing (VNC), XDMCP, or Citrix ICA. Multi-station configurations also support a variety of ANSI text environments, such as IBM 3270, 5250; VT52, VT100, and many other terminal applications, running in parallel with each other, and with local applications.

Remote desktop clients and servers are available for most popular operating systems, including Windows, Linux, and Mac OS X.

# 7.5.4 Where and when to deploy multi-station systems

There are many factors that you should consider when planning a multi-station deployment. This section discusses deployment considerations pertaining to multi-station Linux desktops and reviews several options for minimizing disruptions and maximizing the value derived from leveraging a shared computing platform. See also Chapter 6, "Migration best practices" on page 131.

# New deployments

Always deploying multi-station systems whenever two or more users are in close proximity and their primary computer usage patterns do not involve frequent CPU or memory intensive application demands. Multi-station deployments make the most sense as a simple management and cost reduction enhancement when a desktop Linux migration or deployment is already being considered. Multi-station desktops based on Linux pose few, if additional challenges over those of single-user desktop Linux deployments. As with single-station workstation deployments, a multi-station Linux deployment benefits from an existing technical infrastructure and expertise capable of supporting workstations and users.

A few factors should be noted when considering multi-station deployments:

+   - IT partners considering multi-station deployments into open plan offices should ensure that USB and VGA extension cables from monitors and peripherals in work areas to the multi-station computers. In the typical deployment scenario, a cluster of four to six users share one multi-station computer located at a centrally-accessible cubicle. This configuration minimizes the use of extension cables, and all cabling can be run along or within partitions without crossing floor traffic.

+   - Although costly than extension cables, add-ons that carry keyboard, video, and mouse (KVM) over standard category 5 network cable

168 Linux Client Migration Cookbook, Version 2