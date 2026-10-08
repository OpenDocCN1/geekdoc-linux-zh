# Advanced Bash-Scripting Guide

```
if [ -f /etc/bashrc ]; then
    /etc/bashrc    # Read /etc/bashrc, if present.
fi
```

```
# Automatic setting of $DISPLAY (if not set already).
# This works for me - your mileage may vary. ...
# The problem is that different types of terminals give
#+ different answers to 'who am i (rxvt in particular can be
#+ troublesome) - however this code seems to work in a majority
#+ of cases.
```

```
function get_xserver() {
    case $TERM in
        xterm)
            XSERVER=$(who am i | awk '{print $NF}' | tr -d '"\'')
            # Ane-Pier Weringa suggests the following alternative:
            _IAM=${_IAM_$(who am i)}
            SERVER=${SERVER%%*}
            XSERVER=${XSERVER%%*}
            ;;
        aterm | rxvt)
            # Find some code that works. ...
            ;;
    esac
}
```

```
if [ -z ${DISPLAY:="} ]; then
    get_xserver()
    if [[ -z ${XSERVER} ]] || [ ${XSERVER} == "$(hostname)" ]; then
        if [ ${XSERVER} == "unix" ]; then
            DISPLAY=${DISPLAY}:.0 # Display on local host.
        else
            DISPLAY=${XSERVER}:0  # Display on remote host.
        fi
fi
```

```
export DISPLAY
```

```
# Some settings
#set -o nounset # These two options are useful for debugging.
#set -o xtrace
alias debug="set -o nounset; set -o xtrace"
```

```
ulimit -s -c 0 # Don't want coredumps.
set -o notify
set -o noobclocker
set -o ignoreeof
```

```
# Enable options:
shopt -s cdspell
shopt -s cdable_vars
shopt -s checkhash
```

Appendix M. Sample .bashrc and bash_profile Files

821