To create a guest account, first create a user and the home directory for it. You then create an Anonymous block in the proftpd.conf file for that account. The Anonymous directive includes the home directory of the guest user you create. You can specify this directory with a ~ for the path and the directory name, usually the same as the username. Within the Anonymous block, you use the User and Group directives to specify the user and group name for the user account. Set the AnonRequirePassword directive to on if you want remote users to provide a password. A UserAlias directive defines aliases for the username. A remote user can use either the alias or the original username to log in. You then enter the remaining directives for controlling access to the files and directories in the account's home directory. An example showing the initial directives is listed here. The User directive specifies the user as myproject. The home directory is ~myproject, which usually evaluates to /var/myproject. The UserAlias lets remote users log in with either the name myproject or mydesert.

```
<Anonymous ~myproject>
    User myproject
    Group other
    UserAlias mydesert myproject
    AnonRequirePassword on
    <Directory *>
```

You could just as easily create an account that requires no password, letting users enter in their e-mail addresses instead. The following example configures an anonymous user named mypics. A password isn't required, and neither is a valid shell. The remote user still needs to know the username, in this case mypics.

```
<Anonymous /var/mypics>
    AnonRequirePassword off
    User mypics
    Group nobody
    RequireValidShell off
    <Directory *>
```

The following example provides a more generic kind of guest login. The username is guest, with the home directory located at ~guest. Remote users are required to know the password for the guest account. The first Limit directive lets all users log in. The second Limit directive allows write access from users on a specific network, as indicated by the network IP address, and denies write access by any others.

```
<Anonymous ~guest>
    User            guest
    Group           nobody
    AnonRequirePassword     on
    <Limit LOGIN>
        AllowAll
    </Limit>
    # Deny write access from all except trusted hosts.
    <Limit WRITE>
        Order           allow,deny
        Allow           from 10.0.0.
        Deny            from all
    </Limit>
</Anonymous>
```

# Virtual FTP Servers

The ProFTPD daemon can manage more than one FTP site at once. Using a VirtualHost directive in the