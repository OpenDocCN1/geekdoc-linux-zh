
```
matthew@seymour:~$ cat < file.txt
```

```
matthew@seymour:~$ sudo dpkg --get-selections > pkg.list
```

```
matthew@seymour:~$ sudo dp --set-selections < pkg.list
```

```
matthew@seymour:~$ cat myfile.txtotherfile.txt > combinedfile.txt
```

```
matthew@seymour~$ echo "This is a new line." >> file.txt
```

```
matthew@seymour:~$ verboseprocess > /dev/null
```

```
matthew@seymour:~$ program 2> error.log
```

```
matthew@seymour:~$ program &> filename
```

```
matthew@seymour:~$ program >> 2>&1
```

```
matthew@seymour:~$ diff file1 file2
```

```
matthew@seymour:~$ comm file1 file2
```

```
matthew@seymour:~$ ps aux --sort=-%cpu
```

```
matthew@seymour:~$ programname
```

```
matthew@seymour:~$ a & b & c
```

```
matthew@seymour:~$ find -type f -printf "%s\t%p\n" | sort -n
```

```
matthew@seymour:~$ sudo nice -n 19 tarf compressedfilename.tgz
```

```
matthew@seymour:~$ sudo renice 19 -p20136
```

```
matthew@seymour:~$ sudo renice -20 -u mysql
```

```
matthew@seymour:~$ sudo renice -20 -g website
```

```
matthew@seymour:~$ sudo ionice -c3 -p24351
```

```
matthew@seymour:~$ find "*.txt" -size +10k -not -perm +or -exec chmod o+r \;
```

```
matthew@seymour:~$ find / -name "*.txt" -size +10k -not -perm +or | xargs chmod o+r
```

```
matthew@seymour:~$ find /home/matthew -size +10000k | xargs -cp {} ./home/matthew/archive
```

```
matthew@seymour:~$ ps aux --sort=-%cpu | grep -v 'whoami'
matthew@seymour:~$ ps -N --sort=-%cpu
```

```
matthew@seymour:~$ dpkg --get-selections | grep ftp | sort
ftp install
nlftp install
```

```
matthew@seymour:~$ doctor ; tardis
```

```
matthew@seymour:~$ cat <(ls -al)
```

```
matthew@seymour:~$ diff <(ls firstdirectory) <(ls secondhand)
```

```
matthew@seymour:~$ ls firstdirectory > file.txt
matthew@seymour:~$ ls secondirectory > file2.txt
matthew@seymour:~$ diff file.txt file2.txt
```

```
matthew@seymour:~$ echo $USER
matthew
matthew@seymour:~$
```

```
matthew@seymour:~$ env

ORBIT_SOCKETDIR=/tmp/orbit-mathew
SSH_AGENT_PID=1729
TERM=xterm
SHELL=/bin/bash
WINDOWID=713030173
GOME_KEYRING_CONTROL=/tmp/keyring-qTEFTw
GTK_MODULES=canberra-gtk-module
USER=matt
SSH_AUTH_SOCK=/tmp/keyring-qTEFTw/ssh
DEFAULTS_PATH=/usr/share/gconf/gnome.default.path
SESSION_MANAGER=/local/seymour:/tmp/.ICE-unix/1695
USERNAME=matthew
XDG_CONFIG_DIRS=/etc/xdg/xdg-gnome:/etc/xdg
DESKTOP_SESSION=gnome
PATH=/usr/local/bin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
PWD=/home/matthew
GDM_KEYBOARD_LAYOUT=us
LANG=en_US.utf8
GNOME_KEYRING_PID=1677
MANDATORY_PATH=/usr/share/gconf/gnome.mandatory.path
GDM_LANG=en_US.utf8
GDMSSESSION=gnome
HISTHISTCONTROL=ignoreboth
SPEECHCH_PORT=7560
SHLVL=1
HOME=/home/matt
LOGNAME=matt
LESSOPEN=| /usr/bin/lespipe %s
DISPLAY=:0.0
LESSCLOSE=/usr/bin/lespipe %s %s
AUTHORITY=/var/run/gdm/auth-for-matthew-PzcGf/database
COLORTERM=gnome-terminal
OLDPWD=/var/lib/mlocate
_=/usr/bin/env
```

```
matthew@seymour:~$ command

程序 'command' 当前未安装。你可以通过输入以下命令安装：

sudo apt-get install command
```

```
matthew@seymour:~$ whereis command
command: /sbin/command
```

```
matthew@seymour:~$ /sbin/command
```

```
matthew@seymour:~$ source .bash_profile
```

```
matthew@seymour:~$ export PS1='$OSTYPE r00lz -> '
```

```
matthew@seymour:~$ emacs file.txt
```

```
matthew@seymour:-$ sed sedcommand inputfile
matthew@seymour:-$ sed -e sedcommand inputfile
matthew@seymour:-$ sed -e sedcommand -e anothersedcommand inputfile
```

```
matthew@seymour:-$ sed -e 's/camel/buggy/g' transportation.txt
```

```
matthew@seymour:~$ sed -e '4,17d' longtext.txt
```

```
matthew@seymour:-$ awk -F',' '{print $1, "*was last picked up on", $4}' deskstuff.txt
```

```
matthew@seymour:~$ tar czf compressedfilename.tgz directoryname
```

```
matthew@seymour:~$ tar tzf archive
```

```
matthew@seymour:-$ tar tzf archive | less
```

```
matthew@seymour:~$ tar zxf archive
```
