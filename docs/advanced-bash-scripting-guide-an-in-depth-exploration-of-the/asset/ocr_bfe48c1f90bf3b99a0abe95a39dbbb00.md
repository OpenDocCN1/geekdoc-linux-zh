# Advanced Bash-Scripting Guide

```
[ # -eq 2 ] ||n[ # -eq 3 ] || return 1
local -aee_Excludes
local -aee_Target
local -aee_x
local -aee_t
local IFS=$(NO_WSP)
set -f
e _aee_Excludes=\(${$1[[:digit:]]*}\)
eval _aee_Target=\(${$2[[:digit:]]*}\)
local _aee_len=${#_aee_Target[0]} # Original length.
local _aee_cnt=${#_aee_Excludes[0]} # Exclude list length.
[ ${_aee_len} -ne 0 ] || return 0 # Can't edit zero length.
[ ${_aee_cnt} -ne 0 ] || return 0 # Can't edit zero length.
for (( x = 0; x < ${_aee_cnt}; x++ ))
dn
_aee_x=${_aee_Excludes[$x]}
for (( n = 0; n < ${_aee_len}; n++ ))
dn
_aee_t=${_aee_Target[n]}
if [ "${_aee_t}" == "${_aee_x}" ]
then
unset _aee_Target[$n]
[ $ -eq 2 ] && break # Discard march,
# If 2 arguments, then done.
fi
done
done eval $2=\(${_aee_Excludes[[:digit:]]*}\)
set + f
return 0
```

# This function described in edit_by_glob.bash.
# edit_by_glob <excludes_array_name> <target_name>
edit_by_glob() {

```
[ -eq 2 ] ||[ -eq 3 ] || return 1
local -aebg_Excludes
local -aebg_Target
local -aebg_x
local -aebg_t
local IFS=$(NO_WSP)
set - f
e _aebg_Excludes=\(${$1[[:digit:]]*}\)
eval _aebg_Target=\(${$2[[:digit:]]*}\)
local _aebg_len=${#_aebg_Target[0]}
local _aebg_cnt=${#_aebg_Excludes[0]}
[ ${_aebg_len} -ne 0 ] || return 0
[ ${_aebg_cnt} -ne 0 ] || return 0
for (( x = 0; x < ${_aebg_cnt}; x++ ))
dn
_aebg_x=${_aebg_Excludes[$x]}
for (( n = 0; n < ${_aebg_len}; n++ ))
dn
[ $ -eq 3 ] && ${_aebg_x}*'' # Do prefix edit
if [ ${_aebg_Target[$n]}::= ]
#+ if defined and set.
then
_aebg_t=${_aebg_Target[n]}/#${_aebg_x}/}
[ ${_aebg_t} -eq 0 ] && unset _aebg_Target[$n]
fi
fi
done
```

Appendix A. Contributed Scripts