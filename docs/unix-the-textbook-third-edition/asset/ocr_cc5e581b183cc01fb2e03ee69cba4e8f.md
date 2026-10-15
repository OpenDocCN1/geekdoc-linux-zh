Output: User information extracted from the ~/.project and ~/.plan files
Commonly used options/features:
  -m Match user_list to login names only
  -s Display output in a short format

The following session shows the simplest use of the command in which information about a user, Birch Tree, on the host is displayed.

```
% finger Birch
Login: tree                          Name: Birch Tree
Directory: /usr/home/tree            Shell: /bin/csh
On since Sat Oct 18 21:55 (PKT) on pts/1 from 102.102.241.10
No Mail.
Plan: To become an informed and efficient UNIX user.
%
```

You can use the finger command with the -s option to display the command's output in a short format and the -m option to match user-list to login names only. The finger -m Tree command displays the same information as the finger Birch command if the login name of the user is tree (uppercase and lowercase letters are considered the same by the networking commands). However, if the login name of the user is btree and the login name birch does not exist in the system, the finger command displays the message informing you accordingly.

When run without any argument, the finger command returns the status of all the users who are currently logged on to your machine. The amount of information displayed varies somewhat, depending on the UNIX system that your host runs. The following command runs are on PC-BSD and Solaris systems, respectively.

```
% finger
Login      Name                 TTY   Idle  Login Time     Office Phone
davis      James Davis          pts/0  1d    Aug 14 09:45
sarwar     Mansoor Sarwar       pts/1          Tue      22:43
%
```

```
$ finger
Login      Name                 TTY     Idle    When        Where
root       Super-User          console 7:09  Sat 16:39
sarwar     Mansoor Sarwar       pts/1           Wed 03:50  39.59.92.15
$
```

You can use the finger command to display information about a user on a host on the Internet, provided the host offers the finger service and has the finger server (fingerd; the finger daemon) running. Remote finger is disabled on most systems. The following command can be used to display information about the user Pohm at the iastate.edu host.