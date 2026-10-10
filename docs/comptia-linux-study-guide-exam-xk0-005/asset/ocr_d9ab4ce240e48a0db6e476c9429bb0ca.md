5. Tarissa needs to run a shell script, which has the permissions of `rwxr--r--`, is owned by **root**, and belongs to the `wheel` group. Tarissa's user account is T2T1080, and she is a member of the admin group. What can be done to allow her to run this script? (Choose all that apply.)

+   * **A.** Add Tarissa to the `wheel` group.
+   * **B.** Create a new account for Tarissa named `wheel`.
+   * **C.** Add **w** to the script file's group permissions.
+   * **D.** Add **x** to the script file's group permissions.
+   * **E.** Nothing. Tarissa can run the script now.

6. Miles needs to change his present working directory to the `/home/miles` directory. He does not own the directory, nor is he a member of its group. Assuming needed parent directory permissions are set, what needs to take place for this to successfully occur?

+   * **A.** Nothing. The `/home/miles` directory is Miles's home directory, so he can access it by default.
+   * **B.** The execute (x) permission needs to be added.
+   * **C.** The write (w) permission needs to be added.
+   * **D.** The read (r) permission needs to be added.
+   * **E.** The dash (–) permission needs to be added.

7. Sarah, a system administrator, attempts to create a file and receives an error message indicating the file cannot be created. Which of the following might be the problem? (Choose all that apply.)

+   * **A.** The filesystem on which she is attempting to create the file has quotas set, and she is past her quota and grace period.
+   * **B.** The filesystem on which she is attempting to create the file has run out of space.
+   * **C.** The file that she is attempting to create has the immutable bit set and therefore cannot be created.
+   * **D.** The action is triggering either a SELinux or an AppArmor policy violation.
+   * **E.** The filesystem is experiencing inode exhaustion and therefore cannot accommodate any new files.

8. A user cannot delete one of their files but is able to delete other files in their directory. John, a system administrator, is attempting to troubleshoot this issue. What command should he use first on the file?

+   * **A.** `chown`
+   * **B.** `chattr`
+   * **C.** `chmod`
+   * **D.** `umask`
+   * **E.** `lsattr`