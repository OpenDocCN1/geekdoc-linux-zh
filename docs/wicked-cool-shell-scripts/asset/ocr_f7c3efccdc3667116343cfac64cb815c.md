```
else
    echo "Warning: Trying to double-compress $name"
fi

# Try compressing all three files in parallel.
$Z < "$name" > $Zout &
$gz < "$name" > $gzout &
$bz < "$name" > $bzout &

wait # Wait until all compressions are done.

# Figure out which compressed best.
smallest="$(ls -l "$name" $Zout $gzout $bzout | \ awk '{"print $5"NR}' | sort -n | cut -d= -f2 | head -1)"

case "$smallest" in
    1 ) echo "No space savings by compressing $name. Left as is." ;;
    2 ) echo Best compression is with compress. File renamed $(name).Z
        mv $Zout "${name}.Z" ; rm -f "$name"
        ;;
    3 ) echo Best compression is with gzip. File renamed $(name).gz
        mv $gzout "${name}.gz" ; rm -f "$name"
        ;;
    4 ) echo Best compression is with bzip2. File renamed $(name).bz2
        mv $bzout "${name}.bz2" ; rm -f "$name"
esac

done

exit 0
```

Listing 4-19: The bestcompress script

# How It Works

The most interesting line in this script is at ②. This line has ls output the size of each file (the original and the three compressed files, in a known order), chops out just the file sizes with awk, sorts these numerically, and ends up with the line number of the smallest resultant file. If the compressed versions are all bigger than the original file, the result is 1, and an appropriate message is printed out ①. Otherwise, smallest will indicate which of compress, gzip, or bzip2 did the best job. Then it’s just a matter of moving the appropriate file into the current directory and removing the original file.

The three compression calls starting at ① are also worth pointing out. These calls are done in parallel by using the trailing & to drop each of them into its own subshell, followed by the call to wait, which stops the script until all the calls are completed. On a uniprocessor, this might not offer much performance benefit, but with multiple processors, it should spread the task out and potentially complete quite a bit faster.