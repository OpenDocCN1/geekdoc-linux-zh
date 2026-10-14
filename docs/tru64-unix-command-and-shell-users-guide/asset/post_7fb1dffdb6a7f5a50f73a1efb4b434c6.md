
- Login name
- Terminal name (line)
- Time of login
- Computer from which the network connection came

For example, user lennon might enter the who am i command at the system prompt ($) and read the following output:

```
% who -M am i
lennon     tty p0     Jul 15 14:17     (walrus)
```

In this example, user lennon logged in from host walrus at 2:17 in the afternoon of July 15. The line is tty p0, and walrus is the name for this line, from which the network connection came.

The who am i command can help you keep track of the sessions you have running on your workstation. Some sessions may be remote logins to another host by yourself or by someone with whom you are working. See the who(1) reference page for more information about the who am i command.

To find out if other users are logged in to the same local host, use the who command. In the following example, lennon enters the who command at the prompt of local host london, and learns that three other users are currently logged in to london from different nodes:

```
london$ who -M
lennon     tty p0     Jul 15 08:17     (walrus)
elvis      tty p2     Jul 15 07:55     (velvet)
burdon     tty p1     Jul 15 09:02     (animal)
sarjan     tty p4     Jul 14 16:47     (pepper)
```

The output from the who command is the same as that from the who am i command.

## 10.2 Obtaining Information About Network Users

The finger command and its options enable you to display information about users with accounts on local or remote hosts. The specified host must be running a fingerd daemon server or have the inetd daemon configured to start fingerd. See your system administrator if the finger command does not work as described in the finger(1) reference page.

The finger command has the following syntax:

```
finger [ [ option... ] [ user... ] [ user@host_name... ] ]
```

If you use the finger command without specifying an option or a user name, it lists the following information about all users on the local host where you are logged in, if the information is in the /etc/passwd file for a given user:

- Login name
- Full name
- Terminal line name and whether it can receive messages from other users through write (see Section 11.8) or talk (see Section 11.9)
- Idle time
- Login time
- User’s office location

### 10.2.1 Obtaining Information About a Specific User

If you specify the login name of a user on your local host, the finger command displays more information than if you entered the finger command without specifying a user name. The following additional information about the user is displayed:

- User’s home directory and login shell
- Contents (if any) of the .plan and .project files in the user’s home directory

The following example shows how to use the finger command to find information about user smith, who has an account on your local host:

```
％ finger smith
Login name: smith      (messages off)  In real life: John Smith
Office: LV05-3/724
Directory: /usr/netd/r2/smith             Shell: /bin/csh
On since Apr 9 16:20:56 on ttypb from wombat-lv5.dec.c
18 seconds Idle Time
Project: book "Communicating with Network Users"
Plan:
```

In the first line of output, messages off means that user smith has put the mesg n command in his .login file to prevent his terminal from receiving messages from other users through the write or talk commands, which can be distracting.

The preceding example also displays the contents of the .project file and the .plan file that user smith created in his home directory. The .project file can contain only one line. The .plan file can contain as many lines as the file system allows; finger will print all the lines until the end-of-file (EOF) is reached.

### 10.2.2 Obtaining Information About Users on a Remote Host

In the following example, the `finger` command displays information about users on the remote host `boston`:

```
% finger @boston
[boston]
Login      Name           TTY  Idle   When        Office
amy        Amy Wilson     p0   4      Thu 10:00   345
chang      Peter Chang    *p1  2:58  Thu 10:16   103
```

The first output line lists the remote host name, `boston`, and the second line describes the type of information in each column of the remaining output, each line allocated to one user. The asterisk (*) indicates that user `chang` has put the command, `mesg n` in his `.login` file to prevent his terminal from receiving messages from other users through the `write` or `talk` commands.

### 10.2.3 Obtaining Information About an Individual User on a Remote Host

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

### 10.2.4 Customizing Output from the finger Command

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
