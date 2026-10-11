Some users find it annoying to have to constantly enter their passphrase when connecting to a remote host. To help alleviate this problem, they can use the `ssh-agent` and `ssh-add` tools. The `ssh-agent` tool is used to hold private keys for public key authentication. The normal procedure is that `ssh-agent` is started at the beginning of a login or X11 session, and all other applications or windows are clients. From any of these clients, an SSH session can be made to a remote system, and the passphrase must be entered only once. The syntax for `ssh-agent` is as follows:

```
```
ssh-agent command args ...
      ssh-agent [-c | -s]
      ssh-agent -k
```
```

Table 17-10 lists the `ssh-agent` command-line options.

| Option | Function |
| :--- | :--- |
| -C | Generates C Shell commands. This is the default if the shell looks to be a C-like shell. |
| -s | Generates Bourne commands. This is the default if the shell does not look to be a C-like shell. |
| -k | Kills the current `ssh-agent` process. |

The agent does not open any keys by itself; they are loaded with the `ssh-add` tool. To open a new shell with the `ssh-agent` you can use the following:

```
```
ssh-agent $SHELL
```
```

This causes all connections made from the shell to be handled by the agent. To start X11 with agent support you can use the following:

```
```
xsh-agent startx
```
```

This way any SSH connections made from within X11 will use the agent and not require the passphrase. To add your private keys to `ssh-agent`, use `ssh-add`. The syntax is as follows:

```
```
ssh-add [-lLdD] [file...]
```
```

Table 17-11 lists the command-line options for `ssh-add`. If no options are specified, `ssh-add` loads all private keys for the current user from `~/.ssh/identity` and prompts him or her for his or her passphrase if he or she has one.