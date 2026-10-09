The final example combines the – and –C options to show how to run a single command with root privileges in the root environment:

```
$ su -c pwd
Password:
/home/sam
$ su - -C pwd
Password:
/root
```

# **Root privileges, PATH, and security**

+   - **security**	The fewer directories you keep in **PATH** when you are working with **root** privileges, the less likely you will be to execute an untrusted program while working with **root** privileges. If possible, keep only the default directories, along with `/usr/bin` and `/usr/sbin`, in **root**'s **PATH**. _Never include the working directory in **PATH** (as `:` or `;` anywhere in **PATH** or as the last element of **PATH**). For more information refer to “PATH: Where the Shell Looks for Programs” on page 359.

# **LE+ Using sudo to Gain root Privileges**

If **sudo** (www.sudo.ws) is not set up so you can use it, and a **root** password exists and you know what it is, see “Administrator and the wheel group” on the next page for instructions on setting up **sudo** so you can use it to gain **root** privileges.

# ADVANTAGES OF sudo

Using **sudo** rather than the **root** account for system administration offers many advantages.

+   - When you run **sudo**, it requests _your_ password—not the **root** password— so you have to remember only one password.
+   - The **sudo** utility logs all commands it executes. This log can be useful for retracing your steps for system auditing and if you make a mistake.
+   - The **sudo** utility logs the username of a user who issues an **sudo** command. On systems with more than one administrator, this log tells you which users have issued **sudo** commands. Without **sudo**, you would not know which user issued a command while working with **root** privileges.
+   - The **sudo** utility allows implementation of a finer-grained security policy than does the use of **su** and the **root** account. Using **sudo**, you can enable specific users to execute specific commands—something you cannot do with the classic **root** account setup.
+   - Using **sudo** makes it harder for a malicious user to gain access to a system. When there is an unlocked **root** account, a malicious user knows the username of the account she wants to crack before she starts. When the **root** account is locked, the user has to determine the username _and_ the password to break into a system.