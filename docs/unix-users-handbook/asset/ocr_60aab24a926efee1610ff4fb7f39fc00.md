system.mwrmc has been replaced by the Motif version also, system.mwrmc.

# ### Motif Configuration Files

Motif added only one new configuration file to the X list: system.mwrmc.

By convention, this file is kept with the X configuration files in /usr/lib/X11. Actually, this file isn't new; it is the Motif version of system.mwrmc, which simply replaced system.mwrmc in Motif environments.

Whereas X brought network and interclient communication standards to the graphical user interface, Motif brought a standard for appearance and behavior, the standard originally defined in IBM's System Application Architecture Common User Access (SAA/CUA), which forms the basis of most PC-based GUIs. Thus, push buttons and scroll bars have a defined look and a defined behavior, and double-clicking always causes the default action to happen.

From a programmer's point of view, the Motif widget toolkit represents quite an advance over programming in "raw" X. From a user's or system administrator's point of view, the Motif user environment is about the same as the X environment, except that the mwm window manager is replaced with the Motif window manager.

# ### CDE Configuration Files

It is possible to point to over 80 files that, in one way or another, contribute to configuring some aspect of CDE. By convention, these files reside in the /usr/dt directory. However, if you remove from this list such files as those that:

+   - configure CDE applications as opposed to the environment itself

+   - establish default actions and datatype definitions that, although you create your own definitions in separate files, you never modify