```
PATH=/sbin:/bin:/usr/sbin:/usr/bin
runlevel=$
prevlevel=N
umask 022
export PATH runlevel prevlevel

#
#  See if system needs to be set up. This is ONLY meant to
#  be used for the initial setup after a fresh installation!
#
if [ -x /sbin/unconfigured.sh ]
then
    /sbin/unconfigured.sh
fi

#
#   Source defaults.
#
. /etc/default/rcS
export VERBOSE

#
#  Trap CTRL-C &c only in this shell so we can interrupt
#  subprocesses.
#
trap "": INT QUIT TSTP

#
#   Call all parts in order.
#
for i in /etc/rcS.d/S??*
do
    # Ignore dangling symlinks for now.
    [ ! -f "${i}" ] && continue
    case "${i}" in
        *.sh)
            # Source shell script for speed.
            (
                trap - INT QUIT TSTP
                set start
                . ${i}
            );;
        *)
            # No sh extension, so fork subprocess.
            ${i} start
            ;;
    esac
done

#
#   For compatibility, run the files in /etc/rc.boot too.
#
[ -d /etc/rc.boot ] && run-parts /etc/rc.boot

#
#   Finish setup if needed. The comment above about
#   /sbin/unconfigured.sh applies here as well!
#
if [ -x /sbin/setup.sh ]
then

```