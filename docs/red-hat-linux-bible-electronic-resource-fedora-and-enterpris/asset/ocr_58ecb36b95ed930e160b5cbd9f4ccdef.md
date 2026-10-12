> **TIP:** The NIS-HOWTO document suggests that using shadow passwords with NIS is "always a bad idea." Options in the Makefile (described in the next section) enable you to automatically merge the `shadow` and `gshadow` files into the `passwd` and `group` files, respectively.

# ### Choosing mapping options

Within the Makefile, several options are set. You can choose to change these options or leave them as they are. Here are the options:

+   • **B=** — You can use the `B=` option to allow NIS to use the domain name resolver to find hosts that are not in the current domain. By default, `B=` is not set. To turn on this feature, set it to `-b` (`B=-b`).

+   • **NOPUSH=true** — When set to `true` (the default), the `NOPUSH` option prevents the maps from being pushed to a slave server. This implies that the NIS master server is the only server for the NIS domain. Set this to `false`, and place the host names of slave servers into the `/var/yp/ypservers` file if you do not want the NIS master to be the only server for the domain.

+   • **MINUID=500** — To prevent password entries from being distributed for administrative users, the `MINUID` is set to 500. This assumes that all regular user accounts on the system that you want to share have UIDs that are 500 or above.

+   • **MINGID=500** — To prevent password entries from being distributed for administrative groups, the `MINGID` is set to 500. This assumes that all regular groups that you want to share have GIDs that are 500 or above.

> **NOTE:** Tools for adding users and groups to Red Hat Linux always begin with the number 500. Some UNIX and Linux systems, however, may use lower UIDs and GIDs for regular users. In those cases, you may need to lower `MINUID` and `MINGID` to below 500, but not below 100 (which always represent administrative logins).

+   • **MERGE_PASSWD=true** — Keep this option `true` if you want each user’s password to be merged from the `shadow` file back into the `passwd` file that is shared by NIS.

+   • **MERGE_GROUP=true** — Keep this option `true` if you want each group’s password to be merged from the `gshadow` file back into the `group` file that is shared by NIS.

To build the NIS maps, your system must have the `awk`, `make`, and `umask` commands. In the Makefile, the locations of these commands are `/usr/bin/gawk`, `/usr/bin/gmake`, and `umask`, respectively. (The `umask` command is a shell built-in command, so you don’t have to look for its location.) You can use comparable commands in different locations by changing the values of the `AWK`, `MAKE`, and `UMASK` variables in the Makefile.

Besides the options just mentioned, there are several variables you can set to change the location of NIS files. For example, the locations of password files (`YPPWDDIR`) and other source files (`YPSRCDIR`) are both set to `/etc` by default. The location of YP commands