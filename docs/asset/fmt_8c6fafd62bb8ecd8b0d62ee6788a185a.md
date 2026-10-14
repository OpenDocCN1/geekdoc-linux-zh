
# `/etc/profile`

# `$Id$`

# Minimum system wide initialization of *login*-bourne shells

# Functions and aliases go in `$HOME/.bashrc`

# `[ -e /etc/config.d/0 ] && echo "/etc/profile: \$ = '$.'" 1>&2`

`_ETC_PROFILE=1`

`PATH="/bin:/usr/bin"`

`umask 022`

```
if [ ! -x /usr/bin/id ]&&[ -z "$USER" -o -z "$UID" ]; then

    echo "/usr/bin/id: no such file" 1>&2

    echo "As this program is essential for OpenLinux shell-initiation"

    echo " you experience problems later. Please install 'sh-utils'..." 1>&2

    [ -z "$USER" ] && USER=unknown

    [ -z "$UID" ] && UID=-1

else

    [ -z "$USER" ] && USER=`/usr/bin/id -un`

    [ -z "$UID" ] && UID=`/usr/bin/id -u`

fi

[ -z "$HOST" ] && HOST=`/bin/hostname -f`

[ -z "$HOSTNAME" ] && HOSTNAME=`/bin/hostname -s`

[ -z "$LOGNAME" ] && LOGNAME=$USER

export _ETC_PROFILE PATH USER HOST HOSTNAME LOGNAME
```

`/etc/profile` 文件应由系统管理员维护，任何适用于所有用户的更改都应在此文件中设置。

然后，所有 bash shell 都会运行 `$HOME/.bashrc` 文件。Caldera 提供的 `.bashrc` 如清单 14.2 所示。

### 清单 14.2——默认的 .bashrc 文件

```sh
# ~/.bashrc~

# $Id: .bashrc,v 1.2 1999/02/12 13:32:54 ray Exp ray $

# The individual per-interactive-shell startup file for bash

# [ -e /etc/config.d/ ] && echo "$USER/.bashrc: $-" 1>&2

# load maintained system-defaults...  (NB: $HOME/.profile, i.e.

# /etc/config.d/shells/profile) depend on this one!!!

# [ -r /etc/config.d/shells/bashrc ] && . /etc/config.d/shells/bashrc

# load user-defaults

[ -r $HOME/.bashrc-private ] && . $HOME/.bashrc-private

# personal additions should preferably be placed in the above file,

# but may nevertheless be appended below...
```

请注意引用 `/etc/config.d/shells/bashrc` 的那一行。该行指示 bash 检查文件 `/etc/config.d/shells/bashrc` 是否存在且用户可读，如果存在且可读，则执行它。这是一个类似于 `/etc/profile` 的 bash 专用全局配置文件。两者之间的区别在于，`/etc/profile` 适用于所有 Bourne shell，而 bashrc 中的命令是 bash 特有的（或者说应该是 bash 特有的）。清单 14.3 显示了默认全局 bashrc 文件的内容。

### 清单 14.3——默认的 /etc/config.d/shells/bashrc 文件

```sh
# /etc/config.d/shells/bashrc

# $Id: bashrc,v 1.3 1999/02/12 15:11:02 ray Exp ray $

# Full fledged, system-wide initialization of "interactive"-shells

# (source-able by $HOME/.bashrc)
```

## 清单 14.3（续）

```sh
# [ -e /etc/config.d/D ] && echo "/etc/config.d/shells/bashrc: \$=\$=\$" 1>&2

# if we haven't read /etc/profile (e.g. rsh or su) read it now...

[ -z "$E_PROFILE" ] && . /etc/profile

# fiddle with umask

umask 022

[ -n "$USER" ]&&[ "$USER" = `id -gn` ]&&[ "$UID" != 0 ]&& umask 002

# set up "HOME" variables for certain packages...

[ -z "$KDEDIR" ]&&[ -d /opt/kde ] && export KDEDIR=/opt/kde

[ -z "$OPENWINHOME" ]&&[ -d /usr/openwin ] && export OPENWINHOME=/usr/openwin

[ -z "$JAVA_HOME" ]&&[ -d /usr/java ] && {

  export JAVA_HOME=/usr/java

  [ -r $JAVA_HOME/lib/classes.zip ] &&

    export CLASSPATH=$JAVA_HOME/lib/classes.zip

}

# try to generate an elaborate PATH ...

_p="$HOME/bin"

[ "$UID" = 0 ] && _p="$_p /usr/local/sbin /sbin /usr/sbin"

_q=`echo "$PATH" | sed -e 's/:/ /g' -e 's/ \.[. ]* / /g'`

_q="$_q /usr/local/bin /usr/X11R6/bin /opt/bin /opt/TeTeX/bin"

_q="$_q $KDEDIR/bin $OPENWINHOME/bin $JAVA_HOME/bin"

_p=""

for _i in $_p $_q; do

  case "$_p:" in

    *:$_i:*) : $_i;;

    *) [ -d $_i ] && _p="$_p:$_i" ;;

  esac

done

while [ $_p != ${_p#*:} ]; do _p=${_p#*:}; done

# if you have relaxed security concerns you may uncomment the following...

#[ -n "$UID" ]&&[ "$UID" != 0 ]&& _p="${_p}:"

export PATH=$_p

unset _p _q _i _p

# try to solve this tedious ‘Backspace vs. Delete’ problem...

case $_ in

  *i*)

    if [ -z "$TERM" ]; then

      echo ".bashrc: TERM empty: this shouldn't happen!" 1>&2

      echo "  Please contact 'support@caldera.com'" 1>&2

    else

      case $TERM in

        dumb)

          :

          ;;

        linux*)

          stty erase '^?'

          ;;

        *)

          stty erase '^H'

          ;;

      esac

    fi

    ;;

esac

# general environment settings

export MAIL=/var/spool/mail/$USER

#export GROFF_TYPESETTER=latin1

#export LC_CTYPE=iso-8859-1
```
