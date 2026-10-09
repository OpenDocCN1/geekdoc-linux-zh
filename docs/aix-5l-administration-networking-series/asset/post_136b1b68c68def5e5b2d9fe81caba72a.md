
Figure 5-4. Web-Based System Manager main window

In this environment, the AIX system that is managed remotely is the *server* and the system from which you perform the administration is the *client*. WebSM has been tested with both Netscape Navigator and Microsoft Internet Explorer.

WebSM can be run from any operating system platform that uses a Java 1.3, and *above*, enabled browser. To date, WebSM has been tested only on AIX 5L versions 5.0 and 5.1 and on Microsoft Windows NT, 98, ME, and 2000.

WebSM can be started from the AIX Common Desktop Environment (CDE) application manager System_Admin window or from the command line using the *wsm* command.

## DISTRIBUTED SYSTEMS MANAGEMENT

Distributed system management tools seem to come and go. Distributed SMIT is available as part of IBM’s system management products, which provide a SMIT interface for managing distributed UNIX platforms. References to DsMIT began to disappear after the announced merger of SystemView with Tivoli’s Tivoli Management Environment (TME).

### DSMIT

Distributed System Management Interface (DSMIT) is installed as a separate product on AIX V3.2.5 and AIX V4. Functionally, it is the same as single-system SMIT, but it goes a step further in allowing remote management of a number of vendor UNIX products including the following:

- AIX 3.2.5, AIX V4
- Sun OS 4.1.3
- Solaris 2.3, Solaris 2.4
- HP-UX 9.0

As you might expect, DSMIT is broken up into clients (managed systems) and servers (managing systems). Machines managed by DSMIT are grouped into domains. Subsets of machines within a domain are called the working collective. Table 5-5 shows the breakdown of systems and various configuration information stored in the /usr/share/DSMIT directory.

| File | Purpose |
|---|---|
| domains | Client groups |
| dsmitos | Operating systems managed |
| clients | Managed hosts |
| security/v5srvtab | Principal key |
| security/admin.cfg | Administrator keys |
| security/managing.cfg | Managing systems keys |
| security/managed.cfg | Managed systems keys |
| security/dsmit.ptr | DSMIT config file server |

Table 5-5. /usr/share/DSMIT

As you might imagine, security in a distributed management environment is a critical issue. DSMIT uses MIT Kerberos V5 security services for authenticating DSMIT servers and clients. Commercial masking data facility (CMDF) and message authentication code (MAC) protocols are used to ensure data integrity and guard against message tampering. The nice thing about this is that, after you have validated yourself to Kerberos as a System Administrator, you don't need to log into each system you will be managing.

DSMIT allows you to select sets of systems for management functions. When an update is to be made, you can choose to send the command to all machines in the set at once (concurrent mode) or one at a time (sequential mode). You can bail out in the latter case if problems with an update are indicated. To make things easy or confusing (depending on your point of view), a shell environment variable can be set to indicate that DSMIT should be run when a user or administrator types **SMIT**.

```
SMIT=d      # Invoke DSMIT instead of SMIT
```

This is about all we’re going to say about DSMIT, since bets are being placed on a replacement from Tivoli. The following section describes the OSF’s Distributed Management Environment (DME) specification to give you some background on Tivoli’s systems management technology. Tivoli was one of the principal technology providers for the DME specification.

### DME History

In the early 1990s, the Open Software Foundation defined a management standard for distributed systems called the Distributed Management Environment (DME). The DME technology specification defines a uniform and consistent set of tools and services that may be used to manage both standalone and distributed heterogeneous systems, applications, and networks.

DME combines a select set of vendor management technologies into a consistent framework based on a three-tier model. The lowest tier supports single-host management activities. The second level provides cell naming and security management in distributed environments. The top level encompasses enterprise-wide management via Motif-based GUI interfaces. DME routines communicate with managed objects using DCE, SNMP, and OSI CMIP. Table 5-6 lists the DME technology selections by the developing entity.

The DME Request for Technology (RFT) was first issued in July 1990. After evaluation by OSF’s Munich Development Office, a selection was made in September 1991. The selected technologies went through a period of integration testing, during which time code snapshots were made available to interested parties. DME license fees were set, and the first code release was scheduled for the fourth quarter of 1993.

| Vendor | Technology Selections |
|---|---|
| IBM | Data Engine, System Resource Controller |
| MIT Project Athena | Palladium Print Services |
| Tivoli | WizDOM Object Oriented Framework |
| Banyan | Network Logger |
| HP | Open View Network Management Server |
| | Software Distribution/Installation Utils |
| | Network License Manager |
| Groupe Bull | Consolidated Management API |
| Gradient | PC Ally and Client Lib for Net License Server |
| | PC Agent and Event Components |

Table 5-6. DME Technology Selections

## SMIT

- `smit` Motif interface
- `smit -C`, `smitty` TTY interface
- `smit -X` Inhibit updates, test drive SMIT
- `F6-key` Display command to be executed by SMIT
- `smit <fast-path-name>` Display SMIT submenu
- `$HOME/smit.log` SMIT transaction log
- `$HOME/smit.script` SMIT command log
- `/usr/lib/objrepos/` SMIT ODM panel database sm_xxxx_xx
- DsMIT Distributed SMIT
- `SMIT=d` Invoke DSMIT instead of SMIT

## WSM

- `wsm` Start the Web-based System Manager Interface

## CHECKLIST

The following is a checklist for the key points in system management:

- ☐ Execute the System Management Interface Tool or SMIT, the base system administration management tool for AIX, with the `smit` command for a Motif interface or the `smitty` command for an ANSI interface.
- ☐ Press the F6 key within SMIT to display the actual AIX command and arguments it will invoke before committing the update.
- ☐ Invoke SMIT help from any menu by pressing the F1 key.
- ☐ SMIT creates an audit log of each SMIT session named `smit.log` in the user's `$HOME` directory.
- ☐ SMIT appends the AIX commands invoked during the session to a local `$HOME/smit.script` file.
- ☐ You can use the `smit.script` file to create shell scripts to automate systems changes and reconfigurations.
- ☐ You can bypass SMIT dialog and menu screens and enter a task directly through the use of a FastPath name.
- ☐ Remember FastPath command names by appending one of four prefixes, **ls**, **mk**, **ch**, and **rm**, to a root task name in the **list**, **make**, **change**, and **remove** operating system objects.
- ☐ SMIT uses three types of display panels, Menu, Selector, and Dialog, to manage the dialog between the user and management tasks.
- ☐ SMIT objects are stored in eight files in a designated database found in the `/usr/lib/objrepos` directory by default. These eight files should always be maintained together, including saving and restoring.
- ☐ AIX 5L’s Web-Based System Manager (WSM) provides mouse-driven, point-and-click, drag-and-drop system management tools.
- ☐ Start WebSM from the AIX Common Desktop Environment (CDE) application manager System_Admin window or from the command line using the **wsm** command.
- ☐ In the client/server mode, WSM can manage AIX systems from a remote PC or from another AIX system that uses a graphical user interface.
- ☐ Distributed SMIT, DSMIT, goes a step further than SMIT by allowing remote management of multiple vendors’ UNIX products.
- ☐ When you make an update with DSMIT, you can choose to send the command to all machines in the set at once (concurrent mode) or one at a time (sequential mode).
