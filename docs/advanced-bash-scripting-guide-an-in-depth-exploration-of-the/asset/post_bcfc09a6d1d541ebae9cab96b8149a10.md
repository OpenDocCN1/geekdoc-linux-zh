
# Advanced Bash-Scripting Guide

```bash
# Adds some text in the terminal frame (if applicable)

function xtitle()
{
    case "$TERM" in
        *term | rxvt)
            echo -en "\0;$*\a"
        *)
            ;;
    esac
}
```

```bash
# Aliases use xtitle
alias top='xtitle'
alias make='xtitle Making $(basename PWD); make

# and functions
function man()
{
    for i; do
        xtitle The $(basename "$i"|tr -d .[:digit:]]) manual
        command -a "$i"
    done
}
```

```bash
# Make the following commands run in background automatically:

function te()  # wrapper around emacs/gnuserv
{
    if [ "$(gnucle -batch -el 2>&-)" == "t" ]; then
        gnucle -q "$@"
    else
        emacs "$@"
    fi
}
```

```bash
function soff() { command soff "$@" }
function firefox() { command firefox "$@" }
function xpdf() { command xpdf "$@" }
```

```bash
# File & strings related functions:
# Find a file with a pattern in name:
function ff() { find . -type f -iname "*$1*" -ls; }
```

```bash
# Find a file with pattern $1 in name and Execute $2 on it:
function fe() { find . -type f -iname "*$1*" -maxdepth 1 -exec ${2:2-(2-file)} {} \; }
```

```bash
# Find a pattern in a set of files and highlight them:
# (needs a recent version of egrep)
function fstr()
{
    OPTIND=1
}
```

## Appendix M. Sample .bashrc and .bash_profile Files

```bash
local mycase=""
local usage="fstr; find string in files.
Usage: fstr [-i] [filename pattern]"
while getopts :it opt
do
    case "$opt" in
        i) mycase="-$i"; return ;
        *) echo "$usage"; return;;
    esac
done
shift $(( $OPTIND - 1 ))
if [ "$# -lt 1 ]; then
    echo "$usage"
    return;
fi
find . -type f -name "${2%%*:}" -print0 | \
xargs -0 -egrep --color=always -sn "$mycase" "$1" 2>&1 | more
```

```bash
function swap() {
    # Swap 2 files, if they exist (from Uzi's bashrc).
    local TMPFILE=$tmp.emp

    [ ! -e $1 ] && echo "swap: $1 does not exist" && return 1
    [ ! -e $2 ] && echo "swap: $2 does not exist" && return 1
    mv "$1" "$TMPFILE"
    mv "$2" "$1"
    mv "$TMPFILE" "$2"
}
```

```bash
# Creates an archive (*.tar.gz) from given directory.
function maketar() { tar cvzf "${1%%}.tar.gz" "${1%%}/"; }

# Create a ZIP archive of a file or folder.
function makezip() { zip -r "${1%%}.zip" "$1"; }
```

## Appendix M. Sample .bashrc .bash_profile Files

# Advanced Bash-Scripting Guide

```bash
# Make your directories and files access rights sane.
function sanitize() { chmod -R uwX,gRX,o="$@"; }
```

-
# Process/system related functions:

```bash
function my_ps() { ps -e -U "$USER" -o pid,%cpu,%mem,bsdtime,command ; }
function pp() { my_ps | awk '!/awk/ && $0 ~ var=${1:-".*"} ; } }
```

```bash
function kills() {
  # KILLER by process name
  local pid pname="-TERM" # default signal
  if [ "$#" -lt 1 ] || [ "$#" -gt 2 ]; then
    echo "Usage: kills [-SIGNAL] pattern"
    return;
  fi
  if [ $# -eq 2 ]; then sig=$1; fi
  for pid in $(my_ps | awk '!/awk/ && $0 ~ pat="$2"'); do
    pname=$($my_ps | awk '!/awk/ && $0 ~ pat="$2" | head -n 1)
    if ask "Kill $pname with signal $sig?"; then
      kill "$sig" "$pid"
    fi
  done
}
```

```bash
function mydf() {
  # Pre-print of 'df' output.
  # Inspired by 'df' utility.
  for fs; do
    if [ ! -d "$fs" ]; then
      echo "$fs: No such file or directory";
      continue
    fi
    local local_info=$(df -P "$fs" | awk 'END{ print $2,$3,$5 }')
    local local_free=$(df -P "$fs" | awk 'END{ print $4 }')
    local nbstars=$(( local_info / local_free ))
    local out=""
    for ((j=0;j<nbstars;j++)); do
      if [ $j -lt 20 ]; then
        out="$-"
      else
        out=" "
      fi
    done
    echo -e "$out" "$fs"
  done
}
```

```bash
function my_ip() {
  # Get IP on ethernet.
  MY_IP=$(ifconfig eth0 | awk '/inet/ { print $2 }' | sed -e s/\.*//)
  echo "${MY_IP:-Not connected}"
}
```

## Appendix M. .bashrc and .bash_profile Files

# Advanced Bash-Scripting Guide

```bash
function ii() {
  # Get current host info.
  echo -e "\nYou are logged on $HOST"
  echo -e "\nAdditional information:" ; uname -a
  echo -e "\nUsers logged on:" ; w | cut -d ' ' -f1 | sort
  echo -e "\nCurrent date:" ; date
  echo -e "\nMachine uptime:" ; uptime
  echo -e "\nMemory stats:" ; free
  echo -e "\nDiskspace:" ; df /
  echo -e "\nLocal IP Address:" ; my_ip
  echo -e "\nOpen connections:" ; netstat -pan --inet;
}
```

## Misc utilities:

```bash
function repeat() {
  # Repeat n times.
  local i
  max=$1;
  for ((i=1;i<=max; i++)); do
    echo "$2"
  done
}
```

```bash
function ask() {
  # See 'killps' for example of use.
  echo -n "$@ [y/n]: "; read ans
  case $ans in
    [Y]*) return 0;
    *) return 1;
  esac
}
```

```bash
function corename() {
  # Get name of app that created a corefile.
  for file; do
    echo -n $file : gdb --core=$file --batch | head -1
  done
}
```

## PROGRAMMABLE COMPLETION SECTION
# Most are taken from the bash 2.05 documentation and from Ian McDonald's
# 'Bash completion' package (http://www.caliban.org/bash/#completion)
You will in fact need more than recent 3.0 for some features.

Note that most linux distributions provide many completions
# 'out of the box' - however, you might need to make your own day,
# I kept those there as examples.

```bash
if [ "${BASH_VERSION.*}" < "3.0" ]; then
  echo "You will need to upgrade to version 3.0 for full programmable completion features"
  return
fi

shopt -s extglob      # Necessary.
complete -A hostname      rsh rcp telnet login ftp ping disk
complete -A export        printnew
complete -A variable      export -local unset
complete -A enabled       builtin
complete -A alias        alias unalias
complete -A function      function
complete -A user          su mail finger

complete -A help        help      # Currently as builtins.
complete -A stop         stop
complete -A stopped -P '*'  bg
complete -A job -P '*'     fg jobs joined

complete -A directory     mkdir rmdir
complete -A directory     -o default cd

complete -f -o default -X '*,.*(zip|ZIP)'  zip
complete -f -o default -X '**.*(zip|ZIP)'  unzip
complete -f -o default -X '*,.*(GZ)'      compress
complete -f -o default -X '*,.*(gz)'      uncompressed
complete -f -o default -X '*,.*(gz|GZ)'  gzip
complete -f -o default -X '*,.*(gz)'      gunzip
complete -f -o default -X '*,.*(bz2|BZ2)'  bzip2
```

## Documents - Postscript,pdf...
complete -f -o default -X '*,.*(ps|PS)'  gs ghostview ps2ascii
complete -f -o default -X '*,.*(dvi|DVI)' ddvips xxd dvtype
complete -f -o default -X '*,.*(pdf|PDF)'  acroead pdf2ps
'(.gz,.GZ,.bz2|BZ2).'*,.*(@(es|ps)? [ES] [pdf])?'
complete -f -o default -X '*,.*(tex|TEX)'  makeinfo text2dpi text2html text2pdf
complete -f -o default -X '*,.*(tex|TEX)'  tex latex
complete -f -o default -X '*,.*(lyx|LYX)'  lyx html2ps
complete -f -o default -X '*,.*(htm|HTML)'  lynx html2ps

## Multimedia

```bash
complete -f -o default -X '*,.*(GIF|gif|JPG|JPG|BMP|BMP|xpm|xpm|png|PNG)' xmv mp ggview
complete -f -o default -X '*,.*(mp3|MP3)'  mpg123 mpg321
complete -f -o default -X '*,.*(ogg|OGG)'  ogg
complete -f -o default -X '*'
'!@.(MP3|MP3) [ogg|OGG|WAV|WAV]pl|\
u3|um|m|mod|s|3|mit|||flulc|flac)'  xms
complete -f -o default -X '*,.*(?|e|G|MP?(E|G)|wma|avi|AVI|
asf|vob|VOB|dat|vcd|ps|fi|fliv|vim|ram|yuv|mov|MOV|qt|
QT|mp3|MP3) [ogg|OGG|OGM|OGM|MP4|MP4|WAV|WAV|ASX|ASX]'  xine
```
