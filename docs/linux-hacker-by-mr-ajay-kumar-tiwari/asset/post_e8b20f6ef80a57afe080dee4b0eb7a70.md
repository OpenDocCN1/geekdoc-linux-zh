
## Linux Hack

Ajay Kumar Tiwari

```
ramesh@dev-db ~> vi ~/.bash_profile
```

```
ramesh@dev-db ~> vi ~/.bashrc
```

[Note: Add export PS1="\u@\h \w> " to one of the above files]

Refer to the next chapter for several practical examples of PS1 usage in detail.

## Hack 30. PS2 - Continuation Interactive Prompt

A very long command can be broken down to multiple lines by giving \ at the end of the line. The default interactive prompt for a multi-line command is ">". Let us change this default behavior to display "continue->" by using PS2 environment variable as shown below.

```
ramesh@dev-db ~> myisamchk --silent --force --fast --update-state \
> --key_buffer_size=512M --sort_buffer_size=512M \
> --read_buffer_size=4M --write_buffer_size=4M \
> /var/lib/mysql/bugs/*.MYI
```

[Note: This uses the default ">" for continuation prompt]

```
ramesh@dev-db ~> export PS2="continue-> "
```

```
ramesh@dev-db ~> myisamchk --silent --force --fast --update-state \
continue-> --key_buffer_size=512M --sort_buffer_size=512M \
continue-> --read_buffer_size=4M --write_buffer_size=4M \
continue-> /var/lib/mysql/bugs/*.MYI
```

[Note: This uses the modified "continue-> " for continuation prompt]

I found it very helpful and easy to read, when I break my long commands into multiple lines using \. I have also seen others who don't like to break-up long commands.

## Hack 31. PS3 - Prompt used by "select" inside shell script

You can define a custom prompt for the select loop inside a shell script, using the PS3 environment variable, as explained below.

### Shell script and output WITHOUT PS3:

```
ramesh@dev-db ~> cat ps3.sh
select i in mon tue wed exit
do
  case $i in
  mon) echo "Monday";;
  tue) echo "Tuesday";;
  wed) echo "Wednesday";;
  exit) exit;;
  esac
done
ramesh@dev-db ~> ./ps3.sh
1) mon
2) tue
3) wed
4) exit
#? 1
Monday
#? 4
```

[Note: This displays the default "#?" for select command prompt]

### Shell script and output WITH PS3:

```
ramesh@dev-db ~> cat ps3.sh
PS3="Select a day (1-4): "
select i in mon tue wed exit
do
  case $i in
  mon) echo "Monday";;
  tue) echo "Tuesday";;
  wed) echo "Wednesday";;
  exit) exit;;
  esac
done
```

```
ramesh@dev-db ~> ./ps3.sh
1) mon
2) tue
3) wed
4) exit
Select a day (1-4): 1
Monday
Select a day (1-4): 4
```

[Note: This displays the modified "Select a day (1-4):" for select command prompt]

## Hack 32. PS4 - Used by "set -x" to prefix tracing output

The PS4 shell variable defines the prompt that gets displayed, when you execute a shell script in debug mode as shown below.

### Shell script and output WITHOUT PS4:

```
ramesh@dev-db ~> cat ps4.sh
set -x
echo "PS4 demo script"
ls -l /etc/ | wc -l
du -sh ~
```

```
ramesh@dev-db ~> ./ps4.sh
  ++ echo 'PS4 demo script'
PS4 demo script
++ ls -l /etc/
++ wc -l
243
++ du -sh /home/ramesh
48K/home/ramesh
```

[Note: This displays the default "++" while tracing the output using set -x]

### Shell script and output WITH PS4:

The PS4 defined below in the ps4.sh has the following two codes:

- $0 - indicates the name of script
- $LINENO - displays the current line number within the script

```
ramesh@dev-db ~> cat ps4.sh
export PS4='$0.$LINENO+ '
set -x
echo "PS4 demo script"
ls -l /etc/ | wc -l
du -sh ~
ramesh@dev-db ~> ./ps4.sh
../ps4.sh.3+ echo 'PS4 demo script'
```

PS4 demo script

```
../ps4.sh.4+ ls -l /etc/
```

51

```
../ps4.sh.4+ wc -l
```

243

```
../ps4.sh.5+ du -sh /home/ramesh
```

48K/home/ramesh

[Note: This displays the modified "{script-name}.{line-number}+" while tracing the output using set -x]

## Hack 33. PROMPT_COMMAND

Bash shell executes the content of the PROMPT_COMMAND just before displaying the PS1 variable.

```
ramesh@dev-db ~> export PROMPT_COMMAND="date +%k:%m:%S"
```

22:08:42

ramesh@dev-db ~>

[Note: This displays the PROMPT_COMMAND and PS1 output on different lines]

If you want to display the value of PROMPT_COMMAND in the same line as the PS1, use the echo -n as shown below.

```
ramesh@dev-db ~> export PROMPT_COMMAND="echo -n [$(date +%k:%m:%S)]"
```

[22:08:51]ramesh@dev-db ~>

[Note: This displays the PROMPT_COMMAND and PS1 output on the same line]

## Chapter 6: Colorful and Functional Shell Prompt Using PS1

## Hack 34. Display username, hostname and basename of directory in the prompt

The PS1 in this example displays following three information in the prompt:

- \u – Username
- \h – Hostname
- \W – Base name of the current working directory

```
-bash-3.2$ export PS1="\u@\h \W> "
ramesh@dev-db ~> cd /etc/mail
ramesh@dev-db mail>
```

## Hack 35. Display current time in the prompt

In the PS1 environment variable, you can directly execute any Linux command, by specifying in the format $(linux_command). In the following example, the command $(date) is executed to display the current time inside the prompt.

```
ramesh@dev-db ~> export PS1="\u@\h [\$(date +%k:%m:%S)]> "
ramesh@dev-db [11:09:56]>
```

You can also use \t to display the current time in the hh:mm:ss format as shown below:

```
ramesh@dev-db ~> export PS1="\u@\h [\t]> "
```

```
ramesh@dev-db [12:42:55]>
```

You can also use \@ to display the current time in 12-hour am/pm format as shown below:

```
ramesh@dev-db ~> export PS1="[\@] \u@\h> "
```

```
[04:12 PM] ramesh@dev-db>
```

## Hack 36. Display output of any command in the prompt

You can display output of any Linux command in the prompt. The following example displays three items separated by | (pipe) in the command prompt:

- \!: The history number of the command
- \h: hostname
- $kernel_version: The output of the uname -r command from $kernel_version variable
- \?: Status of the last command

```
ramesh@dev-db ~> kernel_version=$(uname -r)
```

```
ramesh@dev-db ~> export PS1="\!|\h|$kernel_version|\?> "
```

```
473|dev-db|2.6.25-14.fc9.i686|0>
```

## Hack 37. Change foreground color of the prompt

Display prompt in blue color, along with username, host and current directory information

```
$ export PS1="\e[0;34m\u@\h \w> \e[m "
```

[Note: This is for light blue prompt]

```
$ export PS1="\e[1;34m\u@\h \w> \e[m "
```

[Note: This is for dark blue prompt]

\e[ - Indicates the beginning of color prompt

x;ym - Indicates color code. Use the color code values mentioned below.

\e[m - indicates the end of color prompt

### Color Code Table:

| Color | Code |
|-------|------|
| Black | 0;30 |
| Blue | 0;34 |
| Green | 0;32 |
| Cyan | 0;36 |
| Red | 0;31 |
| Purple | 0;35 |
| Brown | 0;33 |

[Note: Replace 0 with 1 for dark color]

Make the color change permanent by adding the following lines your ~/.bash_profile or ~/.bashrc

```
$ vi ~/.bash_profile
```

```
STARTCOLOR='\e[0;34m';
ENDCOLOR="\e[0m"
export PS1="$STARTCOLOR\u@\h \w> $ENDCOLOR"
```

## Hack 38. Change background color of the prompt

Change the background color by specifying \e[{code}m in the PS1 prompt as shown below.

```
$ export PS1="\e[47m\u@\h \w> \e[m "
```

[Note: This is for Light Gray background]

Combination of background and foreground.

```
$ export PS1="\e[0;34m\e[47m\u@\h \w> \e[m "
```

[Note: This is for Light Blue foreground and Light Gray background]

Add the following to your ~/.bash_profile or ~/.bashrc to make the above background and foreground color permanent.

```
$ vi ~/.bash_profile
STARTFGCOLOR='\e[0;34m';
STARTBGCOLOR="\e[47m"
ENDCOLOR="\e[0m"
export PS1="$STARTFGCOLOR$STARTBGCOLOR\u@\h \w> $ENDCOLOR"
```

Play around by using the following background color and choose the one that match your taste:

- \e[40m
- \e[41m
- \e[42m
- \e[43m
- \e[44m
- \e[45m
- \e[46m
- \e[47m

## Hack 39. Display multiple colors in the prompt

You can also display multiple colors in the same prompt. Add the following function to your ~/.bash_profile

```
function prompt {
    local BLUE="\[\033[0;34m\]"
    local DARK_BLUE="\[\033[1;34m\]"
    local RED="\[\033[0;31m\]"
    local DARK_RED="\[\033[1;31m\]"
    local NO_COLOR="\[\033[0m\]"
    case $TERM in
    xterm*|rxvt*)
    TITLEBAR='\[\033]0;\u@\h:\w\007\]'
    ;;
    *)
    TITLEBAR=""
```
