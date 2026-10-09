| Login Level | Description |
| :--- | :--- |
| Root login | The root user is considered a specific user account, with a UID of 0. It has privileges that no other user on the system has. |
| | Specifically, the root user can navigate anywhere on the system, change any file, and manipulate system controls, including user accounts, storage devices, and kernel parameters. |
| | The system administrator(s) will generally have his or her own user accounts with normal user privileges, and the root account. As a rule of thumb, you should do as much as possible under your own UID before working from the root user account. |
| User login | User accounts must be created with security in mind. The user name, or login ID, and the password are stored in two different files, /etc/passwd and /etc/shadow, and are set up with restricted access rights for added security. |
| | The user account file, /etc/passwd, is set up to be read-only by everybody except the root user. |

# Alias for the Root User

If you are using the Bash shell, you can create an alias for root as a precautionary measure. An alias, in this case, is an entry in the `.bashrc` file where you can define additional actions for specific default commands. For example, the `rm` command, which is used for removing or deleting files, can be given an alias that prompts you for additional information, based on the criteria you set.

![](bbox=[0.05, 0.62, 0.17, 0.67])

# The su Command

The *substitute or switch user* command (*su*) is used to change the ownership of a login session without logging out. It is generally used to switch ownership between an ordinary user and a root user, to change access permissions for administrative work.