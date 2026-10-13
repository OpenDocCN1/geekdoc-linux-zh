
![](img/3def70414996f811615f713b2077a154_476_0.png)

## APPENDIX D

### Shell Function Library

This appendix contains the complete shell function library from Chapter 21, "Problem Solving with Functions." The library can be downloaded using the following URL:

http://www.csua.berkeley.edu/~ranga/downloads/tysp2/libtysp2.sh

### LISTING D.1 Listing of the Library libTYP S2.sh

```sh
# Name: printError
# Desc: prints an error message to STDERR
# Args: $0 -> message to print

printError () {
  echo "ERROR: $0" 1>&2
}

# Name: printWarning
# Desc: prints a message to STDERR
# Args: $0 -> message to print

printWarning () {
  echo "WARNING: $0" 1>&2
}
```

### LISTING D.1 Continued

```sh
# Name: promptYESNO
# Desc: Asks a yes/no question
# Args: $1 -> The prompt
#       $2 -> The default answer (optional)
# Global: YESNO -> set to the users response y for yes, n for no

promptYESNO () {
    YESNO=""

    if [ "${1:-t}" ] ; then
        return 1
    fi

    _YNPROMPT="$1 (y/n)? "
    _YNDEFANS=""

    case "$2" in
        [yY][eE][sS] ) _YNDEFANS="y" ;;
        [nN][oO] ) _YNDEFANS="n" ;;
    esac

    _YNPROMPT="$_YNPROMPT[${_YNDEFANS:-[${_YNDEFANS}]}] "

    while :
    do
        printf " $_YNPROMPT"
        read YESNO
        case "${YESNO:-${_YNDEFANS}}" in
            [yY][eE][sS] )
                YESNO="y"
                break
                ;;
            [nN][oO] )
                YESNO="n"
                break
                ;;
            * ) YESNO="" ;;
        esac
    done

    unset _YNPROMPT _YNDEFANS
    export YESNO
    return 0
}

# Name: promptRESPONSE
# Desc: Asks a question
# Args: $1 -> The prompt
```

### LISTING D.1 Continued

```bash
# $2 -> The default answer (optional)
# Globals: RESPONSE -> set to the users response

promptRESPONSE () {
    RESPONSE=""

    if [ $# -lt 1 ] ; then
        return 1
    fi
    _RDEFANS="${2:2:$2}"
    _RPROMPT="${1} [${_RDEFANS}:${_RDEFANS}] "

    while :
    do
        printf '%s' "$_RPROMPT"
        read RESPONSE
        RESPONSE="${RESPONSE:-$_RDEFANS}"
        if [ -n "$RESPONSE" ] ; then
            break
        fi
    RESPONSE=""
    done
    unset _RDEFANS _RPROMPT
    export RESPONSE
    return 0
}

# Name: getSpaceFree
# Desc: Outputs the space avail for a directory
# Args: $1 -> The directory to check

getSpaceFree () {
    if [ $# -ge 1 ] ; then
        df -k "$1" 2>/dev/null | awk 'NR != 1 { print $4; }'
        return 0
    fi
    return 1
}

# Name: getSpaceUsed
# Desc: output the space used for a directory
# Args: $1 -> The directory to check

getSpaceUsed () {
    if [ -d "$1" ] ; then
        du -sk "$1" | awk '{ print $1; }'
```

### LISTING D.1 Continued

```sh
return $?
return 1
}
# Name: getPID
# Desc: Outputs a list of process id matching $1
# Args: $1 -> the command name to look for
getPID() {
    if [ $# -lt 1 ]; then
        return 1
    fi
    PSOPTS="-ef"
    /bin/ps $PSOPTS | grep "$1" | grep -v grep | awk '{ print $2; }'
}
# Name: getUID
# Desc: outputs a numeric user id
# Args: $1 -> a user name (optional)
getUID() {
    id $1 | sed -e 's/(.*// ' -e 's/^uid=//'
}
# Name: toLower
# Desc: changes an input string to lower case
# Args: $0 -> string to change
toLower() {
    echo $0 | tr '[A-Z]' '[a-z]' ;
}
# Name: toUpper
# Desc: changes an input string to upper case
# Args: $0 -> string to change
toUpper() {
    echo $0 | tr '[a-z]' '[A-Z]'
}
```

![](img/3def70414996f811615f713b2077a154_480_0.png)

## INDEX

### Symbols

& (ampersand), background processes, 106
&& and compound operator, 273
-atime option, find command, 301
` (backquote), command substitution, 143
\ (backslash)
echo command escape sequences, 155-156
newline character, 154
quoting, 148-149
tr command, 239
#| bin/sh, 404
{ } (braces), while statement, 286
-c option, uniq command, 242

$ character, 10
; character, 12
: character, 24
shell command, 294-296
if statement, 295
while statement, 295-296
/ character, 53
# character, comments, 30
- character, getopts command, 206
+ character, shell tracing, 333
: (colon), 420
;; command, case statement, 175
. command, including functions and variable definitions in other files, 409
--ftime option, find command, 301

$ (dollar sign)
field operator, 269
newline character, 153
quoting with double quotes, 151
" (double quote), quoting, 150
-exec action, find command, 303-304
-f option, tail command, 234
-i option, grep command, 236
-k option, sort command, 243
-l option, grep command, 238
[>] (less than sign), quoting, 150
^M (carriage return) removing from files, 415-416

-m option, uname command, 393
$ (meta-character), 252
* (meta-character), 252
. (meta-character), 252
\ (meta-character), 252
-mtime option, find command, 301
-n option, 328
find command, 300
grep command, 327
sort command, 242-243
$? variable, 198
^ (negation operator), 254
! operator, 171
until loop, 187
>> operator, here documents, 80
|= operator, test command, 169
|| operator, 171, 408
&& operator, 171, 408
|| (or) compound operator, 273
% (percent sign), job number prefixes, 109
. (period), 39, 420
-print action, find command, 303
-r option
sort command, 242-243
uname command, 393
-s option, tr command, 240
[<>] (redirection sign), eval command, 294
; (semicolon), 148
awk command, 269

! sign, find command, 303
' (single quote), filtering, 244
-size option, find command, 302
-type option, find command, 300
$USAGE variable, 202
-v option, 351
grep command, 236-237
$? variable, 198
$# variable, 198, 203
$* variable, 198
$@ variable, 198
compared to $* @, 204
$0 variable, 198-199, 404
usage statements, 199-200
$? variable, 198
$@ variable, 198
compared to $*, 204
variable values, 124
* wildcard
basename command, 202
globbing, 136
* wildcard, globbing, 139
? wildcard, globbing, 138
common errors, 138-139
-x option, 332

### A

a- option, 39
absolute pathnames, 56
find command, 299
abstraction, portability, 397-400
accounts, 14

actions (find command)
-exec, 303-304
-print, 303
adaptability, init script, 372-373
addperson script, 378-379
address books, 373-374
adding people, 377-380
deleting people, 380-383
interactive mode, 377
listing people in, 375-377
noninteractive mode, 377
ALARM signals, handler function, 321
alias command, 217
aliases, 217, 420
C shells, 16
displaying pathnames for, 206
functions, comparing, 217-218
unaliases, 218
ampersand (&), background processes, 106
anchoring, regular expressions, 254-256
and-and operator (&&), 273
appending output to files, 78
arguments, 200
basename command, 201
emulating, 202
cd command, 59
considering one at a time, 409
example, 201
forwarding to another command, 410

functions, executing, 215-216
mkdir command, 63
passing to commands with xargs command, 304
shell tracing, 335
troubleshooting, 203-205
arithmetic
be command, 307
expr command, 306
arithmetic expressions, 425
arithmetic substitution, 144
common errors, 145-146
operators, 144-145
precedence, 145
array variables, 121-127, 427
arrays
accessing values, 127-128
indices, 126
notation, 126
support arrays, 427
assigning variables, awk, 276
assignment operators, numeric expressions, 278-279
associating files with file descriptors, 82-83
AT&T System V UNIX
See System V UNIX
awk
invocation syntax, 250
operations, 250-251
versus sed, 250

awk command, 268-269
comparison operators, 271-272
compound expressions, 273
next command, 273-274
field editing, 269-270
flow control, 283
do statement, 286
for statement, 286-288
if statement, 284-285
while statement, 285
formatting address book with, 375
FS, 282
numeric variables, 277
pattern-specific actions, 270-271
STDIN as input, 274-275
variables, 276
numeric expressions, 276-283

### B

background processes, 106-107
fg command, 110
input, requiring, 107-108
moving foreground processes to, 108-110
preventing termination, 110
waiting for, 111

backquote (`), command substitution, 143
backslash (\), 148-149
echo command escape sequences, 155-156
newline character, 154
backslash character (\), tr command, 239
basename command, 201-202, 412
bash (Bourne Again shell), 17, 15
exporting variables, 130
initialization, 25
online resources, 34
Bash shell
integer expressions, 425
support arrays, 427
wildcards, 430
bc command, 307-308
beeps, sounding a series with sleep command, 297
BEGIN pattern, numeric expressions, 279-280
Berkeley Software Distribution (BSD), 390
bg, 420
bg command, 109
bit bucket, 405
block special files, 94
Bourne Again shell (bash), 17
arrays, 125
initialization, 25
online resources, 34
wildcards, 430
