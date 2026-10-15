In a typical UNIX system, you are not allowed to access all the files and directories in the system. In particular, you are typically not allowed to access many important files and directories related to system administration and files and directories belonging to other users. However, you have permissions to read a number of directories and files. The following session illustrates that we have permissions to go to and list the contents of, among many other directories, the / and /usr directories.

```
$ cd /usr
$ ls
bin  home  jails  lib32  libexec  obj  ports  share  swap
games  include  lib  libdata  local  pbi  sbin  src  tests
$ cd /
$ ls
COPYRIGHT  compat  entropy  lib  mnt  root  tmp
bin  data  etc  libexec  proc  sbin  usr
boot  dev  home  media  rescue  sys  var
$ cd
$ ls /usr
bin  home  jails  lib32  libexec  obj  ports  share  swap
games  include  lib  libdata  local  pbi  sbin  src  tests
$
```

Without any option, the ls command does not show all the files and directories; in particular, it does not display the names of hidden files. Examples of these files include ., .., .bash_history, .bashrc, .config, .cshrc, .history, .login, .mailrc, .profile, .rhosts, .shrc, .ssh, and .xsession. We have already discussed the . and .. directories. The purposes of some of the more important hidden files are summarized in Table 4.2.

You can also display the names of all the files and directories in a directory, including the hidden files, by using the ls command with the -a option. In the following session, the cd command places you in your home directory and the ls -a command displays all the files and directories, including the hidden files, in your home directory.

```
$ cd
$ ls -a
.  .gnome2  .lesshst  .shrc  Downloads
..  .gtkrc-2.0  .login  .ssh  GNUstep
.bash_history  .history  .login_conf  .windowlab  Images
.cinnamon  .i3  .mail_aliases  .xprofile  Music
.config  .icewm  .mailrc  .xscreensaver  Videos
.cshrc  .icons  .profile  .xsession  courses
.fluxbox  .ideskrc  .ratpoisonrc  .zshrc  personal
.fvwm-crystal  .kde4  .rhosts  Desktop  unix3e
.gconf  .kde4  .screenrc  Documents
$
```