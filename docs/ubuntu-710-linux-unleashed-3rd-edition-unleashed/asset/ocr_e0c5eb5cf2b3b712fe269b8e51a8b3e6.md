This setting allows normal users to execute the command (as root) to make changes to a root-only accessible file, /etc/passwd.

You also can assign similar permission with the chfn command. This command allows users to update or change finger information in /etc/passwd. You accomplish this permission modification by using a leading 4 (or the mnemonic s) in front of the three octal values.

> NOTE
> Other files that might have suid or guid permissions include at, rcp, rlogin, rsh, chage, csh, ssh, cron tab, sudo, sendmail, ping, mount, and several Unix-to-Unix Copy (UUCP) utilities. Many programs (such as games) might also have this type of permission to access a sound device.

Files or programs that have suid or guid permissions can sometimes present security holes because they bypass normal permissions. This problem is compounded if the permission extends to an executable binary (a command) with an inherent security flaw because it could lead to any system user or intruder gaining root access. In past exploits, this typically happened when a user fed a vulnerable command with unexpected input (such as a long pathname or option); the command would fail, and the user would be presented a root prompt. Although Linux developers are constantly on the lookout for poor programming practices, new exploits are found all the time, and can crop up unexpectedly, especially in newer software packages that haven’t had the benefit of peer developer review.

Savvy Linux system administrators keep the number of suid or guid files present on a system to a minimum. The find command can be used to display all such files on your system:

```
# find / -type f -perm +6000 -exec ls -l {} \;
```

> NOTE
> The find command is quite helpful and can be used for many purposes, such as before or during backup operations. See the section “Using Backup Software” in Chapter 13, “Backing Up.”

Note that the programs do not necessarily have to be removed from your system. If your users really do not need to use the program, you can remove the program’s execute permission for anyone. You have to decide, as the root operator, whether your users are allowed to, for example, mount and unmount CD-ROMs or other media on your system. Although Linux-based operating systems can be set up to accommodate ease of use and convenience, allowing programs such as mount to be suid might not be the best security policy. Other candidates for suid permission change could include the csh, at, or chage commands.