# LISTING 22.1 Complete Listing of the sshd Init Script

```
```bash
1 #!/bin/sh
2
3 USAGE="Usage: $0 | start | stop | enable | disable | "
4
5 # print out an usage message if no arguments are specified
6
7 if [ -z "$0" ] ; then
8 echo "$USAGE"
9 exit 1
10 fi
11
12 # variables that hold the location of the program, any options
13 # that might be required and the name of the program itself
14
15 PGM=/usr/local/sbin/sshd
16 PGM_OPTS=
17 PGM_NAME=`echo $PGM | sed 's/.*\/\//''`
18
19 # determine the correct options for ps
20
21 case `uname -s` in
22 Linux|Darwin|*BSD) PS="/bin/ps auxxx" ;;
23 *) PS="/bin/ps -ef" ;;
24 esac
25
26 # evaluate each argument
27
28 for ARG in $*
29 do
30 case "$ARG" in
31 "start")
32
33 # check if the program is disabled
34
35 if [ -e "/etc/no-$PGM_NAME" ] ; then
36 echo "Error: Program disabled: $PGM" 1>&2
37 exit 1
38 fi
39
40 # verify that the program is executable
41
42 if [ ! -x "$PGM" ] ; then
43 echo "Error: Not Executable: $PGM" 1>&2
44 exit 1
45 fi
46
47 # check if the program is running
48
49 RUNNING=`$PS | grep "$PGM" | grep -v grep | head`
50 if [ -n "$RUNNING" ] ; then
```
```