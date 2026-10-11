# **Listing 9.6 Continued**

```
exit 192
fi

# Test parameters

RESULT=`getopt --name "$SCRIPT" --options "$OPTSSTRING" \
  --longoptions "help" \ -- "@$"
if [ $? -gt 0 ] ; then
exit 192
fi

# Replace the parameters with the results of getopt

eval set -- "$RESULT"

# Process the parameters

while [ $# -gt 0 ] ; do
  case "$1" in
    -h | --help) # Show help
      printf "${N}" "Usage: $SCRIPT [-h][--help] -c companyid"
      exit 0
    ;/
    -c ) shift
      if [ $# -eq 0 ] ; then
        printf "$SCRIPT;$LINENO: %${N}" "company for -c is missing" >&2
        exit 192
      fi
      COMPANY="$1"
    ;/
  esac
  shift
done

if [ -z "$COMPANY" ] ; then
  printf "${N}" "company name missing" >&2
  exit 192
fi

printf "$SCRIPT: ${N}" "Processing files for $COMPANY..."

# <-- begin work here

exit 0
```