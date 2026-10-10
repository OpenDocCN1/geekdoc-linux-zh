# Part IV: Working with Alternative Shells

Many of the tcsh environment variables are duplicates of the shell variable of the same name. This is to provide some compatibility with the Bourne shell environment (note the inclusion of the PATH environment variable, which uses the same format as the Bourne shell PATH environment variable).

However, the two aren't linked. If you change one, the other won't change. Thus, you can cause all sorts of problems by setting a shell variable (such as path) without setting the corresponding environment variable (PATH).

To display the current environment variables, you must use the setenv command:

```
```
ubuntu2404:~$ setenv
SHELL=/bin/bash
SESSION_MANAGER=local/ubuntu2404:/tmp/.ICE-unix/2797,unix/ubuntu2404:/tmp/.ICE-unix/2797
QT_ACCESSIBILITY=1
COLORTERM=truecolor
XDG_CONFIG_DIRS=/etc/xdg:/xdg-ubuntu:/etc/xdg
XDG_MENU_PREFIX=gnome-
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
GNOME_SHELL_SESSION_MODE=ubuntu
SSH_AUTH_SOCK=/run/user/1000/keyring/ssh
MEMORY_PRESSURE_WRITE=c29tZS9Mb2FkMDMgMDAwA\n
DMIDATE88=immibiuc
DESKTOP_SESSION=ubuntu
GTK_MODULES=gail:atk-bridge
PWD=/home/rich
LOGNAME=rich
XDG_SESSION_DESKTOP=ubuntu
XDG_SESSION_TYPE=wayland
SYSTEMD_EXEC_PID=2832
XAUTHORITY=/run/user/1000/.mutter-Xwaylandauth.D03AC3
HOME=/home/rich
USERNAME=rich
IM_CONFIG_PHASE=1
LANG=en_US.UTF-8
LS_COLORS=rs:0:di:01;34:ln:01;36:mh:00:pi:40;33:so:00:ex:00;32:tw:42:ow:34:42:st:37:44:e:40;33:or:40:31:01:mi:00:su:37:41:bg:00;33:ca:00:tw:30;42:ow:34;42:st:37:44:co:32:tar:01;33:tar:01;31:tgz:01;31:7z:41;33:gz:41;33:jar:41;31:rar:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41:41.41.41.41.41.41.41.41.41.41
```
```