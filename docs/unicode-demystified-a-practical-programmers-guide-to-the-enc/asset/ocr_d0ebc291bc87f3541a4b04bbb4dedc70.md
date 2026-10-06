# Samba/swat

| GNOME | GNOME: Extras=>Server Settings=>Samba Configuration start-here: Server SettingsExtras=>Samba Configuration |
| KDE | menu: Extras=>Server Settings=>Samba Configuration start-here: Server SettingsExtras=>Samba Configuration |
| graphical | Point a browser on the local system to http://127.0.0.1:901 |
| character-based | Point lynx or links on the local system to http://127.0.0.1:901 |

Samba is a free suite of programs that implement the Server Message Block (SMB) protocol on several operating systems, including GNU/Linux. A Samba server shares files and printers on a host system with client systems. Samba systems that use the SMB protocol natively, and are thus potential clients, include MS Windows, Manager, and OS/2. The Common Internet Filesystem (CIFS), Microsoft Networking, and NetBIOS all use the SMB protocol.

The suite includes many programs, each having many options, switches, modes, and so on, so that you can work with Samba on many different levels. This section gives you an introduction so that you can set up and use Samba in a minimal configuration; it also points you toward the documentation you will need to work with Samba at a higher level.

Before you start, make sure that you have all the necessary Samba packages installed:

```
$ rpm -qa | grep samba
samba-common-2.2.5-10
samba-2.2.5-10
samba-swat-2.2.5-10
```

The Samba Web Administration Tool (swat) is a browser-based utility that allows you to control Samba setup and administration graphically and gives you access to the Samba documentation. Before you can use swat, you must enable xincted to launch swat and enable the swat daemon: Run Service Configuration (redhat-config-services: Configures Services II on page 946), and repeat the following for runlevels (on the menubar) 3 and 5:

+   - Click samb to put a check mark in the checkbox.
- Click Start (on the toolbar) to start the smb service.