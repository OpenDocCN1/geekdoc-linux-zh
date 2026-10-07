```
start () {
  echo -n "Starting myewutilityd: "
  # start daemon
  daemon /usr/sbin/mynewutilityd
  RETVAL=$?
  echo
  [ $RETVAL = 0 ] && touch /var/lock/subsys/mynewutilityd
  return $RETVAL
}
```

```
stop () {
  # stop daemon
  echo -n "Stopping myewutilityd: "
  killproc /usr/sbin/mynewutilityd
  RETVAL=$?
  echo
  [ $RETVAL = 0 ] && rm -f /var/lock/subsys/mynewutilityd
  return $RETVAL
}
```

```
restart () {
  stop
  start
  RETVAL=$?
  return $RETVAL
}
```

# See how we were called.
case "$1" in
start)