# Advanced Bash-Scripting Guide

```
'Unable to create log file >${SPAMMER_TRACE}'
pend_release
exit 1
fi
log_file=${SPAMMER_TRACE}
pend_hook=_trace_logger
log_dump=dump_log
else
if [ ! -w ${SPAMMER_TRACE} ];
then
  pend_func $(printf '%q\n')
  'Unable to write log file >${SPAMMER_TRACE}'
pend_release
  exit 1
fi
log_file=${SPAMMER_TRACE}
echo '' '${log_file}'
pend_hook=_trace_logger
log_dump=dump_log
fi
return 0
environment.variable SPAMMER_DATA
data_capture() {
if [ ${SPAMMER_DATA}= ]; # Wants a data dump?
if [ -e ${SPAMMER_DATA} ];
then
  if touch ${SPAMMER_DATA} 2>/dev/null
  then
    pend_func $(printf '%q\n') \
    'Unable to create data output file >${SPAMMER_DATA}'
    pend_release
    exit 1
  fi
  .dot_file=${SPAMMER_DATA}
  .dot_dump=dump_dot
else
  if [ ! -w ${SPAMMER_DATA} ];
  then
    pend_func $(printf '%q\n') \
    'Unable to write data output file >${SPAMMER_DATA}'
    pend_release
    exit 1
  fi
  .dot_file=${SPAMMER_DATA}
  .dot_dump=dump_dot
fi
fi}
# Grope user specified arguments.
do_user_args() {
if [ $#-gt 0 ] && is_number $1;
then
  indirect=$1
  shift
fi}
```

Appendix A. Contributed Scripts

659