```
confirm() {
  local YES=$'yY'
  local NO=$'nN'
  local CONT=$'cC'

  while : ; do
    echo -n $'Start service $1 (Y)es/(N)o/(C)ontinue? [Y] '
    read answer
    if strstr "$YES" "$answer" || [ "$answer" = "" ] ; then
      return 0 # || is an OR condition above
    elif strstr "$CONT" "$answer" ; then
      return 2
    elif strstr "$NO" "$answer" ; then
      return 1
    fi
  done
}
```

Mac OS X has startup scripts in the /etc/rc.local file (a typical BSD location for them), and within that file there are some interesting additional shell functions:

```
##
# Print a message to the console and display it in the startup screen
##
ConsoleMessage()
{
  local Message="$*"

  echo "$Message"
}
##
## Determine if the network is up by looking for any non-loopback
# internet network interfaces. - uses 'sed', the stream-editor, to
# make simple modifications to information in a pipe. See sed(1)
##
CheckForNetwork()
{
  local test

  if [ -z "${NETWORKUP:-}" ]; then
    test=$(ifconfig a | sed -e '/127.0.0.1/d' | sed -e '/0.0.0.0/d' | sed -n '/inet/p' | wc -l)
    if [ "$test" -gt 0 ]; then
      NETWORKUP="YES"
    else
      NETWORKUP="NO"
    fi
  fi
}
```