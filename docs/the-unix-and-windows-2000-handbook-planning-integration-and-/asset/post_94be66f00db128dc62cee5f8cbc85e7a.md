
Especially useful feature for the system administrator when performing maintenance and upgrading software. The second entry in the `auto_master` defines the mount parameters for `/home`. When attempting to mount directories under `/home`, the automounter is directed to use the `auto_home` map, which is shown here.

```
#
#/etc/auto_home
#
local       -bg    earth:/usr/local
*           -bg    saturn:/home/users/&
```
```

By directing automountd to `auto_home`, we can customize how the automounter should act for the `/home` directory. In the example, `/etc/auto_home`, the first entry, directs automountd to mount `/home/local` from `earth:/usr/local` while running in the background. The second entry uses wildcard entries `*` and `&`. The `*` tells the automounter what to do with requests that are not explicitly defined in the map. The `&` is an expansion wildcard that expands the current request into the mount definition. For example, if user `ralph` attempts to mount `ralph`'s home directory using the command:

```
```
mars# cd /home/ralph
```
```

The automounter looks in the `auto_home` map and sees that `ralph` is not explicitly defined. All undefined requests are expanded using the `saturn:/home/users/&` entry. By replacing the `&` with `ralph`, `mars` will attempt to mount the filesystem `/home/users/ralph` from the system `saturn`.

If `/home/users/ralph` exists and is shared, it will be mounted; otherwise, `ralph` will see a “directory not found” error. As long as the filesystem has activity, it will remain mounted. After some period of time (the default time is generally five minutes), the automounter will attempt to unmount the filesystem as long as there is no activity.

No user intervention is necessary, and better yet, no root user intervention is needed. By releasing the NFS file-system, there is less chance for an NFS problem. You also reduce the resources necessary to manage NFS on the client system.

## Am-utils: 4.4BSD Automounter Utilities

The Am-utils comprise a suite of automounter tools that can be used in place of Sun’s automounter. The suite includes `amd`, the automounter daemon, and `amq`, the automounter query tool. Am-utils have been ported to AIX, HP-UX, Linux, and Solaris. They are available in source or binary form for each platform. The source provides configuration tools that greatly simplify the compilation and installation of the suite. The Am-utils suite provides greater support for diverse filesystem types, selector variables, and mount map types than the automounter.

Amd is the automounter daemon that mounts filesystems when a file or directory is accessed. The startup scripts discussed in Chapter 2, "System Planning, Installation, and Configuration," must be searched and modified to start amd in place of automountd. In the following example, amd reads configuration information from /etc/amd.conf on initialization. The file contains parameters and sections to govern the behavior of amd. Information is limited to one line and is case-sensitive. Parameters can be common to all sectors, or are only applicable to the global section. The man pages for amd.conf provide details on all valid parameters. There are two main sections: global and map.

Sections begin with the name of the section in square brackets and end when a new section begins or the file ends. The global section, which should be placed first in the file, applies to amd (in place of command-line switches) and all following map sections where applicable. The map section parameters apply only to a specific map entry. Parameters specified in the map section override parameters defined in the global section.

```
#
# amd default config file
#
# check amd.conf(5) man page for details about options in this file
#
# GLOBAL OPTIONS SECTION
[ global ]
normalize_hostnames =  no
print_pid =           yes
pid_file =            /var/run/amd.pid
restart_mounts =      yes
auto_dir =            /.automount
log_file =            /var/log/amd
#log_file =           syslog
log_options =         all
#debug_options =      all
plock =               no
selectors_on_default = yes
print_version =       no
# set map_type to "nis" for NIS maps, or comment it out to search for all
# types
map_type =            nis
```
