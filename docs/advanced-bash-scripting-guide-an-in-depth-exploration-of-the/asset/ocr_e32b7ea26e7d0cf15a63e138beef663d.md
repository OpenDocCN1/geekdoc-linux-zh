# Advanced Bash-Scripting

| IF EXIST FILENAME | if [ -e filename ] | test if file exists |
| IF ! %N==! | if [ -z"$N ] | replaceable parameter "N" not present |
| CALL | source . (dot operator) | "include" another script |
| COMMAND /C | source . (dot operator) | "include" another script (same as CALL) |
| SET | export | set an environmental variable |
| SHIFT | shift | left shift command-line argument |
| SGN | -It -gt | sign of (integer) |
| ERRORLEVEL | $? | exit status |
| CON | stdin | "console" (stdin) |
| PRN | /dev/lp0 | (generic) printer device |
| LPT1 | /dev/lp0 | first printer device |
| COM1 | /dev/ttyS0 | first serial port |

Batch files usually contain DOS commands. These must be translated into their UNIX equivalents in order to convert a batch file into a shell script.

Table N-2. DOS commands and the UNIX equivalents

| DOS Command | UNIX Equivalent | Effect |
| ASSIGN | ln | link file or directory |
| ATTRIB | chmod | change file permissions |
| CD | cd | change directory |
| CHDIR | ed | change directory |
| CLS | clear | clear screen |
| COMP | diff, comm, comp | file compare |
| COPY | cp | file copy |
| Ctl-C | Ctl-C | break (signal) |
| Ctl-Z | Ctl-D | EOF (end-of-file) |
| DEL | rm | delete file(s) |
| DELTREE | rm -rf | delete directory recursively |
| DIR | ls -l | directory listing |
| ERASE | rm | delete file(s) |
| EXIT | exit | exit current process |
| FC | comm, comp | file compare |
| FIND | grep | find strings in files |
| MD | mkdir | make directory |