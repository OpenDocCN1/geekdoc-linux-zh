# Advanced Bash-Scripting Guide

```
MX) Mail Server Record
# Domain name being serviced (wildcards not handled here)
if den_str=${name_fixup $${den_tmp[0]}}
then
    den_name=${#_den_name[0]}=${den_str}
    den_ref=${#_den_ref[0]}}=${den_who}' '${den_str}' MX
fi
## Domain name of service provider
if den_str=${name_fixup $${den_tmp[5]}}
then
    den_name=${#_den_name[0]}=${den_str}
    den_ref=${#_den_ref[0]}}=${den_who}' '${den_str}' MXH
    den_ns=${#_den_ns[0]}=${den_str}' MX
    den_pc=${#_den_pc[0]}=${den_who}' '${den_str}'
fi;
```

```
PTR) Reverse address record
# Special name
if den_str=${name_fixup $${den_tmp[0]}}
then
    den_ref=${#_den_ref[0]}}=${den_str}' PTR
# Host name (not a CNAME)
if den_str2=${name_fixup $${den_tmp[4]}}
then
    den_rev=${#_den_rev[0]}=${den_str}' '${den_str2}
    den_ref=${#_den_ref[0]}}=${den_who}' '${den_str2}' PTRH
    den_pc=${#_den_pc[0]}=${den_who}' '${den_str}'
fi;
```

```
AAAA) (IP6) Address
if den_str=${name_fixup $${den_tmp[0]}}
then
    den_name=${#_den_name[0]}=${den_str}
    den_pair=${#_den_pair[0]}=${den_tmp[4]}' '${den_str}
    den_na=${#_den_na[0]}=${den_str}' '${den_tmp[4]}
    den_ref=${#_den_ref[0]}}=${den_who}' '${den_str}' AAAA
else
    den_pair=${#_den_pair[0]}=${den_str}' unknown.domain'
    den_na=${#_den_na[0]}=unknown.domain '${den_tmp[4]}
    den_ref=${#_den_ref[0]}}=${den_who}' unknown.domain'
fi;
```

```
# No processing for IPv6 addresses
den_pc=${#_den_pc[0]}=${den_who}' '${den_tmp[4]}'
fi;
```

```
CNAME) Alias name record
# Nickname
if den_str=${name_fixup $${den_tmp[0]}}
then
    den_name=${#_den_name[0]}=${den_str}
    den_ref=${#_den_ref[0]}}=${den_who}' '${den_str}' CNAME
    den_pc=${#_den_pc[0]}=${den_who}' '${den_str}'
fi;
```

```
# Hostname
if den_str=${name_fixup $${den_tmp[4]}}
then
    den_name=${#_den_name[0]}=${den_str}
    den_ref=${#_den_ref[0]}}=${den_who}' '${den_str}' CHOST
    den_pc=${#_den_pc[0]}=${den_who}' '${den_str}'
```