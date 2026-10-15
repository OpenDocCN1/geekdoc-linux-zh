```
else
    echo "{$lineno}p" >> $sedscript
fi
matches="$(( $matches + 1 ))"
done

if [ $matches -gt 0 ] ; then
    sed -n -f $sedscript $1 | uniq | more
fi
}

trap "$($which rm) -f $tempout $sedscript" EXIT

if [ -z "$1" ] ; then
    echo "Usage: $0 [-c X] pattern {filename}" >&2
    exit 0
fi

if [ "$1" = "-c" ] ; then
    context="$2"
    shift; shift
elif [ "$(echo $1 | cut -c1-2)" = "-c" ] ; then
    context="$(echo $1 | cut -c3-)"
    shift
fi

pattern="$1"; shift

if [ $# -gt 0 ] ; then
    for filename ; do
        echo "----- $filename -----"
        showMatches $filename
    done
else
    cat - > $tempout    # Save stream to a temp file.
    showMatches $tempout
fi

exit 0
```

Listing 4-13: The cgrep script

# How It Works

This script uses grep -n to get the line numbers of all matching lines in the file ① and then, using the specified number of lines of context to include, identifies a starting ② and ending ③ line for displaying each match. These are written out to the temporary sed script defined at ④, which executes a word substitution command that wraps the specified pattern in bold-on and bold-off ANSI sequences. That's 90 percent of the script, in a nutshell.

The other thing worth mentioning in this script is the useful trap command ⑤, which lets you tie events into the shell's script execution