# Hour 15

1. A sample implementation is

```
ispids() {
  USAGE="usage: ispids [-h] process"
  HEADER=false
  PSCMD="/bin/ps -ef"
  case "$1" in
    -h) HEADER=true ; shift ;;
  esac
  if [ -z "$1" ] ; then
    echo $USAGE
    return 1
  fi
  if [ "$HEADER" = "true" ] ; then
    $PSCMD 2> /dev/null | head -n 1 ;
  fi
  $PSCMD 2> /dev/null | grep "$1" | grep -v grep
}
```

For Linux or FreeBSD, change the variable PSCMD from

```
PSCMD="/bin/ps -ef*"
```

to

```
PSCMD="/bin/ps -auxe*"
```

2. The following is one possible implementation:

```
ispids () {
  USAGE="usage: ispids [-h -s] process";
  HEADER=false;
  SORT=false;
  PSCMD="/bin/ps -efk";
  SORTCMD="sort -rnk 2,2";
  for OPT in $8;
  do
    case "$OPT" in
      -h)
        HEADER=true;
        shift
        ;;
      -s)
        SORT=true;
        shift
        ;;

```