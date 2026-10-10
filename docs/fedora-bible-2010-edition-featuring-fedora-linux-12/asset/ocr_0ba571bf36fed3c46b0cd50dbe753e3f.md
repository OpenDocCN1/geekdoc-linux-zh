+   * **Specify user ID manually** — Typically, you would not check this box, so that the UID for the new user would be assigned automatically. New UIDs for regular users start at 500. However, if you want to assign a particular UID for a user (for example, if you want to match the UID with the user’s UID from another computer on your network), select this box and type the number you want to use in the UID box.
+   * **Specify group ID manually** — As with the user ID, you would typically just have the group ID automatically assigned. However, you can assign a different GID to have the user assigned to a particular group.

+   3. Click OK when you are done. The new user is added to the /etc/passwd and /etc/group files. The user account is now available for that user to log in.

> **TIP:** Fedora uses a user private group (UPG) scheme, which makes Unix groups easier to use. The UPG scheme does not add or change anything in the standard UNIX way of handling groups; it simply offers a new convention. Whenever you create a new user, by default, that user has a unique group. You can extend this scheme for sharing files among several users. Here’s an example:
> ```bash
> # useradd -m projectx
> # mkdir /usr/local/x
> # chown root.projectx /usr/local/x
> # chmod 2775 /usr/local/x
> # ls -ld /usr/local/x
> drwxrwsr-x 2 root projectx 4096 Aug 18 01:54 /usr/local/x
> # passwd -a nextuser projectx
> ```
> In this example, you create a user named projectx (with a group named projectx). Create a /usr/local/x directory and have it owned by root user and the projectx group. Set the setgid bit to be on for the group (2), open full read/write/execute permissions for user and group (77), and open read and execute permissions for everyone else (5). Add each user to the group that you want to be able to write to the projectx directory (replace nextuser with the user you want to add). After that, regardless of a user’s primary group, any file created in the /usr/local/x directory by a user can be read or modified by anyone in the projectx group.

# # Setting User Defaults

The useradd command and User Manager window both determine the default values for new accounts by reading the /etc/login.defs and /etc/default/useradd files. You can modify those defaults either by editing those files manually with a standard text editor or by running the useradd command with the -D option. If you choose to edit the files manually, here is what you face:

```
```
# *REQUIRED*
# Directory where mailboxx reside, or name of file, relative to the home directory. If you _do_ define both, MAIL_DIR takes precedence.
```
```