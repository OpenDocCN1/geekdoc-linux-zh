| Runlevel | Description |
|---|---|
| 0 | Shuts the system down |
| 1 | Single-user mode |
| 2 | Multuser mode but no NFS capability |
| 3 | Full multuser mode; standard runlevel for booting to the command line |
| 5 | Full multuser mode with GUI; standard runlevel for booting into the GUI |
| 6 | Reboots the machine |

+   7. If you are concerned about making mistakes at this point, type “ls -la S > /root/ruIlisting”. This command saves the long version file listing to the file /root/ruIlisting so that you can return to what you had before if necessary.

+   8. Delete the files that correspond to services you do not want to use. The items in this directory are not the real daemons. They are all soft links to the real daemons. So, as long as you backed up the file listing, you can restore items later if necessary.

+   9. Now that you have removed unneeded daemons, you can begin removing other programs that start at boot time. If it helps you to gather your thoughts, type “shutdown -r now” to reboot the machine immediately, and look again at what processes are running after you are back up.

+   10. In Red Hat Linux, type “vi /etc/rc.d/rc.local” to open the file where you are most likely to find non-daemon programs that start at boot time. By default, this file contains the following:

```
#!/bin/sh
#
# This script will be executed *after* all the other init scripts.
# You can put your own initialization stuff in here if you don't
# want to do the full Sys V style init stuff.

if [ -f /etc/redhat-release ]; then
    R=$(cat /etc/redhat-release)

    arch=$(uname -m)
    a="a"
    case "_-$arch" in
        _a*) a="an";;
        _i*) a="an";;
    esac
```