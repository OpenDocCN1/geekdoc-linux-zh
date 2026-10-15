system itself. The first argument is the command or sequence of commands you want invoked, and all subsequent arguments are the specific signals (events). In this case, we’re telling the shell that when the script exits, invoke rm to remove the two temp files.

What’s particularly nice about working with trap is that it works regardless of where you exit the script, not just at the very bottom. In subsequent scripts, you’ll see that trap can be tied to a wide variety of signals, not just SIGEXIT (or EXIT, or the numeric equivalent of SIGEXIT, which is 0). In fact, you can have different trap commands associated with different signals, so you might output a "cleaned-up temp files" message if someone sends a SIGQUIT (CTRL-C) to a script, while that wouldn’t be displayed on a regular (SIGEXIT) event.

# Running the Script

This script works either with an input stream, in which case it saves the input to a temp file and then processes the temp file as if its name had been specified on the command line, or with a list of one or more files on the command line. Listing 4-14 shows passing a single file via the command line.

# The Results

```
$ cgrep -c 1 teacup ragged.txt
----- ragged.txt -----
in the wind, and the pool rippling to the waving of the reeds--the
rattling teacups would change to tinkling sheep-bells, and the
Queen’s shrill cries to the voice of the shepherd boy--and the
```

Listing 4-14: Testing the cgrep script

# Hacking the Script

A useful refinement to this script would return line numbers along with the matched lines.

# #33 Working with Compressed Files

Throughout the years of Unix development, few programs have been reconsidered and redeveloped more times than compress. On most Linux systems, three significantly different compression programs are available: compress, gzip, and bzip2. Each uses a different suffix (.z, .gz, and .bz2, respectively), and the degree of compression can vary among the three programs, depending on the layout of data within a file.

Regardless of the level of compression, and regardless of which compression programs you have installed, working with compressed files on many Unix systems requires decompressing them by hand, accomplishing the desired tasks, and recompressing them when finished. Tedious, and thus a