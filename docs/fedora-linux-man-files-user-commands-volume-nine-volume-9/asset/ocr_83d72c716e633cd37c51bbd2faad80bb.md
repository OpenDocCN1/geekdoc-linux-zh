# ## OPTION

**—clear-groups**
Clear supplementary groups.

**-d, —dump**
Dump current privilege state. Can be specified more than once to show extra, mostly useless, information. Incompatible with all other options.

**—groups** *group*…
Set supplementary groups. The argument is a comma-separated list.

**—inh-caps** *(+|-)*cap*… or **—bounding-set** *(+|-)*cap*…
Set the inheritable capabilities or the capability bounding set. See (7). The argument is a comma-separated list of +cap and -cap entries, which add or remove an entry respectively. **+all** and **-all** can be used to add or remove all caps. The set of capabilities starts out as the current inheritable set for **—inh-caps** and the current bounding set for **—bounding-set**. If you drop sothing from the bounding set without also dropping it from the inheritable set, you are likely to beco confused. Do not do that.

**—keep-groups**
Preserve supplementary groups. Only useful in conjunction with **—rgid**, **—egid**, or **—regid**.

**—list-caps**
List all known capabilities. This option st be specified alone.

**—no-new-privs**
Set the *no_new_privs* bit. With this bit set, (2) will not grant new privileges. For example, the setuid and setgid bits as well as file capabilities will be disabled. (Executing binaries with these bits set will still work, but they will not gain privileges. Certain LSMs, especially AppArmor, may result in failures to execute certain programs.) This bit is inherited by child processes and cannot be unset. See (2) and *Docunation/:prctl/:no:_new_:privs.txt* in the Linux kernel source.
The no_new_privs bit is supported since Linux 3.5.

**—rgid** *gid*, **—egid** *gid*, **—regid** *gid*
Set the real, effective, or both gids. The gid argument can be given as textual group na.

For safety, you st specify one of **—clear-groups**, **—groups**, or **—keep-groups** if you set any primary *gid*.

**—ruid** *uid*, **—euid** *uid*, **—reuid** *uid*
Set the real, effective, or both uids. The uid argument can be given as textual login na.

Setting a *uid* or *gid* does not change capabilities, although the exec call at the end might change capabilities. This ans that, if you are root, you probably want to do sothing like: