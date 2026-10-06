# Advanced Bash–Scripting Guide

```
_configure_func ()
{
    case "$2" in
        *) ;;
        *) return ;;
    esac

    case "$1" in
        \*) eval cmd=$1 ;;;
        *) cmd="$1";;
    esac
}
nCOMPRELY=$( "$cmcmd" --help | awk '{if ($1 ~ -.*/) print $1}' | grep "^$2" | sort -u)

complete -F _configure_func configure

# cvs (1) completion
_cvs ()
{
    local cur prev
    COMPRELY=()
    cur=$(COMP_WORDS[COMP_CWORD])
    prev=$(COMP_WORDS[COMP_CWORD-1])

    if [ $COMP_CWORD -eq 1 ] || [ "${prev:0:1}\ = "-" ]; then
        COMPRELY=($0 compgen -w addin commit diff \
            export history import log diff release rtag status \
            tag update' $cur)
    else
        COMPRELY=($0 compgen -f $cur)
    fi
    return 0
}
complete -F _cvs cvs
```

```
_killall ()
{
    local cur prev
    COMPRELY=()
    cur=$(COMP_WORDS[COMP_CWORD])

    # get a list of processes (the first sed evaluation
    # takes care of swapped processes, the second
    # takes care of getting the basename of the process)
    COMPRELY=($0 /usr/bin/ps -u $USER -o comm | \
        sed -e '1,d' -e 's/[#][]//@' -e 's/.*$##' | \
        awk 'if ($0 ~ /^$cur\/) print $0')

    return 0
}
complete -F _killall killall killps
```

# Local Variables:
# mode:shell-script
# sh-shell:bash
# End.

Appendix G. A Sample .bashrc file

378