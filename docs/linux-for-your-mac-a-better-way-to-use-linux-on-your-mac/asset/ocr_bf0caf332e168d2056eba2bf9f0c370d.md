> If you use a Red Hat Linux-based PowerPC distribution, and log in with the **xdm** display manager, use the *switchdesk* client after you log in to choose your default window manager.

# ### Configuring kdm

Unlike *xdm*, the *kdm* client and login dialog box offers a choice of window managers for your *X* session, which include a **Go!** button to launch the session, a **Cancel** button to cancel your login, and a **Shutdown** button that can be used to shut down, reboot your system, or restart your *X* server.

To log in, type your username, then your password. Before pressing Enter or clicking the **Go!** button, click the drop-down menu to select a window manager to use for your session. *kdm* can be configured during an active KDE session by the root operator using the *kdmconfig* client. This client may be accessed by using the KDE Control Center, or from the command line of an X11 terminal window like this:

```
```bash
# kdmconfig
```
```

After you press Enter, you will see a dialog box, as shown in Figure 7.15.

![](bbox=[0.08, 0.59, 0.68, 0.95])