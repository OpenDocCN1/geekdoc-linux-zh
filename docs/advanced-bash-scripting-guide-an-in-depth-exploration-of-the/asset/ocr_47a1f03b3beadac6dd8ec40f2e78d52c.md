```
# Execution trace is enabled by setting the
+ environment variable SPAMMER_TRACE to the name of a writable file.
declare -a _trace_log
declare _log_file

# Function to fill the trace log
trace_logger() {
    _trace_log[$#_trace_log[@]]]=${pend_current}
}

# Dump trace log to file variable.
declare -f _log_dump
dump_dump=pend_dummy # Initially a no-op.
# Dump the trace log to a file.
dump_log() {
    local -l dl_cnt
    _dl_cnt=$${_trace_log[@]}
    for (( _dl = 0; _dl < _dl_cnt; _dl++ ));
    do
        echo ${_trace_log[$_dl]} >> ${_log_file}
    done
    _dl_cnt=${_pending[@]}
    if [ ${_dl_cnt} -gt 0 ];
    then
        _dl_cnt=$${_dl_cnt}-1
        echo '# # Operations stack not empty # #' >> ${_log_file}
        for (( _dl = ${_dl_cnt}; _dl >= 0; --dl-- ));
        do
            echo ${_pending[$_dl]} >> ${_log_file}
        done
    fi
}

# Utility program 'dig' wrappers
# These wrappers are derived from
+# examples shown in dig_wrappers.bash.
# The major difference is these return
+# their results as a list in an array.
# See dig_wrappers.bash for details and
+# use that script to develop any changes.

# Short form answer: 'dig' parses answer.
# Forward lookup : Name -> Address
# short_fwd :<domain_name> <array_name>
short_fwd() {
    local -a _sf_reply
    local -i _sf_rc
    local -i _sf_cnt
IFS=$-
    echo -n ' '
    echo 'sfwfd: '${1}'
    _sf_reply=$(dig +short ${1} -c n -t 2>>/dev/null)
    _sf_rc=$?
    if [ ${_sf_rc} -ne 0 ];

```