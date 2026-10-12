# # Assigning Privileges to Ordinary Users

Using the sudo command, you can allow ordinary users to execute commands that are typically run by a superuser. Suppose that you are the chief system administrator for your organization and have just been blessed with two new assistant system administrators, to whom you want to distribute some of your routine administrative tasks. Should you create two superuser accounts with UIDs and GIDs set to 0, so that these two administrators can have full access to everything, as you do? That depends on how confident you are in their ability to be as careful as you are when working as the ultimate user. Because confidence is something that requires a certain amount of time to build, you probably want to allow them access only to what they need to have access to, and thus need to configure sudo to allow these individuals to run privileged commands as regular users. Here is how.

The sudo command allows users specified in the /etc/sudoers file to run superuser commands. For example, an ordinary user who is permitted to run superuser commands via sudo can run the following:

```
`sudo vi /etc/passwd`
```

This allows this user to modify the /etc/passwd file. The sudo program is very configurable, so you can custom-tailor what an ordinary user who is listed in /etc/sudoers can or cannot do. The /etc/sudoers files have the following types of lines:

+   - **Blank and comment lines** (starting with `#`), ignored lines.

+   - **Optional host alias lines**. Used to create short names for the list of hosts. A host alias line must start with the `Host_Alias` keyword, and the hosts in the list must be separated by commas. For example, in the following line,

```
`Host_Alias REDHAT=wormhole,blackhole`
```

wormhole and blackhole are two hosts that can be called REDHAT.