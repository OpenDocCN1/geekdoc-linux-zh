Each of these components are explored in the following sections.

# Linux Users

As with other multiuser operating systems, Linux uses user accounts. During the installation of a Linux system, one user account is always created by default: root.

The root user account has full access to the entire system. Anyone logged in as root can open, modify, copy, or delete any file in the file system. This user account has a great deal of power and must always be used with discretion.

As mentioned earlier in this book, you should never log in as root to perform routine, day-to-day work. This rule prevents two problems. First, it eliminates the possibility of someone using your root account to wreak havoc on your system while you're away from your desk. Second, it keeps you from accidentally wreaking havoc on your own system. I'll explain why later in this chapter.

For these reasons, you should always log in as a regular system user to conduct your normal tasks on the system. When you need root-level access, use the `su` - command at the shell prompt to switch to the root account. When you're done, be sure to switch back to your regular account with the `exit` command at the shell prompt.

Most Linux installation routines provide you with the ability to create one or more regular user accounts during installation.

> **TIP**
> Some Linux distributions will *require* that you create at least one regular user account during installation.

After installation, you can use YaST2 on a SUSE system to create new user accounts. If you're working from within GNOME or KDE, just select **Applications, SUSE Menu, System, YaST2**.

When you do, the YaST Control Center appears. Select **Security and Users** and then select **Edit and Create Users**. The *User and group administration* screen appears, as shown in Figure 3.1.

> **TIP**
> If you are working within a nongraphical session, you can enter `yast2` at the shell prompt.

To create a new user, select **Add**. To modify an existing user, select **Edit**. To delete an existing user, select **Delete**.