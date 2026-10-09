```
# Check argument count
usage "$0"

# Set up temporary files for sorting
file1=$TMPDIR/$$.file1
file2=$TMPDIR/$$.file2

# Sort
sort $1 > $file1
sort $2 > $file2

# Open $file1 and $file2 for reading. Use file descriptors 3 and 4.
exec 3<$file1
exec 4<$file2

# Read the first line from each file to figure out how to start.
read line1 <&3
status1=$?
read line2 <&4
status2=$?

# Strategy: while there is still input left in both files:
# Output the line that should come first.
# Read a new line from the file that line came from.
while [ $status1 -eq 0 -a $status2 -eq 0 ]
do
	if [[ "$line2" > "$line1" ]]; then
	echo -e "1.$line1"
	read -u3 line1
	status1=$?
	else
	echo -e "2.$line2"
	read -u4 line2
	status2=$?
	fi
done

# Now one of the files is at end of file.
# Read from each file until the end.
# First $file1:
while [ $status1 -eq 0 ]
do
	echo -e "1.$line1"
	read line1 <&3
	status1=$?
done

# Next $file2:
while [ [ $status2 -eq 0 ]]  
do
	echo -e "2.$line2"
	read line2 <&4
	status2=$?
done

# Close and remove both input files
exec 3<&- 4<&-
rm -f $file1 $file2
exit 0
```