# Advanced Bash–Scripting Guide

```
SITE=`domainname`.toronto.edu
# ==> `domainname` similar to 'hostname'
# ==> May rewrite this to parameterize for this general use.

usage="Usage: $0 [-h remotehost] [-d remotirectory]... [-f remfile:localfile] ... \
  [-c localdirectory] [-m filename] [-v]"
ftpflags="i -n*"
varflag=""
set x="# So we use globbing in -m*"
set x 'getopts d:ic:f:'
if [ $? -ne 0 ]; then
    echo "$usage"
    exit 65
fi
shift
trap 'rm -f "$TMPFILE"; exit 0 1 2 3 15' EXIT
echo "user anonymous ${USER-gnu}@${SITE}" > ${TMPFILE}
# ==> Added quotes (recommended in complex echoes)
echo binary >> ${TMPFILE}
for i in $@
do
    case $i in
        -v) varflag=-v; echo hash >> ${TMPFILE}; shift;
        -h) remothost=$2; shift 2;
        -d) echo cd $2 >> ${TMPFILE};
            if [ "$varflag" != "$x" ]; then
                echo passwd >> ${TMPFILE};
            fi;
            shift 2;
        -c) echo cd $2 "$2" >> ${TMPFILE}; shift 2;
        -f) fi-expr="$2" = "([^[::]]**"; f2="$2" = "[[::]]*(:.+)"
            echo get $($f2) >> ${TMPFILE}; shift 2;
        *) break;
    esac
done
if [ $# -ne 0 ]; then
    echo $usage
    exit 65 # ==> Changed from "exit 2" to conform with standard.
fi
if [ "$varflag" != "$x" ]; then
    ftpflags="${ftpflags}-v"
fi
if [ "$remhost" = "" ]; then
    remotep=prep.ai.mit.edu
    # ==> Rewrite to your favorite ftp site.
fi
echo quit >> ${TMPFILE}
# ==> All commands saved in template.

tftp ${ftpflags} ${remhost} < ${TMPFILE}
# ==> Now, tempfile batch processed by ftp.

rm -f ${TMPFILE}
# ==> Finally, deleted template (you may wish to copy it to a logfile).

# ==> Exercises:
# ==> 1) Add error checking.
# ==> 2) Add bells & whistles.
```

Appendix A. Contributed Scripts

350