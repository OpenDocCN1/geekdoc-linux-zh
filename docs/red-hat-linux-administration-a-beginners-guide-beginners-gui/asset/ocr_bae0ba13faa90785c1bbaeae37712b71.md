This specifies whether root can log in using **ssh**. The default is “yes,” but some sites prefer to disallow this (by specifying “no”) for an added measure of security. There is also the possibility of setting this to **without-password**, which restricts root to public authentication, even if other users are allowed password-based logins. Finally there is a **forced-commands-only** option that can be handy for administrative scripts, as it allows root to execute certain commands through **ssh**, but not to log in interactively.

```
DenyUsers john sally * @windows.domain.com
```

The default is to allow all users with accounts on the machine to log in. You can restrict some of them from being able to log in with the **DenyUsers** option. The wildcard characters * and ? can be used, and you can also specify *user@host* for more fine-grained denials.

```
AllowUsers amy anie rachael@gorey
```

This is similar to the **DenyUsers** option, except that it reverses the sense. The default becomes to deny users except those specified here.

```
X11Forwarding yes
```

Enabling this allows users logged in to this machine to launch X-based applications and have them tunneled down the encrypted connection for display on their local workstations. Turning this off doesn’t really add any security, as there are other ways to accomplish the same task. Nevertheless the default is “no.”

```
StrictModes yes
```

Specifies whether **sshd** should check file modes and ownership of the user’s files and home directory. If the permissions are too lax, **sshd** will deny them login. The default for this is “yes.”

```
UsePrivilegeSeparation yes
```

Privilege separation is a new feature in OpenSSH. It tries to enhance security by having an unprivileged process listen for connections, and only after the user is authenticated does a process get created with the permissions of the authenticated user. The idea is to limit how much damage can be caused if a new vulnerability is discovered in the listening process. Although this is a really cool idea, it doesn’t play well with some **pam** configurations. The default is “yes.”