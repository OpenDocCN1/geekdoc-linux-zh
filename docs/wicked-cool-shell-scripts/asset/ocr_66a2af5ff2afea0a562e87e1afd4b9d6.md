```
trap "rm -f $tempfile" EXIT

cat << 'EOF' > $tempfile
{ sum += $4 }
END { mb = sum / 1024
      gb = mb / 1024
      printf "%.0f MB (%.2fGB) of available disk space\n", mb, gb
}
EOF
```

● df -k | awk -f $tempfile

```
exit 0
```

Listing 5-9: The diskspace script, a handy wrapper with friendlier output to df

# How It Works

The diskspace shell script relies mainly on a temporary awk script that is written to the /tmp directory. This awk script calculates the total amount of disk space left using data fed to it and then prints the result in a user-friendly format. The output of df is then piped through awk, which performs the actions in the awk script. When execution of the script is finished, the temporary awk script is removed from the /tmp directory because of the trap command run at the beginning of the script.

# Running the Script

This script, which can be run as any user, produces a succinct one-line summary of available disk space.

# The Results

For the same system that generated the earlier df output, this script reports output similar to that shown in Listing 5-10.

```
$ diskspace
96199 MB (93.94GB) of available disk space
```

Listing 5-10: Testing the diskspace script

# Hacking the Script

If your system has lots of disk space across many multiterabyte drives, you might expand this script to automatically return values in terabytes as needed. If you’re just out of space, it’ll doubtlessly be discouraging to see 0.03GB of available disk space—but that’s a good incentive to use Script #36 on page 121 and clean things up, right?