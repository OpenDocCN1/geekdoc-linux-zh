# Appendix A Shell Summary

```
do
  case "$opt"
    in
      r) rflag=1;
      O) oflag=1
        file=$OPTARG;
      \?) echo "$usage"
    esac
    exit 1;
```

```
if [ $OPTIND -gt $# ]
then
  echo "Needs input file!"
  echo "$usage"
  exit 2
fi
```

```
shift $((OPTIND - 1))
if=$1
```

# The hash Command

**General Format:** hash `commands`

This command tells the shell to look for the specified commands and to remember what directories they are located in. If `commands` is not specified, a list of the hashed commands is displayed.

If the format

```
hash -r
```

used, the shell removes all commands from its hash list. Next time any command is executed, the shell uses its normal search methods to find the command.

*Examples*

```
hash rolo whoq
hash
hash -r
```

Add rolo and whoq to hash list
Print hash list
Remove hash list

# The if if Command

**General Format:**

```
if command;
then
```