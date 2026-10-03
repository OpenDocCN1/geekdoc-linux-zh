
## Configuring SSH Key-based Authentication on RHEL 9

filter to All Files (*.*) for the key file to be visible). Once located, select the file and load it into PuTTYgen. When prompted, enter the passphrase used initially to encrypt the file. Once the private key has been imported, save it as a PuTTY key file by clicking the Save Private Key button. For consistency, save the key file to the .ssh folder but give it a different name to differentiate it from the original key file.

Launch PuTTY from the Start menu and enter the IP address or hostname of the remote server into the main screen before selecting the Connection -> SSH -> Auth -> Credentials category in the left-hand panel, as highlighted in Figure 15-3:

![](img/be1f159c3cc937d7b264dc5b134856dc_136_0.png)

Figure 15-3

Click the Browse button next to the Private key for authentication field and navigate to and select the previously saved PuTTY private key file. Then, optionally, scroll to the top of the left-hand panel, select the Session entry, and enter a name for the session in the Saved Sessions field before clicking on the Save button. This will save the session configuration for future use without re-entering the settings each time.

Finally, click on the Open button to establish the connection to the remote server, entering the user name and passphrase when prompted to do so to complete the authentication.

### 15.9 Generating a Private Key with PuTTYgen

The previous section explored using existing private and public keys when working with PuTTY. If keys do not exist, they can be created using the PuTTYgen tool, which is included in the main PuTTY installation.

To create new keys, launch PuTTYgen and click on the Generate button highlighted in Figure 15-4:

![](img/be1f159c3cc937d7b264dc5b134856dc_137_0.png)

Figure 15-4

Move the mouse pointer to generate random data as instructed, then enter an optional passphrase to encrypt the private key. Once the keys have been generated, save the files to suitable locations using the Save public key and Save private key buttons. As outlined in the previous section, the private key can be used with PuTTY. To install the public key on the remote server, use the steps covered in the earlier section on SSH within PowerShell on Windows.

### 15.10 Summary

Any remote access to a RHEL 9 system must be implemented in a way that provides a high level of security. By default, SSH allows remote system access using password-based authentication. However, this leaves the system vulnerable to anyone who can guess a password or find out the password through other means. For this reason, key-based authentication is recommended to protect system access. Key-based authentication uses public key encryption involving public and private keys. When implemented, users can only connect to a server if they are using a client with a private key that matches a public key on the server. As an added layer of security, the private key may also be encrypted and password protected. Once key-based encryption has been implemented, the server system is configured to disable support for the less secure password-based authentication.

This chapter has provided an overview of SSH key-based authentication and outlined the steps involved in generating keys and configuring clients on macOS, Linux, and Windows, as well as installing and managing public keys on a RHEL 9 server.

## 16. RHEL 9 Remote Desktop Access with VNC

RHEL 9 can be configured to provide remote access to the graphical desktop environment over a network or internet connection. Although not enabled by default, displaying and accessing a RHEL 9 desktop from a system anywhere else on a network or the internet is relatively straightforward. This can be achieved regardless of whether that system runs Linux, Windows, or macOS. There are even apps available for Android and iOS that will allow you to access your RHEL 9 desktop from just about anywhere that a data signal is available.

Remote desktop access can be helpful in many scenarios. For example, it enables you or another person to view and interact with your RHEL 9 desktop environment from another computer system on the same network or over the internet. This is useful if you need to work on your computer when you are away from your desk, such as while traveling. It is also helpful when a co-worker or IT support technician needs access to your desktop to resolve a problem.

When the RHEL 9 system runs on a cloud-based server, it also allows access to the desktop environment as an alternative to performing administrative tasks using the command-line prompt or Cockpit web console.

The RHEL 9 remote desktop functionality is based on a technology known as Virtual Network Computing (VNC). This chapter will cover the key aspects of configuring and using remote desktops within RHEL 9.

### 16.1 Secure and Insecure Remote Desktop Access

In this chapter, we will cover both secure and insecure remote desktop access methods. Assuming you are accessing one system from another within a secure internal network, using the insecure access method is generally safe. If, on the other hand, you plan to access your desktop remotely over any public network, you must use the secure method of access to avoid your system and data being compromised.

### 16.2 Installing the GNOME Desktop Environment

It is, of course, only possible to access the desktop environment if the desktop itself has been installed. If, for example, the system was initially configured as a server, it is unlikely that the desktop packages were installed. The easiest way to install the packages necessary to run the GNOME desktop is to perform a group install. The key to installing groups of packages to enable a specific feature is knowing the group’s name. At the time of writing, there are two groups for installing the desktop environment on RHEL 9: “Server with GUI” and “Workstation”. As the group names tend to change from one RHEL release to another, it is helpful to know that the list of groups that are either installed or available to be installed can be obtained using the dnf utility as follows:

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

- Printing Client
Standard
Workstation product core
base-x
Optional Groups:
  Backup Client
  GNOME Applications
  Headless Management
  Internet Applications
  Office Suite and Productivity
  Remote Desktop Clients
  Smart Card Support

Having confirmed that this is the correct group, it can be installed as follows:

```
# dnf groupinstall workstation
```

Once installed, and assuming that the system has a display added, the desktop can be launched using the following startx command:

```
$ startx
```

If, on the other hand, the system is a server with no directly connected display, the only way to run and access the desktop will be to configure VNC support on the system.

### 16.3 Installing VNC on RHEL 9

Access to a remote desktop requires a VNC server installed on the remote system, a VNC viewer on the system from which access is being established, and, optionally, a secure SSH connection. While several VNC server and viewer implementations are available, Red Hat has standardized on TigerVNC, which provides both server and viewer components for Linux-based operating systems. VNC viewer clients for non-Linux platforms include RealVNC and TightVNC.

To install the TigerVNC server package on RHEL 9, run the following command:

```
# dnf install tigervnc-server
```

If required, the TigerVNC viewer may also be installed as follows:

```
# dnf install tigervnc
```

Once the server has been installed, the system must be configured to run one or more VNC services and open the appropriate ports on the firewall.

### 16.4 Configuring the VNC Server

With the VNC server packages installed, the next step is configuring the server. The first step is to specify a password for the remote desktop environment user. While logged in as root, execute the vncpasswd command (where the user name is assumed to be demo):

```
# su - demo
[demo@demserver ~]$ vncpasswd
Password:
```
