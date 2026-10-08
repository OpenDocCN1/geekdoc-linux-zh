
```bash
# Execution trace is enabled by setting the 
# environment variable SPAMMER_TRACE to the name of a writable file.
declare -a _trace_log
declare _log_file

# Function to fill the trace log
trace_logger() {
    _trace_log[$#_trace_log[@]]=${pend_current}
}

# Dump trace log to file variable.
declare -f _log_dump
dump_dump=pend_dummy # Initially a no-op.
# Dump the trace log to a file.
dump_log() {
    local -l dl_cnt
    _dl_cnt=${#_trace_log[@]}
    for (( _dl = 0; _dl < _dl_cnt; _dl++ ));
    do
        echo ${_trace_log[$_dl]} >> ${_log_file}
    done
    _dl_cnt=${#_pending[@]}
    if [ ${_dl_cnt} -gt 0 ];
    then
        _dl_cnt=$((_dl_cnt-1))
        echo '# # Operations stack not empty # #' >> ${_log_file}
        for (( _dl = ${_dl_cnt}; _dl >= 0; --dl-- ));
        do
            echo ${_pending[$_dl]} >> ${_log_file}
        done
    fi
}

# Utility program 'dig' wrappers
# These wrappers are derived from
# examples shown in dig_wrappers.bash.
# The major difference is these return
# their results as a list in an array.
# See dig_wrappers.bash for details and
# use that script to develop any changes.

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
    then
        _trace_log(${#_trace_log[@]})===='# Lookup error '${_sf_rc}' on '${1}' ''
        # [ ${_sf_rc} -ne 9 ] && pend_drop
        return ${_sf_rc}
    else
        # Some versions of 'dig' return warnings on stdout.
        sf_cnt=${#_sf_reply[@]}
        for (( _sr = 0; _sr < ${_sf_cnt}; _sr++ ))
        do
            [ 'x${_sf_reply[$_sr]}:0:2' == 'x;' ] &&
                unset _sf_reply[$_sr]
        done
        eval 2="${_sf_reply[0]}"
    fi
    return 0
}

# Reverse lookup : Address -> Name
# short_rev <ip_address> <array_name>
short_rev() {
    local -a _sr_reply
    local -i _st_rc
    local -i _st_cnt
    IFS=$NO_WSP
    echo -n ' '
    echo "${1}'
    _sr_reply=$(dig +x ${1} 2>/dev/null)
    _sr_rc=$?
    if [ ${_sr_rc} -ne 0 ]
    then
        _trace_log(${#_trace_log[@]})===='# Lookup error '${_sr_rc}' on '${1}'''
        # [ ${_sr_rc} -ne 9 ] && pend_drop
        return ${_sr_rc}
    else
        # Some versions of 'dig' return warnings on stdout.
        _sr_cnt=${#_sr_reply[@]}
        for (( _sr = 0; _sr < ${_sr_cnt}; _sr++ ))
        do
            [ 'x${_sr_reply[$_sr]}:0:2' == 'x;' ] &&
                unset _sr_reply[$_sr]
        done
        eval 2="${_sr_reply[0]}"
    fi
    return 0
}

# Special format lookup used to query blacklist servers.
# short_text <ip_address> <array_name>
short_text() {
    local -a _st_reply
    local -i _st_rc
    local -i _st_cnt
    IFS=$NO_WSP
    echo -n '${1}'
    _st_reply=$(dig +short ${1} -in -t txt 2>/dev/null)
    _st_rc=$?
    if [ ${_st_rc} -ne 0 ]
    then
        _trace_log(${#_trace_log[@]})===='# Text lookup error '${_st_rc}' on '${1}'''
        # [ ${_st_rc} -ne 9 ] && pend_drop
        return ${_st_rc}
    else
        # Some versions of 'dig' return warnings on stdout.
        _st_cnt=${#_st_reply[@]}
        for (( _st = 0; _st < ${_st_cnt}; _st++ ))
        do
            [ 'x${_st_reply[$_st]}:0:2' == 'x;' ] &&
                unset _st_reply[$_st]
        done
        eval 2="${_st_reply[0]}"
    fi
    return 0
}
```

Appendix A. Compiled Scripts

## Advanced Bash-Scripting Guide

## Application specific functions

Appendix A. Contributed Scripts
