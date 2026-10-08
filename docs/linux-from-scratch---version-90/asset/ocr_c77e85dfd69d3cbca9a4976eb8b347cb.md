```
suffix=$($i#/etc/rc.d/rc$runlevel.d/K[0-9][0-9]
prev_start=$etc/rc.d/rc$previous.S[0-9][0-9]$suffix
sysinit_start=$etc/rc.d/rc$d/S[0-9][0-9]$suffix

if [ "$runlevel" != "0" -a "$runlevel" != "6" ]; then
  if [ ! -f "${prev_start}" -a ! -f "${sysinit_start}" ]; then
    MSG="$(MSG)WARNING:\n$(i) cannot be"
    MSG="$(MSG)executed because it was not"
    MSG="$(MSG)not started in the previous"
    MSG="$(MSG)runlevel (${previous})"\n    log_warning_msg "$MSG"
    continue
  fi

run$${i} stop
error_value=${?}

if [ "${error_value}" != "0" ]; then print_error_msg;
fi

if [ "${previous}" != "N" ]; then export IN_BOOT=1; fi
if [ "${runlevel}" != "6" -a n "${FASTBOOT}" ]; then
touch /fastboot
fi

# Start all functions in this runlevel
for i in $(ls -v /etc/rc.d/rc$runlevel).d/S* 2>/dev/null);
do
  if [ "${previous}" != "N" ]; then
    suffix=$($i#/etc/rc.d/rc$runlevel.d/K[0-9][0-9])
    stop=$/etc/rc.d/rc$runlevel.d
    prev_start=$etc/rc.d/rc$previous.S[0-9][0-9]$suffix

    [ -f "${prev_start}" -a ! -f "${stop}" ] && continue
  fi
do

check_script_status
if [ "${SCRIPT_STAT}" == "1" ]; then
  SCRIPT_STAT="0"
  continue
fi

case ${runlevel} in
0|6)
  run$${i} stop
  ;;
  *)
  run$${i} start
  ;;
esac

error_value=${?}

```