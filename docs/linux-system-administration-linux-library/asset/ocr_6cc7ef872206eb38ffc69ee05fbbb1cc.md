```
*.sh)
# Source shell script for speed.
(
  trap - INT QUIT TSTP
  set start
  $i
)
;;
*)
# No sh extension, so fork subprocess.
$i start
;;
esac
done
```

```
#
# For compatibility, run the files in /etc/rc.boot too.
#
[ -d /etc/rc.boot ] && run-parts /etc/rc.boot
```

```
#
# Finish setup if needed. The comment above about
# /sbin/unconfigured.sh applies here as well
#
if [ -x /sbin/setup.sh ]
then
  /sbin/setup.sh
fi
```

The rcS files set up some environmental variables, including the PATH variable. It runs a special configuration shell script if the system is running for the first time after installation. The rcS script then runs other scripts, which do things like enable virtual