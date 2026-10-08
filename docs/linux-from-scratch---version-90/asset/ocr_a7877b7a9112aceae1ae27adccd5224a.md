# Linux From Scratch - Version 9.0

# Inputs: -f (force) run the program even if it is already running.
# -n nicelevel: specify a nice level. See 'man nice(1)'
# -p pidfile: use the specified file to determine PIDs.
# pathname: the complete path to the specified program
# args: additional arguments passed to the program (pathname)

# Return values (as defined by LSB exit codes):
# 0 - program is running or service is OK
# 1 - generic or unspecified error
# 2 - invalid or excessive argument(s)
# 3 - program is not installed

```
################################################################################
start_daemon() {
    local force=""
    local nice="0"
    local pidfile=""
    local pidlist=""
    local retval=""

    # Process arguments
    while true
    do
        case "${1}" in
            -f)
                force="$1"
                shift 1
                ;;

            -n)
                nice="${2}"
                shift 2
                ;;

            -p)
                pidfile="${2}"
                shift 2
                ;;

            -*)
                return 2
                ;;

            *)
                program="${1}"
                break
                ;;
        esac
    end

    # Check for a valid program
    if [ -e "${program}" ]; then return 5; fi

    # Execute
    if [ -z "${force}" ]; then
        if [ -z "${pidfile}" ]; then
```
```

285