# *GNOME now acts weird after I upgraded it.*

Remove your local setting by deleting the .GNOME directories in your home directory. Try again.

# *The configure script fails and I am not sure why.*

Check the message it failed with, and if you still don't know why, read the contents of the file config.log. Everything the configure script does is reported in that file.

# *Ok, I fixed the problem with the configure script, but it still fails.*

Remove the file config.cache and try again.

# *Some applications don't run anymore now that I upgraded one of my libraries.*

Read the README file that came with the libraries to see whether it says anything about broken applications. Recompile the applications that don't run.

# *The kernel won't compile after I upgraded my GCC.*

Well, if you upgraded to GCC 2.95, this is expected. Revert back to the old one or compile the kernel on a different machine. ●