# More on Subshells 233

```
# Set up default values
mailopt=FALSE
interval=60
```

```
# process command options

while getopts mt: option
do
  case "$option"
    in
      m) mailopt=TRUE;
      t) interval=$OPTARG;
        echo "Usage: mon [-m] [-t] user"
        echo " -m means to be informed by mail"
        echo " -t means check every n secs."
        exit 1)
  esac
done
```

```
# Make sure a user name was specified

if [ "$OPTIND" -gt "#" ]; then
  echo "Missing user name!"
  exit 2
fi
```

```
shiftcount=$(( OPTIND - 1 ))
shift $shiftcount
user=$1
```

```
#
# Send everything that follows into the background
#
(
#
# Check for user logging on
#

until while | grep "*$user " > /dev/null
do
  sleep $interval

```

```
#
# When we reach this point, the user has logged on
#
```