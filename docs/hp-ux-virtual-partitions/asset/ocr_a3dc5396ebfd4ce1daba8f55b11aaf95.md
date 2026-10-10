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

+   *   Workspace Menu 	A menu that displays when mouse button 3 is pressed while the mouse pointer is over the workspace backdrop.

+   *   Button Bindings 	Definitions of what action happens when a particular mouse button is pressed or released while the mouse pointer is over a particular area (frame, icon, window, or root).

+   *   Key Bindings 	Definitions of what action happens when a particular key or key sequence is pressed while the mouse pointer is over a particular area (frame, icon, window, or root).

Unlike configuration files for X or Motif, **sys.dtwmrc** does not control the following configuration elements:

+   *   Front Panel 	The box, usually at the bottom of the workspace, that contains commonly referenced indicators and frequently used graphical con-