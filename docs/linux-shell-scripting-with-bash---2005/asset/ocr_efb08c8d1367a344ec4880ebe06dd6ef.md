```
VALUE=\$\{VAR\#\+=\}"                  # variable's encoded value is after =

# Process any hex values

while true ; do
    PART1=\$\{VALUE0\$\*\}"          # value before last %
    if [ "\$PART1" = "\$VALUE" ] ; then # same as whole value?
        break                              # then no % left
    fi
    TMP=\$\{VALUE\#\*\$\}"            # value after last %
    HEXA=\$\{TMP:0:2\}"                # extract two digit hex code
    PART2=\$\{TMP:2\}"                  # value after the hex code
    VALUE=\$"\$PART1"\$printf "\\x\$HEX""\$PART2" # combine, replacing hex code
done
    printf "Var \$id \$s is `\$s`/n" \$CNT "\$NAME" "\$VALUE" # display variable
    if [ "\$REMAINING" = "\$VARIABLES" ] ; then # remaining same as last?
        printf "\$s"\n" "<br />"           # all variables done
        printf "%s\n" "End of CGI variables<br />" # display end message
        break
    fi
    VARIABLES="\$REMAINING"               # do remaining variables
    CNT=CNT+1                              # increment count
done

) # end of decode
readonly -f decode
declare -t decode

# Declarations

declare -rx SCRIPT=\$\{0\#\*/\}
declare GATEWAY_INTERFACE
if [ ! -z "\$GATEWAY_INTERFACE" ] ; then
    printf "\$s\n" "\$SCRIPT: this script should be run by a web browser" >&2
    exit 192
fi

declare -rx ERRORS=\`mktemp /tmp/env.errors.XXXXX`\`
if [ ! -z "\$ERRORS" ] ; then
    ERRORS=\`/tmp/env.errors.\$*\`
    printf "\$s\n" "\`mktemp failed\`" 2> "\$ERRORS"
fi
declare QUERY_STRING               # ensure QUERY_STRING exists
declare REQUEST_METHOD               # ensure REQUEST_METHOD exists

# Write Response Header
```