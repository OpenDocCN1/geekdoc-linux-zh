
## Nature of Configuration File

| Nature of Configuration File | System-Wide Influence | User's Personal Influence |
|---|---|---|
| File Types & Action Definitions | misc\*.dt files | user-prefs.dt |
| Client Startup at Login | sys.sessions | .Xsession |
|  | Xstartup | sessionetc |
|  | Xsession |  |
|  | Xreset |  |
|  | Xfailsafe |  |
| Workspace Manager & Front Panel | sys.dtwmrc | dtwmrc |
|  | dtwm.fp | user-prefs.fp |
| Clients/Servers & Access | Xaccess | .Xauthority |
|  | Xservers |  |

The file **sys.dtwmrc** controls the configuration of the Workspace Manager at the system level. This includes all of the following:

- **Workspace Menu**: A menu that displays when mouse button 3 is pressed while the mouse pointer is over the workspace backdrop.
- **Button Bindings**: Definitions of what action happens when a particular mouse button is pressed or released while the mouse pointer is over a particular area (frame, icon, window, or root).
- **Key Bindings**: Definitions of what action happens when a particular key or key sequence is pressed while the mouse pointer is over a particular area (frame, icon, window, or root).

Unlike configuration files for X or Motif, **sys.dtwmrc** does not control the following configuration elements:

- **Front Panel**: The box, usually at the bottom of the workspace, that contains commonly referenced indicators and frequently used graphical controls, including a six-button workspace switch.
- **Slidewp Subpanels**: Menus that slide up from the front panel at various locations to provide more functionality without consuming more screen space.

Instead, to avoid a massively large and overly complex configuration file, these elements were separated into their own configuration file in CDE, dtwm.fp.

Some front panel configuration elements, like the number of workspaces and their arrangement in the workspace switch, are controlled through resources in a **sys.resources**, **dt.resources**, or **.Xdefaults** file. Like other Workspace Manager configuration files, **sys.dtwmrc** can be copied to a user's home directory, actually to $HOME/.dt as **dtwmrc**, and modified to personalize the user's environment beyond the system-wide configuration of **sys.dtwmrc**.

The **sys.resources** file is one of those files you might modify once, and then never again. The **dt.resources** file is one file you won't ever need to modify and can ignore. The **.Xdefaults** file is one you or your users may modify on occasion.

The **sys.resources** file is where you put any non-default resources that you want in effect when a brand new user logs into CDE for the very first time. For example, as system administrator, you may want your users to have a CDE front panel with prenamed workspaces, special colors, particular fonts, or application windows in certain locations. After the first-time login, **sys.resources** is ignored in favor of **dt.resources**. This file, **dt.resources**, resides in $HOME/.dt/sessions/current (or $HOME/.dt/sessions/home when the home session is restored) and is created automatically by CDE. You can consider it a CDE working file and forget about it. The **.Xdefaults** is where you or an end-user would list X resources specific to the user's personal CDE environment. **sys.resources**, **dt.resources**, and **.Xdefaults** contain a list of resources and their values.

The **sys.sessions** file controls which clients start the very first time a new user logs into CDE. The **dt.sessions** file is to **sys.sessions** as **dt.resources** is to **sys.resources**.

It may be efficient to configure CDE to start particular applications for your users. You would specify these applications in **sys.sessions**. When a new user logs in for the first time, the CDE environment includes the specified clients. At the end of this first session by logging out, the remaining clients would be recorded in $HOME/.dt/sessions/current for CDE ($HOME/.dt/sessions/home when the home session is restored).

The `sys.dttprofile` file is a template that is automatically copied at first login into each new user's home directory as `.dttprofile`. `sys.dttprofile` replaces `.profile` or `.login` in the CDE environment (although either `.profile` or `.login` can be sourced in `.dttprofile` by removing the # comment symbol in front of DTSOURCEPROFILE=true). The `.dttprofile` file holds the personal environment variables that would, in a character-based environment, be found in `.profile` or `.login`. Use `.dttprofile` to avoid the interference that terminal I/O commands cause to CDE's graphical environment.

The CDE login manager, `dttlogin`, presets the following environment variables to default values:

| Variable | Description |
| :--- | :--- |
| DISPLAY | The name of the local display |
| EDITOR | The default text editor |
| HOME | The user's home directory as specified in `/etc/passwd` |
| KBD_LANG | The current language of the keyboard |
| LANG | The current NLS language |
| LC_ALL | The value of LANG |
| LC_MESSAGES | The value of LANG |
| LOGNAME | The user's login name as specified in `/etc/passwd` |
| MAIL | The default file for mail (usually /var/mail/$USER) |
| PATH | The default directories to search for files and applications |
| USER | The user name |
| SHELL | The default shell as specified in `/etc/passwd` |
| TERM | The default terminal emulation |
| TZ | The time zone in effect |

Variations to these default values belong in each user's `.dttprofile`. Additional environment variables can be added as needed to shape the user's environment to the needs of the work context. Just beware of using commands that cause any terminal I/O.

Like `.dttprofile`, `$Xsession` is a shell script that sets user environment variables. The environment variables in `Xsession` apply system-wide. The environment variables in `.dttprofile` apply only to a user's personal environment. Furthermore, because the login manager runs `Xsession` after the X server has started, the variables in **Xsession** are not available to the X server. Variables typically set in **Xsession** include the following:

| Item | Description |
| :--- | :--- |
| **EDITOR** | The default text editor. |
| **KBD_LANG** | The language of the keyboard (usually, set to the value of `LANG`). |
| **TERM** | The default terminal emulation. |
| **MAIL** | The default file for mail, which is usually `/var/mail`$USER. |
| **DTHELPISEARCHPATH** | The locations to search for CDE help files. |
| **DTAPPSEARCHPATH** | The locations to search for applications registered with the CDE application manager. |
| **DTDATABASESEARCHPATH** | The locations to search for additional action and datatype definitions. |
| **XMICONSEARCHPATH** | The locations to search for additional icons. |
| **XMICONBMSEARCHPATH** | Same as above. |

As an example, suppose that you are the system administrator for several mixed workstation and X terminal clusters located at a single site. As usually happens, most users have grown accustomed to certain text editors. Some like `vi`, others prefer `emacs`, and a couple wouldn't be caught dead without `dmx`. An easy way to provide each user with his or her favored text editor would be to reset their **EDITOR** variable to the appropriate value in the individual **.cprofile** files.

**Xconfig** contains resources that control the behavior of **dtlogin** and it also provides a place to specify the locations for any other **dtlogin** configuration files you create. The **Xconfig** file works on a system-wide basis, so it's one of those files that you modify only once and then forget about. When, during login, **Xconfig** is run, several CDE configuration files get referenced: **Xaccess**, **Xservers**, **Xresources**, **Xstartup**, **Xsession**, **Xreset**, and **Xfailsafe**. Like **Xconfig** itself, most of these files are the type that you modify once when installing CDE and then, unless the network topology changes, you never deal with again.

**Xaccess**, as the name implies, is a remote display access control file. **Xaccess** contains a list of the host names allowed or denied XDMCP connection access to the local computer. For example, when an X terminal requests login service, dtlogin consults the **Xaccess** file to determine whether service should be granted.

The primary use of the **Xservers** file is to list the display screens on the local system that dtlogin is responsible for managing. dtlogin reads the **Xservers** file and starts an X server for each display listed there. It then starts a child dtlogin process to manage the server and display the login screen. Note that dtlogin works only locally; dtlogin can't start an X server on a remote system or X terminal. For remote display servers, some other mechanism must be used to start the server, which then uses the X Display Management Control Protocol (XDMCP) to request a login screen from dtlogin.

The **Xservers** file is another of those files that you may spend some time with initially and then, unless the topology of your network changes, never deal with again. When do you use **Xservers**? When a display doesn't match the default configuration. The default configuration assumes that each system has a single bitmap display and is the system console. X terminals, multiple displays (heads), multiple screens, and Starbase applications all require configuration lines in the **Xservers** file.

The **Xresources** file contains the list of resources that control the appearance and behavior of the login screen. After you substitute your company's logo for the CDE logo and change the fonts and colors, you'll probably never have to deal with **Xresources** again (unless your company changes its logo).

**Xstartup** is a system-wide configuration file executed by the login manager, from which it receives several environment variables:

| VARIABLE | DESCRIPTION |
| :--- | :--- |
| DISPLAY | The name of the local display. |
| USER | The login name of the user. |
| HOME | The user's home directory. |
| PATH | The value of the systemPath resource in Xconfig. |
| SHELL | The value of the systemShell resource in Xconfig. |
| XAUTHORITY | The file to access for authority permissions. |
| TZ | The local time zone. |
