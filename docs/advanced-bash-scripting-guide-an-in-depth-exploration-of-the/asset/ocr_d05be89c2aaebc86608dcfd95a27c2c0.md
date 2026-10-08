# Advanced Bash-Scripting Guide

```
then
_trace_log($${_trace_log[@]})===='# Lookup error '${_sf_rc}' on '${1}' ''
# [ ${_sf_rc} -ne 9 ] && pend_drop
    return ${_sf_rc}
else
    # Some versions of 'dig' return warnings on stdout.
    sf_cnt=$${_sf_reply[@]}
    for (( _sr = 0; _sr < ${_sf_cnt}; _sr++ ))
    do
        [ 'x${_sf_reply[$_sr]}:0:2' == 'x;' ] &&
            unset _sf_reply[$_sr]
    done
    eval 2=$=\${_sf_reply[\\]}\]
fi
return 0
}

# Reverse lookup : Address -> Name
# short_rev <ip_address> <array_name>
short_rev()
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
        _trace_log($${_trace_log[@]})===='# Lookup error '${_sr_rc}' on '${1}'''
        # [ ${_sr_rc} -ne 9 ] && pend_drop
        return ${_sr_rc}
else
        # Some versions of 'dig' return warnings on stdout.
        _sr_cnt=$${_sr_reply[@]}
        for (( _sr = 0; _sr < ${_sr_cnt}; _sr++ ))
        do
            [ 'x${_sr_reply[$_sr]}:0:2' == 'x;' ] &&
                unset _sr_reply[$_sr]
        done
        eval 2=$=\${_sr_reply[\\]}\]
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
        _trace_log($${_trace_log[@]})===='# Text lookup error '${_st_rc}' on '${1}'''
        # [ ${_st_rc} -ne 9 ] && pend_drop
        return ${_st_rc}
else
fi}
```

Appendix A. Compiled Scripts

645