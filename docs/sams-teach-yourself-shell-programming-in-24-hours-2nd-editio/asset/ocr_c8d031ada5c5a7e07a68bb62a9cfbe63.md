You can solve the first issue by using shift to remove the first argument. You can solve the second issue by using the variable $? to check the exit status of tar. If you implement these changes, your script becomes:

```
#!/bin/sh

USAGE="usage: `basename $0` [-c|-t] [files|directories]"

if [ $# -lt 2 ] ; then
  echo "$USAGE" ;
  exit 1 ;
fi

case "$1" in
  -t) shift
      TARGS="-tvf" ;
      for i in $* ;
      do
        if [ -f "$i" ] ; then
          FILES=`tar $TARGS $i 2>/dev/null`
          if [ $? -eq 0 ] ; then
            echo ; echo "$FILES"
          else
            echo "ERROR: $i not a tar file."
          fi
        else
          echo "ERROR: $i not a file."
        fi
      done
      ;;
  -c) shift
      TARGS="-cvf" ;
      TARGS_ARCHIVE.tar $*
      ;;
  *) echo "$USAGE"
     exit 0
     ;;
esac
exit $?
```

# Option Parsing in Shell Scripts

In the previous example, you manually handled the options passed to your script. In this second example, you will explore a second method, using the getopts command. The syntax of the getopts command is as follows:

```
getopts option-string var
```