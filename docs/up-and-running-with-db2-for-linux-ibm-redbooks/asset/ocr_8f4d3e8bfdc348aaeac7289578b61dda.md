# Table 2-4 Package requirements for SuSE

| Package name | RPM name | Description |
|---|---|---|
| pdksh | pdksh-5.2.14-293.i386.rpm (for V7.2)
pdksh-5.2.14-515.src.rpm (for V8) | Korn Shell. This is required for multi-partitioned database environments. |
| rsh-server | rsh-0.17-214.src.rpm (for V7.2)
rsh-0.17-285.src.rpm (for V8) | Contains a set of server programs which allow users to run commands on remote machines, login in to other machines, and copy files between machines (rsh, rexec, rlogin, and rcp) |
| nfs-utils | nfs-utils-0.3.3-109.src.rpm (for V7.2)
nfs-utils-1.0.1-26.src.rpm (for V8) | Network File System support package. It allows access for local files to remote machines. |

# Table 2-5 Package requirements for Red Hat

| Directory | Package name | RPM name | Description |
|---|---|---|---|
| /System Environment/Shell | pdksh | pdksh-5.2.14-13.i386.rpm (for V7.2)
pdksh-5.2.14-19.i386.rpm (for V8) | Korn Shell. This is required for multi-partitioned database environments. |
| /System Environment/Daemons | rsh-server | rsh-0.17-5.i386.rpm (for V7.2)
rsh-0.17-10.src.rpm (for V8) | Contains a set of programs which allow users to run commands on a remote machine. Required for multiple-partition environments. |
| /System Environment/Daemons | nfs-utils | nfs-utils-0.3.3-5.src.rpm (for V7.2)
nfs-utils-1.0.1-2.src.rpm (for V8) | Network File System support package. It allows access for local files to remote machines. |