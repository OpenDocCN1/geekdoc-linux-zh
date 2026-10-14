# 10.2.2 Obtaining Information About Users on a Remote Host

In the following example, the `finger` command displays information about users on the remote host `boston`:

```
% finger @boston
[boston]
Login      Name           TTY  Idle   When        Office
amy        Amy Wilson     p0   4      Thu 10:00   345
chang      Peter Chang    *p1  2:58  Thu 10:16   103
```

The first output line lists the remote host name, `boston`, and the second line describes the type of information in each column of the remaining output, each line allocated to one user. The asterisk (*) indicates that user `chang` has put the command, `mesg n` in his `.login` file to prevent his terminal from receiving messages from other users through the `write` or `talk` commands.

# 10.2.3 Obtaining Information About an Individual User on a Remote Host

To display information about user `luis` on remote host `havana` use the following `finger` command:

```
% finger luis@havana
Login name: luis                     In real life: Luis Aguilera
Directory: /users/luis               Shell: /bin/csh
On since May 24 10:16:07 on tty p2 from :0.0
58 minutes Idle Time
Project: baseball game simulation software
Plan:
Distribute with linked statistics module.
```

# 10.2.4 Customizing Output from the finger Command

There are several options to the `finger` command that enable you to modify the output according to the data you need. Table 10-1 lists and describes each option.

# Table 10-1: Options to the finger Command

| Option | Description |
|--------|-------------|
| -b     | Produces a brief version of output |
| -f     | Suppresses display of titles of each field |
| -h     | Suppresses printing of users' `.project` files |
| -i     | Displays list of users with idle times |
| -l     | Produces long format of output despite other options |
| -m     | Assumes that `user` is an account name |