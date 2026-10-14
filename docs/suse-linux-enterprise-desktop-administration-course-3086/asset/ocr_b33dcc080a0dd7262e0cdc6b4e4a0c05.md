+   4. Which of the following files could you edit to create groups and add members to those groups?
+      a. `/etc/passwd`
+      b. `/etc/shadow`
+      c. `/etc/groups`
+      d. `/etc/group`

+   5. Which of the following files are used to obtain default user account settings when you create a user with the `useradd` command? (Choose all that apply.)
+      a. `/etc/default/useradd`
+      b. `/etc/skel`
+      c. `/etc/login.defs`
+      d. `/etc/useradd.default`

+   6. Which two of the following commands can be used to create the group `research` and add the user `dgrant` to it? (Each answer is part of the solution.)
+      a. `groupmod -A dgrant research`
+      b. `groupadd -p research`
+      c. `groupadd research`
+      d. `groupmod -A research dgrant`

+   7. Which of the following lines in `/etc/sudoers` will give the user `bob` the right to run the `useradd` command on all computers?
+      a. `bob /sbin/useradd = all`
+      b. `/sbin/useradd all = bob`
+      c. `bob all = /sbin/useradd`
+      d. `!/sbin/useradd bob = all`

+   8. Which of the following directory permissions gives the owner the ability to list the contents of the directory? (Choose all that apply.)
+      a. `rwxr-xr-x`
+      b. `rwxr--r-x`
+      c. `r-xrwxr-x`
+      d. `-w-rw-r-x`

9. What command could you use to change the owner to `dgrant` and the group owner to `research` for the file `/etc/config`? ____________

10. What command could you use to change the permissions on the file `/etc/config` to `rw-rw-r--` using numeric notation? ____________