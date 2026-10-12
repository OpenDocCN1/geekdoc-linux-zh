easy to perform administrative duties without hassle. However, the system assumes you know what you are doing, and will do exactly what you request—no questions asked.
Therefore, it is easy with a mistyped command to wipe out crucial system files. When you are logged in as or acting as root, the shell prompt displays # as the last character (if you are using bash). This is to serve as a warning to you of the absolute power of this account.

The rule of thumb is, never sign in as root unless absolutely necessary. While root, type commands carefully and double-check them before pressing Enter. Sign off from the root account as soon as you have accomplished the task you signed on for. During the install, you can create normal user accounts at the same dialog box that allows you to set the root password. It is advised that you set an account up here and use it all the time rather than the root account.

You may also set up other user accounts at this time as well. It is suggested that you set up at least one other user account—at this time. Enter in the account name as well as the password. You may also include the full name of this person as well. Click Add to accept the user. If you want to edit a user you create, just highlight the account name and click Edit. You may also delete any users here.

Press Next to continue.

# ### Authentication Configuration

Additional authentication configuration settings follow the setting of root's password. The first two choices have to do with added password security. It is recommended that you at least turn on shadow passwords, if not both shadow passwords and MD5 passwords. This is highly important—not using encrypted passwords means that hackers who have a field day if they gain access to your computer. In today's environment, with many people having a permanent connection to the Internet, it means that your computer is viewable to more or less the whole world, including hackers.

You are asked if you want to have NIS enabled. If you do, you also need to supply the NIS domain and server. (See Chapter 15, “NIS: Network Information Service.” for more information on NIS.) You also get the option of choosing to have the system request services via a broadcast instead of providing a server name.

You may also enable Lightweight Directory Access Protocol (LDAP). If you do you will be asked to enter in the LDAP server and the LDAP base distinguished name (DN).

The last option you have is to enable Kerberos. You may enter the realm, Key Distribution Center (KDC), and admin server that apply.

Press Next to continue to select the package groups.