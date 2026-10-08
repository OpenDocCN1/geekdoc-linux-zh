```
log_warning_msg "${i} is not executable, skipping."
SCRIPT_STAT="1"
fi

run()
{
    if [ -z $interactive ]; then
        ${1} $($2)
        return $?
    fi

    while true; do
        read -p "Run $($1) $($2) (Yes/no/continue)? " -n 1 run
        echo
        case $($1) in
            c | C)
                interactive=""
                $($1) $($2)
                ret=$?
                break;
                ;;
            n | N)
                return 0
                ;;
            y | Y)
                $($1) $($2)
                ret=$?
                break;
                ;;
        esac
    done
    return $$
}
```

# Read any local settings/overrides
[ -r /etc/sysconfig/rc.site ] && source /etc/sysconfig/rc.site
DISTRO=$DISTRO-"Linux from Scratch"
DISTRO_CONTACT=$DISTRO_CONTACT-"lfs-dev@linuxfromscratch.org (Registration required)
DISTRO_MINI=$DISTRO_MINI-"LFS"
IPROMPT=$IPROMPT-"no"

# These 3 signals will not cause our script to exit
trap "" INT QSTP

```
[ "${1}" != "" ] && runlevel=$($1)

if [ "${runlevel}" == "" ]; then
    echo "Usage: $0 <runlevel>" >&2
    exit 1
fi
```