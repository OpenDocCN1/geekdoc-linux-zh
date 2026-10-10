**Note**
Only *root* may specify an absolute path with the *-xfs6Config* option, so if an ordinary user must use a special XF86Config file, that file might best reside in the user's home directory and be referenced with a relative path.

# Summary

Although the core of X is simple compared to many competing GUI environments, X is powerful. Indeed, part of X's power comes from its simplicity because higher-level tools, such as widget sets and window managers, can be swapped in and out at will. You can adjust some of these features on a system-wide basis, or even on a user-by-user basis, and individual programs set others.

Much X configuration occurs in the /*/etc/XF86Config* file, which controls global features like the resolution of the video display and the device used for accessing the mouse. This file's format appears mysterious at first, but like many FreeBSD configuration files, its key features can be understood through a few keywords and principles. Nonetheless, using a configuration tool can help you get X up and running quickly, or reconfigure the system with minimal pain if necessary. Setting user-level options usually entails editing a user's X login file (*.xsession* or *.xinitrc, depending upon whether the system is configured to start X automatically or not) or adjusting desktop environment tools.

BASIC SYSTEM
ADMINISTRATION