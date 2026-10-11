The inetd daemon is configured using the */etc/inetd.conf* file. All of the services managed by inetd are configured in this single configuration file. Each line in this file configures a single service to be managed by inetd. The syntax used in *inetd.conf* is shown here:

```
service_name socket_type protocol flags user executable arguments
```

You can use TCP wrappers with inetd just as you did with xinetd. This allows you to control access to the network services running on the host using the */etc/hosts.allow* and */etc/hosts.deny* files.

# ## Accelerated Review

+   - Many organizations overlook physical security and leave their systems in unsecured areas.
+   - Servers need the highest degree of physical security and should be locked in a server room where physical access is strictly controlled.
+   - Workstations require a higher degree of access than servers.
+   - Access to the work area itself should be secured to prevent unauthorized persons from accessing users' workstations.
+   - Because users tend to leave workstations logged in while the system is unattended, you should implement screen-saver passwords.
+   - You should train your users to lock their workstations or log out completely before leaving their systems.
+   - You can use the *nohup* command to load processes and allow them to continue running even if you log out from the shell prompt.
+   - Users, groups, and permissions are the main means of controlling access to the system.
+   - The root user should be used only to complete root tasks; all other tasks should be completed using a standard user account.
+   - The system should never be left unattended while the root user is logged in.
+   - You can use the *su* command to switch to the root user account when you need to complete tasks that require root-level access.
+   - You can use the *exit* command to switch back to your regular user account.
+   - You can use the *sudo* command to allow specific users to run commands as root without giving them your root password.
+   - You use the */etc/sudoers* file to specify which users can run what commands as root.
+   - You edit */etc/sudoers* using the *visudo* utility, which will check your syntax to make sure you didn't make syntax errors in the file.
+   - Users need to be trained to avoid using passwords that can be easily guessed.