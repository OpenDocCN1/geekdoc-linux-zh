# # RUNLEVELS

As described on page 440, systemd has done away with traditional runlevels although vestiges remain. Table 10-1 lists the runlevels (target units) as they exist under systemd.

**Table 10-1 Runlevels (target units)**

| SysVinit runlevel | systemd runlevel (target unit) | Name/function |
| :--- | :--- | :--- |
| **0** | `runlevel0.target`, `poweroff.target` | Shuts down the system |
| **1 or S** | `runlevel1.target`, `rescue.target` | Brings the system to single-user/rescue mode |
| **2, 3, 4** | `runlevel2.target`, `runlevel3.target`, `runlevel4.target`, `multi-user.target` | Brings the system to multiuser textual mode |
| **5** | `runlevel5.target`, `graphical.target` | Brings the system to multiuser graphical mode |
| **6** | `runlevel6.target`, `reboot.target` | Reboots the system |
|  | `emergency.target` | Emergency shell |

+   *   **Default (persistent) `runlevel`** By default, systems boot to multiuser graphical mode (`graphical.target`). See “Setting the Persistent Runlevel” on page 444 for instructions on how to change this default.
+   *   **`runlevel`** The `runlevel` utility (`runlevel` man page) displays the previous and current runlevels. This utility is a transitional tool; it provides compatibility with SysVinit. In the following example, the N indicates the system does not know which was the previous runlevel, and the 5 indicates the system is in multiuser graphical mode.
+   
+   ```text
+   $ runlevel
+   N 5
+   ```
+   *   **`who`** The `who` utility with the `-r` option also displays the current runlevel:
+   
+   ```text
+   $ who -r
+          run-level 5  2013-07-21 14:41
+   ```
+   *   **`telinit`** The `telinit` utility (`telinit` man page) allows a user working with **root** privileges to bring the system down, reboot the system, or change between runlevels. The `telinit` utility is a transitional tool; it provides compatibility with SysVinit and calls `systemctl`. The format of a `telinit` command is
+   
+   ```text
+   telinit runlevel
+   ```
+   
+   where `runlevel` is one of the runlevels described in Table 10-1.