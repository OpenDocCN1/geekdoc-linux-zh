plify the compilation and installation of the suite. The Am-utils suite provides greater support for diverse filesystem types, selector variables, and mount map types than the automounter.

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