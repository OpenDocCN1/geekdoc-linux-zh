# Advanced Bash-Scripting Guide

the Field-Array-Name:
Index-Array-Name[Line-Number * 2] : The "inode" field element.
NOTE: This distance may be +11 or +12 elements.
Index-Array-Name[(Line-Number * 2) + 1] : The "pathname" element.
NOTE: This distance may be a variable number of elements.
Next line index pair for Line-Number+1.
IndexListoc

```
IndexList() {
    local -a INDEX=( 0 0 )
    local -i LidxCnt
    local -i if=0 # Default to variable names

    case "#" in # Simplistic option testing
        0) return 1;
        1) return 1;
        2) ;;
        3) case "$1" in # Poor man's continue
            -if) if=1;
            -of) of=1;
            *) return 1;
        esac; shift;
        4) if=1; of=1; shift; shift;
        *) return 1
    esac
```

# A little elegance here would handle pipes,
++ sockets, deleted files - later.

# Appendix A Contributed Scripts