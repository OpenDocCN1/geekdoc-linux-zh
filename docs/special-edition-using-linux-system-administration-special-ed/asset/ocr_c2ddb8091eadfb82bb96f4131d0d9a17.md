```
```sh
cat <<EOF > $report
`hostname`: Failed SU report:`date`
EOF
#
# Check failed attempts to gain super user access over the past 2 days
#
# Print a header line
cat <<EOF >> $report
Failed super user login attempts reported in /var/log/messages
EOF
today=`date` awk '{printf "%s %s\n", $2, $3}'
yesterday=`date | awk '{printf "%s %s\n", $2, $3-1}'`
grep "$yesterday" /var/log/messages | grep 'authentication failure' \
    | grep 'su service' >> $report
grep "$today" /var/log/messages | grep 'authentication failure' \
    | grep 'su service' >> $report

Mail -n -s "Failed SU Report: `date`" $MAILTO < $report

rm -f $report
```
```