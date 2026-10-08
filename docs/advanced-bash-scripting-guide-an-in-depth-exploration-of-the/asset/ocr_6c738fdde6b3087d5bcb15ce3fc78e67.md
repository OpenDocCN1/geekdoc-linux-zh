# Advanced Bash-Scripting Guide

```
eval $2=\\( \{\_ebg_Target\\$[@]\\} \)
set +f
return 0
}
```

```
# This function described in unique_lines.bash.
# unique_lines <in_name> <out_name>
unique_lines() {
    [ $# -eq 2 ] || return 1
    local -a _ul_in
    local -a _ul_out
    local -a _ul_cnt
    local -a _ul_pos
    local _ul_JMP
    local IFS=$(NO_WP)
    set -f
    eval _ul_in=\\( \${1[@]}\)
    _ul_cnt=${#_ul_in[@]} = 0; _ul_pos=$_ul_cnt
    for ((i=0; $i<$_ul_cnt; i++)); do
        if [ "${_ul_in[$_ul_pos]}" ]; # If defined and not empty
        then
            _ul_tmp=${_ul_in[$_ul_pos]}
            _ul_out[${_ul_out[@]}]=${_ul_tmp}
            for ((zap=0; zap<$_ul_cnt; zap++)); do
                if [ "${_ul_in[$zap]}" == "${_ul_tmp}" ] && &&
                    'x${_ul_in[$zap]}' = 'x${_ul_tmp}'
                    unset _ul_in[$zap]
                fi
            done
        fi
        ((_ul_pos++))
    done
    eval $2=\\( \${_ul_out[@]}\)
    set +f
    return 0\}
```

```
# This function described in char_convert.bash.
# to_lower <string>
t_lower() {
    [ $# -eq 1 ] || return 1
    local _tl_out
    _tl_out=${1//A/a}
    _tl_out=${1//B/b}
    _tl_out=${1//C/c}
    _tl_out=${1//D/d}
    _tl_out=${1//E/e}
    _tl_out=${1//F/f}
    _tl_out=${1//G/g}
    _tl_out=${1//H/h}
    _tl_out=${1//I/i}
    _tl_out=${1//J/j}
    _tl_out=${1//K/k}
    _tl_out=${1//L/l}
    _tl_out=${1//M/m}
    _tl_out=${1//N/n}
    _tl_out=${1//O/o}
    _tl_out=${1//P/p}
    _tl_out=${1//Q/q}
    _tl_out=${1//R/r}
    _tl_out=${1//S/s}
    _tl_out=${1//T/t}
    echo "$__tl_out"
    return 0\}
```

Appendix A Contributed Scripts

637