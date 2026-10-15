This can be accomplished by using the script as a wrapper. The basic idea of wrappers is that they live between an actual Unix command and the user, offering the user useful functionality that's not available with the original command alone.

> Wrappers are such a powerful concept that you'll see them show up time and again as you go through this book.

# The Code

```
#!/bin/bash
# logrm--logs all file deletion requests unless the -s flag is used

removelog="/var/log/remove.log"

① if [ "$#" -eq 0 ] ; then
    echo "Usage: $0 [-s] list of files or directories" >&2
    exit 1
fi

② if [ "$1" = "-s" ] ; then
    # Silent operation requested ... don't log.
    shift
else
    echo "$(date): $(USER): $0 $@" >> $removelog
fi

③ /bin/rm "$@"

exit 0
```

Listing 2-10: The logrm shell script

# How It Works

The first section ① tests the user input, generating a simple file listing if no arguments are given. Then at ②, the script tests whether argument 1 is -s; if so, it skips logging the removal request. Finally, the timestamp, user, and command are added to the $removelog file ③ and the user command is silently passed over to the real /bin/rm program ④.

# Running the Script

Rather than giving this script a name like logrm, a typical way to install a wrapper program is to rename the underlying command it's intending to wrap and then install the wrapper using the original command's old name. If you choose this route, however, make sure that the wrapper invokes the newly renamed program, not itself! For example, if you rename /bin/rm to /bin/rm.old, and name this script /bin/rm, then the last few lines of the script will need to be changed so that it invokes /bin/rm.old instead of itself.