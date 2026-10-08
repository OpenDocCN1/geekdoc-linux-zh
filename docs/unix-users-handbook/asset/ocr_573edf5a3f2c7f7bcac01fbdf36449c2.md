For resources, the elements used to specify a GUI's appearance and behavior, CDE sets values according to the following priorities:

+   1.  **Command line** - When you start a client from the command line, options listed on the command line have top priority.
2.  **Xresources, .Xdefaults, dt.resources, sys.resources**, - When CDE starts, it reads these resource configuration files to determine the value of X resources to use for the session.
3.  **RESOURCE MANAGER** - Resources already in the property **RESOURCE_MANAGER** may affect an application that is just starting.
4.  **app-defaults** - Specifies "default" resource values that differ from built-in resource values.
5.  **built-in defaults** - Default resources that are "hard coded" have the lowest priority.

Specific resource specifications take precedence over general resource specifications. For example, suppose that you want a certain font in your text entry areas. You could correctly specify a *FontList* resource in your personal **.Xdefaults** file, only to have it overwritten by an \*XmText\*FontList in an **app-defaults** file. Although **app-defaults** is of lower priority than **.Xdefaults**, the resource specification set there is more specific, so it takes precedence.

For environment variables, CDE sets values according to the following priorities:

+   1.  **$HOME/.dtprofile** - User-specific variables have top priority.
2.  **/etc/dt/config/C/Xsession** - Custom system-wide variables not read by X server.
3.  **/etc/dt/config/C/Xconfig** - Custom system-wide variables read by X server.
4.  **/usr/dt/config/C/Xsession** - Default system-wide variables not read by X server.