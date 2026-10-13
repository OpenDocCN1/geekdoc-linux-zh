```
compressed=0

# clean up our temp files before we start
/bin/rm -f /tmp/autocompress.*

for fname in `find $homedir -type f -size $threshold -print | \
egrep -v '(\.Z$|\.gz$|\.tgz$)'`
do
owner=`ls -l $fname | awk '{print $3}'`
if [ $owner = 'root' ]; then
echo "... skipping file $fname (owned by root)"
else
echo 'autocompressing file $fname (owned by $owner)'
gzip $fname
echo "$fname" >> /tmp/autocompress.$owner
compressed=`expr $compressed + 1`
fi
done

# now send out email reports to any users who has had files compressed

if [ $compressed -gt 0 ]; then
for report in `ls /tmp/autocompress.*`
do
recipient=`echo $report | sed 's|/tmp/autocompress.||'`
echo ""
echo "Sending autocompress report to ${recipient}:"
cat $report
(
echo 'In an effort to save disk space, files larger than $threshold'
echo 'are automatically compressed on this system. On a regular sweep'
echo 'through the disk, the following file or files of yours have been'
echo 'identified and auto-compressed:'
cat $report
echo 'To learn how to work with compressed files, please see the '
echo 'gzip man page. You can do this with the command '
echo 'man gzip'
) | mail -s 'Notice: Compressed your big files' $recipient

/bin/rm -f $report
done
echo ""
echo "$compressed file(s) compressed."
else
echo ""
echo "autocompress: no files compressed, no report generated"
fi

exit 0
```