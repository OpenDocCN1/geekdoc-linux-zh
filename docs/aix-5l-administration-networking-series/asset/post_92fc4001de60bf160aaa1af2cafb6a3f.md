
## SMIT Script File

Along with the log file, SMIT appends the AIX commands invoked during the session to a local /home/smit.script file. The script file information can be used to create complex management scripts or review the commands invoked during a previous session. For example, say you use SMIT to configure the first of a set of 64 TTY devices. Edit the /home/smit.script file and, duplicating the mdev command 62 times for the remaining devices, change each device name and attributes as required. The script file can be executed from the command line to complete the definition for the remaining devices. Use the `smit -s <PathName>` option to create a script file in a location other than your home directory.

```
# smit -s /tmp/smit.script   Create a script file in /tmp
```

For example, the smit.script entries surrounding the removal of the paging00 paging space:

```
#       [Jul 26 2001, 22:43:50]
#
rm_lv -f 'paging00'
#
#       [Jul 26 2001, 22:44:23]
#
lsvg -o|lsvg -i -l
#
#   [Jul 26 2001, 22:44:57]
#
rmlv -f '10g1v00'
#
#   [Jul 26 2001, 22:47:20]
#
chdev -1 sys0 -a maxuproc='128'
#
```

As you can see, we were doing a lot more than removing the `paging00` paging space on July 26. We began by removing the `paging00` paging space but then went on to display a listing of all currently active logical volumes, remove the `loglv00` logical volume and set the maximum number of processes per user to 128. The `smitscript` file is extremely valuable when you want to create shell scripts to automate systems changes and reconfigurations.

### SMIT FastPaths

SMIT allows you to bypass dialog and menu screens and enter a task directly through the use of a FastPath name (see Table 5-3). A FastPath name is an identifier for a particular SMIT panel. FastPath names are recorded as part of the `$HOME/smit.log` information. The FastPath name is included as an argument to the **smit** command to enter a task panel directly.

```
# smit nfs ⟵ Access SMIT NFS management
```

Remembering all the FastPath names and management commands can be a real challenge. Fortunately, the AIX developers implemented an easy-to-remember rule for the FastPath and command names. A set of four prefixes, **ls, mk, ch, and rm**, are appended to a root task name in the list, **make, change**, and **remove** operating system objects. For example, to make a TTY device, the FastPath or command name is **mkitty**.

#### FastPath and Command Operations and Objects

AIX administration commands are made up using two parts: the operation followed by an operation object, as shown here:

| Operation | Objects |
| :--- | :--- |
| mk, ls, ch, rm | dev, user, fs, vg, pv, tty, cd, tape, etc. |

Putting the operation with the object will produce a direct SMIT FastPath, in most cases, as shown in Table 5-3.

Many more SMIT FastPath options are available for most every other system management task that has a lower-level submenu. As an example, if you want to go directly to adding a user to the system, the SMIT FastPath is **smitty mkuser**.

| Task | SMIT FastPath |
| :--- | :--- |
| Software installation and maintenance | install |
| Software license management | licenses |
| Device management | dev |
| System Storage management (physical and logical storage) | storage |
| Journaled filesystem management | jfs |
| Logical volume management | lvm |
| NFS management | nfs |
| Security management | security |
| User management | user or users |
| Communications applications and services | commo |
| TCP/IP management | tcpip |
| Print queue management | spooler |
| Problem determination | problem |
| System diagnostics | diag |
| Performance and resource scheduling | performance |
| System environments | system |
| Processes and subsystems | src |

### Customizing SMIT

SMIT is composed of a hierarchical set of menu panels, an NLS message catalog, a command interface, and a logging and scripting facility. These components are integrated to provide a seamless interface for managing the operating system and system resources. Three types of SMIT display panels are used to manage the dialog between the user and management tasks: Menu, Selector, and Dialog. Menu panels display management task selections. Selector panels (see Table 5-4) present a range of values from which you must choose before proceeding with the management task. You may choose more than one. Dialog panels provide input fields for specifying command arguments and values.

| Type | Function |
| :--- | :--- |
| Menu | List of task options |
| Selector | Request additional input before proceeding |
| Dialog | Request values for command arguments and options |

SMIT objects are generated with the ODM generation facility and then stored in files in a designated database. By default, they reside in the /usr/lib/ibmpg/objects directory. The SMIT database consists of the following files, by default:

- sm_menu_opt
- sm_menu_opt.vc
- sm_name_hdr
- sm_name_hdr.vc
- sm_cmd_hdr
- sm_cmd_hdr.vc
- sm_cmd_opt
- sm_cmd_opt.vc

These eight files should always be maintained together, including saving and restoring. After becoming experienced with the ODM (see Chapter 9 for more on the ODM) and SMIT architectures, you may use ODM commands to customize SMIT. SMIT object class names and object identifiers are listed in the SMIT log file when SMIT is invoked with the verbose trace -vt option.

## smit -vt - SMIT verbose tracing

## WEB-BASED SYSTEM MANAGER

For those of you who prefer a bit more flash in system management tools, Web-Based System Manager (WebSM) is the tool for you. WebSM provides a comprehensive set of system management tools for AIX 5L. Because of the mouse-driven, point-and-click, drag-and-drop Web-based desktop environment, WebSM is intuitive to use. It is more colorful than SMIT, and it prevents you from wallowing in the muck of the AIX command line. AIX 5L leans heavily toward the WebSM, and it appears that some new features may be available only via the WebSM in coming AIX releases. Managed objects and associated tasks are displayed as icons with a Web browser look and feel (see Figure 5-4). To perform an action, double-click on the desired object. If additional information is required, a WebSM dialog panel is displayed to acquire configuration information.

The AIX 5L release of WebSM has the ability to manage numerous AIX 5L host machines on both Power and IA-64 hardware. Also new to the 5L release of WebSM is the support for dynamic monitoring of system events through the Resource Monitoring and Control (RMC) software originally created for the IBM RS/6000 SP frames. Now you do not have to write all of those shell scripts to monitor your systems for problems like full filesystems.

WebSM can run in stand-alone or client/server modes. In the stand-alone mode, WebSM manages the local AIX system. In the client/server mode, WebSM can manage AIX systems from a remote PC or from another AIX system that uses a graphical user
