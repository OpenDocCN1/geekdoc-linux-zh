
> With Linux being open source software, just about all its components are freely available in source code format. A hacker would just need to modify some SUID program, such as ping or passwd, and wait for it to spawn a hidden root SUID shell when executed.
>
> As an administrator, you should check frequently to see whether any previously disabled service is suddenly active and review the contents of the configuration files for unfamiliar changes. The popular targets are services that use privileged ports (ports lower than 1024) because they generally run as root. Any service that runs as root, however, is a potential target.

Often, an application’s configuration file is set to be group-readable and -writable. At the same time, some applications store passwords in cleartext in their configuration files. Furthermore, human nature suggests that the probability of someone (such as the system administrator) using the same password for server login and application login is high. Therefore, if a hacker gains access to the unprivileged account named eric, there is a chance that the hacker can locate the root password in one of the group-owned files that Eric has access to.

First, after the hacker logs in using account eric, he can find out the groups Eric belongs to by using the id command:

```text
$ id
uid=1001(eric) gid=100(users) groups=100(users),201(web)
```

After noticing Eric belongs to the group named web, the hacker can then use the find command to locate all files owned by that group:

```text
$ find / -group web -print 2> /dev/null
/projects/web/README
/projects/web/password.txt
/projects/web/index.html
/projects/web/passwd.txt.backup
```

And the two passwd.* files may prove interesting!

From the information in the password files, the hacker may gain access to other accounts, which may in turn lead to more passwords. As the cycle goes on, the hacker may eventually gain root access. Therefore, it is very important that good security procedures be devised and enforced. (Refer to the “Corporate Security Policies” section in Chapter 11, “Network Security Concepts,” for more information.)

## Default Access Permissions

When a user creates a file or directory, a permission mask, known as the umask setting, controls the final permissions assigned. The umask is a built-in shell function that removes (“masks out”) certain permission bits set by a program. A file or directory ends up with its permission bits as follows: When a file is newly created, the kernel assigns it a permission mode of 666 (rw-rw-rw-), and a directory gets 777 (rwxrwxrwx). But before the permissions are actually set, the umask value is applied. The umask value is specified the same way as chmod: first, use the mask, then the group mask; finally, all others (the special mode mask is skipped for now). So, if the umask value is 022, the final file permission setting is 644 (rw-r--r--). It is often stated that this is as a result of subtracting the umask value from the default permission setting. While the final result in this example reflects such an assertion—and makes it easier to remember the process—the actual mechanics do not work exactly like this. (For example, what if the umask is 027?)

What actually happens is that the requested permission setting (666 in the example) is logically ANDed with the one's complement (that is, it is bit-flipped) of the umask value. Shown in Table 6.5 is the “truth table” for logical AND operations; for example, 0 & 0 results in 0, 1 & 1 results in 1, and so on.

**TABLE 6.5**

**Logical And Truth Table**

| & | 0 | 1 |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |

When you're working with logical AND operations, it is easier to work in binary mode. Table 6.6 illustrates how the default permission value of 666 is “masked” by the umask setting of 022.

**TABLE 6.6**

**Logical And of One's Complement of umask Values with Default Permissions**

|  | U | G | O |
|---|---:|---:|---:|
| umask setting of 022 | 000 | 010 | 010 |
| One's complement of the umask value | 111 | 101 | 101 |
| Default permission of 666 | 110 | 110 | 110 |
| Applying logical AND |  |  |  |
| Result | 110 | 100 | 100 |
| Decimal value | 6 | 4 | 4 |

As mentioned earlier, what if your umask is 027? The subtraction concept isn't applicable now; is it? The “proper mechanics” discussed here show that the resulting permission setting is 640, as illustrated in Table 6.7.

**TABLE 6.7**  
*File Permission Setting Using a umask of 027*

|  | U | G | O |
|---|---:|---:|---:|
| umask setting of 027 | 000 | 010 | 111 |
| One's complement of the umask value | 111 | 101 | 000 |
| Default permission of 666 | 110 | 110 | 110 |
| Applying logical AND |  |  |  |
| Result | 110 | 100 | 000 |
| Decimal value | 6 | 4 | 0 |

SLES sets the default umask value (022) in `/etc/profile`. Therefore, when a user starts a shell (such as by logging on to the server), this value is automatically set. Furthermore, a new child process gets the umask value (and other shell information) from its parent process. However, after the process is spawned, it is free to change its shell environment, such as the umask setting—and these changes are not propagated back to its parent or other existing child processes. If you want to change your umask, you can include the command `umask mask_value` in your home directory's `.profile` or one of the configuration files used by the shell (such as `.bashrc`) so that it takes effect whenever you log in or start a new shell.

Keep in mind that with a umask of 022, system applications (such as vi and mkdir) will create files with 644 (rw-r--r--) permissions and directories with 755 (rwx-r-xr-x). The world could read (thus copy) the newly created files and directories. This may not be a good idea if you also have guest users from outside your company accessing your server. A better default umask setting is 027. Such a umask would eliminate all world access to any newly created files and directories. You can later selectively make some available to the world using chmod.

## CAUTION

Any user or process may set the umask for its shell. So, even if you put in the more restrictive umask 027 in `/etc/profile`, any user can easily override it with a less restrictive setting. Because umask is a built-in shell function, you cannot easily restrict it from general use; you need to create a custom shell by compiling the modified source code to do that. It is best to educate your users that the more restrictive setting is in everybody's best interest and should not be changed.

SLES includes a number of tools to help you maintain system file and directory permission integrity. For instance, the seccheck (SUSE Security Checker) package can report on executables that are group-and/or world-writable. YaST includes a Local Security Configuration module (Control Center, Security and Users, Security Settings; or yast security from a terminal session) that configures the level of file permissions as Easy, Secure, or Paranoid. You can use SuSEConfig to set or reset file permissions accordingly—using specifications according to /etc/permissions*.

## Special File Permissions

In addition to the basic permissions discussed earlier, you can also set three special permission bits on files and directories:

- **SUID bit**—Generally referred to as the SUID bit because of the name of the API call used, this bit changes the user ID on execution. When a program is executed with the SUID bit set, the process will have the same rights as the owner of the file being executed.

- **SGID bit**—Generally referred to as the SGID bit because of the name of the API call used, this bit changes the group ID on execution. It operates the same as the SUID bit but inherits rights of the group of the owner of the file. If set on a directory, it means that when a new file is created in the directory, the new file’s group owner will be the same as the directory’s group owner.

> **NOTE**
>
> Because of shell scripts’ inherent lack of tight security, Linux has disabled the SUID/SGID support for them: You can set the bits, but they have no effect. Should you have the need for a SUID/SGID script, use Perl instead. See man perlsec for more information.

- **Sticky bit**—In older Unix kernels, this bit was used to trigger a program to “stick” in memory after it is finished (so the next time the application is executed, it is already in memory); now this usage is obsolete with the advent of virtual memory. When set on a directory, the sticky bit ensures nonroot users can only delete files they own in that directory. The sticky bit is applicable only to the world permission setting of a directory; it has no effect when applied to a file.
