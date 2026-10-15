# EXAMPLE 1: DOCUMENTATION

```
```text
-f, --silent, --quiet  suppress most error messages
-R, --recursive         operate on files and directories recursively
-v, --verbose           explain what is being done
    --help              display this help and exit
    --version           output version information and exit

Owner is unchanged if missing. Group is unchanged if missing, but changed to login group
if implied by a period. A colon may replace the period.

Report bugs to fileutils-bugs@gnu.ai.mit.edu
```
```

# EXAMPLE 1.4

```
```text
(The Command Line)
1   $ ls -l filetest
    -rw-rw-r--  1 ellie  ellie       0 Jan 10 12:19 filetest
2   $ chown root filetest
    chown: filetest: Operation not permitted
3   $ su root
    Password:
4   # ls -l filetest
    -rw-rw-r--  1 ellie  ellie       0 Jan 10 12:19 filetest
5   # chown root filetest
6   # ls -l filetest
    -rw-rw-r--  1 root   ellie       0 Jan 10 12:19 filetest
7   # chown root:root filetest
8   # ls -l filetest
    -rw-rw-r--  1 root   root        0 Jan 10 12:19 filetest
```
```

# EXPLANATION

+   1. The user and group ownership of filetest is ellie.
+   2. The chown command will only work if you are the superuser, i.e., user root.
+   3. The user changes identity to root with the su command.
+   4. The listing shows that user and group are ellie for filetest.
+   5. Only the superuser can change the ownership of files and directories. Ownership of filetest is changed to root with the chown command. Group ownership is still ellie.
+   6. Output of ls shows that root now owns filetest.
+   7. The colon (or a dot) is used to indicate that after root will now change the group ownership to root. The group name is listed after the colon. There can be no spaces.
+   8. The user and group ownership for filetest now belongs to root.