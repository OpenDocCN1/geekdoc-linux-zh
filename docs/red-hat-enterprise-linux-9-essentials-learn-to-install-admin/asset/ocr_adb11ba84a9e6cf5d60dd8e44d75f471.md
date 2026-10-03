# RHEL 9 Remote Desktop Access with VNC

of groups that are either installed or available to be installed can be obtained using the dnf utility as follows:

```
# dnf grouplist
Updating Subscription Management repositories.
Available Environment Groups:
    Server with GUI
    Minimal Install
    Workstation
    Custom Operating System
    Virtualization Host
Installed Environment Groups:
    Server
Installed Groups:
    Container Management
    Headless Management
Available Groups:
    Legacy UNIX Compatibility
    Graphical Administration Tools
    Smart Card Support
    RPM Development Tools
    .NET Development
    System Tools
    Development Tools
    Console Internet Tools
    Security Tools
    Network Servers
    Scientific Support
```

The Workstation environment group is listed as available (and therefore not already installed) in the above example. To find out more information about the contents of a group before installation, use the following command:

```
# dnf groupinfo workstation
Updating Subscription Management repositories.
Environment Group: Workstation
Description: Workstation is a user-friendly desktop system for laptops and PCs.
Mandatory Groups:
    Common NetworkManager submodules
    Core
    Fonts
    GNOME
    Guest Desktop Agents
    Hardware Support
    Internet Browser
    Multimedia
```