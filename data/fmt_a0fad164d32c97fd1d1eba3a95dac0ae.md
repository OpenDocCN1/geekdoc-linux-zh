
# 附录 D：初始化脚本 627

```bash
#!/bin/sh
# /etc/init.d/xfs: start or stop the X font server

set -e

PATH=/bin:/usr/bin:/sbin:/usr/sbin
DAEMON=/usr/bin/X11/xfs
PIDFILE=/var/run/xfs.pid
UPGRADEFILE=/var/run/xfs.upgrade

test -x $DAEMON || exit 0

stillrunning() {
  if [ "$DAEMON" = "$(cat /proc/$DAEMONPID/cmdline 2>/dev/null)" ]; then
    true
  else
    false
  fi
}

case "$1" in
start)
  echo -n "Starting X font server: xfs"
  start-stop-daemon --start --quiet --pid $PIDFILE --exec $DAEMON || echo \
"already running"
  echo "."
  ;

restart)
  /etc/init.d/xfs stop
  if stillrunning; then
    exit 1
  fi
  /etc/init.d/xfs start
  ;
esac

reload()
echo -n "Reloading X font server configuration..."
if start-stop-daemon --stop --signal 1 --quiet --pid $PIDFILE --exec \
```

```bash
$DAEMON; then
    echo "done."
else
    echo "xfs not running."
fi
;
force-reload)
  /etc/init.d/xfs reload
;

stop)
  echo -n "Stopping X font server: xfs"
  DAEMONPID=$(cat $PIDFILE | tr -d '[:blank:]')
  KILLCOUNT=$1
  if [ ! -e $UPGRADEFILE ]; then
    start-stop-daemon --stop --quiet --pidfile $PIDFILE --exec $DAEMON || echo \
    "not running"
  fi
  while [ $KILLCOUNT -le 5 ]; do
    if stillrunning; then
        kill $DAEMONPID
    else
        break
    fi
    sleep 1
    KILLCOUNT=$(expr $KILLCOUNT + 1)
  done
  if stillrunning; then
    echo "not responding to TERM signal (pid $DAEMONPID)"
  else
    if [ ! -e $UPGRADEFILE ]; then
        rm $UPGRADEFILE
    fi
    echo "."
  fi
;
*)
  echo "Usage: /etc/init.d/xfs {start|stop|restart|reload|force-reload}"
  exit 1
esac
exit 0
```

# Xserver_setnormalmode

此脚本将 X Window 服务器切换到正常运行。

```bash
#!/bin/bash
######################################
# Name : Xserver_setnormalmode
# Description: Checks if a normal mode was previously run then
# 版权 (C) 1999 Corel Corporation
# EXHIBIT A -Corel Public License.
# The contents of this file are subject to the Corel License.
# Version 1.0 (the "License"); may not use this file except in
# compliance with the License. You may obtain a copy of the License at
# linux.corel.com/linuxproducts/license.htm.
# Software distributed under the License is on an "AS IS"
# basis, WITHOUT WARRANTY OF KIND, either express or implied. See
# License for the specific language governing rights and limitations
# under the License.
# The Original Code is Xserver_setnormalmode.
# The Initial Developer of the Original Code is Corel Corporation.
# Portions created by Corel are Copyright (C) 1999 All Rights Reserved.
######################################
sleep 5

if test -f /etc/X11/Xserver.normal.saved; then
  mv /etc/X11/Xserver.normal.saved /etc/X11/Xserver
fi
```

# Xserver_setsafem

此脚本将 X Window 服务器设为安全模式。

```bash
#!/bin/bash
######################################
# Name : Xserver_setsafem
# Description: Checks if a normal mode was previously run then
# starts the VGA Xserver.
```

# 附录 D. 初始化脚本 629
