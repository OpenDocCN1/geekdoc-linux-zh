![](bbox=[0.09, 0.16, 0.17, 0.26])

Remember that superusers (UID = 0, GID = 0) have access to everything in the system, and thus these are very sensitive accounts that should only be used when necessary.

# Using sudo to perform root tasks by ordinary users

The sudo command enables ordinary users to execute commands that are typically run by a superuser. As an example of how this could be useful, suppose that you are the chief system administrator for your organization and have just been blessed with two new assistant system administrators, to whom you want to delegate some of your routine administrative tasks. While you could create two new superuser accounts with UIDs and GIDs set to 0 for the new administrators, whether you do so or not depends on how confident you are in their ability to be as careful as you are when working as the ultimate user. Because confidence is something that requires a certain amount of time to build, you would probably want to allow these new administrators access only to what they need to have access to. To do this, you need to configure the sudo command, which allows users specified in the /etc/sudoers file to run superuser commands. For example, an ordinary user who is permitted to run superuser commands via sudo can run the following to modify the /etc/passwd file:

```
sudo vi /etc/passwd
```

The sudo program is very configurable, so you can custom-tailor what an ordinary user who is listed in /etc/sudoers can or cannot do. The /etc/sudoers files have the following types of lines:

+   - **Blank and comment lines (starting with #).** This information is for humans only. The sudo program ignores these lines.
+   - **Optional host alias lines.** These are used to create short names for the list of hosts. A host alias line must start with the Host_Alias keyword, and the hosts in the list must be separated by commas. For example, in the following line, wormhole and blackhole are two hosts that can be called REDHAT:
+   
+       Host_Alias REDHAT=wormhole,blackhole