# Backups and Crash Recovery (continued)

| BOX | SYMPTOM | PAGE |
|---|---|---|
| 97 | Tape capacity exceeded. Underused tape capacity. | 200 |
| 98 | Client host denies access. | 203 |
| 99 | Amanda backups fail, rejecting the name of the tape. Amanda writes to the wrong tape. | 204 |
| 100 | The kernel can't find the disk or the CD-ROM drive. | 209 |
| 101 | fsck can't find a superblock or filesystem on a partition. | 212 |
| 102 | You're unable to remount / read-only. | 212 |
| 103 | Even though the filesystem is clean, a “maximal mount count exceeded” error forces full fsck at every boot, causing long boot times. | 213 |
| 104 | Even though you shut down the machine properly, the filesystem is always dirty upon reboot and requires a check. | 213 |
| 105 | You don't know the root password. Commands say they don't know who you are and ignore /etc/passwd. | 215 |
| 106 | The boot fails after mounting the root filesystem. You get a partial boot. | 216 |

# User Environments

| BOX | SYMPTOM | PAGE |
|---|---|---|
| 107 | The exit in a .profile (or some other startup file) unexpectedly logs you out. | 218 |
| 108 | Users wonder where environment variables come from and complain about being forced to use the default system startup files. | 219 |
| 109 | “Spontaneous file creation” confuses users. | 221 |
| 110 | You experience frustration and rage at users when they ask you to restore files they removed. | 222 |
| 111 | Interactive shell commands in .cshrc unexpectedly run upon startup of noninteractive shells. | 230 |
| 112 | Users log in (with xml login) and get kicked out again. | 232 |
| 113 | You get kicked out of an X session without running the .xsession. | 232 |
| 114 | Lingering processes (Netscape and FwmTaskBar are big culprits here). | 235 |
| 115 | Applications look hideous. You encounter unexpected changes in applications other than the one you're trying to modify. X applications stop working. | 236 |