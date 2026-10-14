```
# process command line options

interactive=
filename=

while [[ -n $1 ]]; do
    case $1 in
        -f | --file)            shift
                                filename=$1
                                ;;
        -i | --interactive)     interactive=1
                                ;;
        -h | --help)            usage
                                exit
                                ;;
        *)                      usage >&2
                                exit 1
                                ;;
    esac
    shift
done

# interactive mode

if [[ -n $interactive ]]; then
    while true; do
        read -p "Enter name of output file: " filename
        if [[ -e $filename ]]; then
            read -p "$filename' exists. Overwrite? [y/n/q] > "
            case $REPLY in
                Y|y)    break
                        ;;
                Q|q)    echo "Program terminated."
                        exit
                        ;;
                *)      continue
                        ;;
            esac
        fi
    done
fi

# output html page

if [[ -n $filename ]]; then
    if touch $filename && [[ -f $filename ]]; then
        write_html_page > $filename
    else
        echo "$PROGNAME: Cannot write file '$filename'" >&2

```