# Chapter 12

# 12. RHEL 9 Network Management

It is difficult to envisage a RHEL 9 system that does not have at least one network connection and harder still to imagine how such an isolated system could be of much practical use. The simple fact is that RHEL 9 is designed to provide enterprise-level services over network and internet connections. Therefore, a crucial part of learning how to administer a RHEL 9 system involves learning how to configure and manage the network interfaces installed on the system.

This chapter provides an overview of network management on RHEL 9, including the NetworkManager service and tools and some other useful utilities.

# 12.1 An Introduction to NetworkManager

NetworkManager is a service and set of tools designed specifically to make it easier to manage the networking configuration on Linux systems and is the default network management service on RHEL 9.

In addition to a service that runs in the background, NetworkManager also includes the following tools:

+   - **nmcli** - A tool for working with NetworkManager via the command line. This tool is useful when access to a graphical environment is unavailable and can also be used within scripts to make network configuration changes.
- **nmtui** - A basic text-based user interface for managing NetworkManager. This tool can be run within any terminal window and allows changes to be made by making menu selections and entering data. While helpful in performing basic tasks, nmtui lacks many of the features provided by the nmcli tool.
- **nm-connection-editor** - A complete graphical management tool providing access to most NetworkManager configuration options.
- **GNOME Settings** - The Network screen of the GNOME desktop Settings application allows basic network management tasks to be performed.
- **Cockpit Network Settings** - The Network screen of the Cockpit web interface allows a range of network management tasks to be performed.

Although there are several ways to manage the network environment on a RHEL 9 system, this chapter will focus on the nmcli command. While the graphical tools are certainly helpful when you have access to a desktop environment or Cockpit has been enabled, understanding the command-line interface is essential for situations where a command prompt is all that is available. Also, the graphical tools (Cockpit included) only include some of the capabilities of the nmcli tool. Finally, once you are familiar with NetworkManager and nmcli, those skills will translate easily when