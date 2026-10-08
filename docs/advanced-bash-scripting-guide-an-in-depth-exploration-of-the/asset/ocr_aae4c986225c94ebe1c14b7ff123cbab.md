# Advanced Bash-Scripting Guide

```
# a Bash script to make wget bit more friendly, and save typing.

# Carefully crafted by Little Monster.
# More or less complete on 02/02/2005.
# If you think this script can be improved,
# email me at: monster@monstruum.co.uk
# ==> cc: to the author of the ABS Guide, please.
# This script is licensed under the GPL.
# You are free to copy, alter and re-use,
# but please don't to claim you wrote it.
# Log your changes here instead.

# ==================================================
# changelog:

# 07/02/2005. Fixups by Little Monster.
# 02/02/2005. Minor additions by Little Monster.
# (After # +++++)
# 29/01/2005. Minor stylistic edits and cleanups by author of ABS Guide.
# Added edit error codes.
# 22/11/2004. Finished initial version of second version of wget:
# wget2.0 is here.
# 01/12/2004. Changed 'run' function so it can be 2 ways
# either as a file name or have one input on the CL.
# Made sensible handling of URL's given.
# 01/12/2004. Made loop of options, so you don't
# 01/12/2004. have to keep calling wetter 2 all the time.
# Runs as a session.
# 01/12/2004. Added looping to 'run' function.
# Simplified and improved.
# 01/12/2004. Added state to recursion setting.
# Enables re-use of previous value.
# 05/12/2004. Modified the file routine in the 'run' function
# so it's not fooled by empty values, and is cleaner.
# 01/02/2004. Added cookie funding routine from later version (which
# isn't ready yet), so as not to have hard-coded paths.
# ==================================================

# Error codes for abnormal exit:
# E_USAGE=67 # Usage message, then.
# E_NO_OPTS=68 # No command-line arguments.
# E_NO_URL=69 # No URLs passed to script.
# E_NO_SAVEFILE=70 # No filename passed to script.
# E_USER_EXIT=71 # User decides to quit.

# Basic default wget command we want to use.
# This is the place to change it, if required.
# Now if using a proxy, set http_proxy = yourproxy in .wgetrc.
# Otherwise delete --proxy=on, below.
# ====================================================
# CommandA="wget -nc -t 5 --progress=bar --random-wait --proxy=on -r"
# ====================================================

# Set some other variables and explain them.
# pattern="-A .jpg, .JPG, .JPEG, .gif, .GIF, .htm, .html, .shtml, .php"
# wget's option to only get certain types of file.
# Comment out if not using
```

Appendix A. Contributed Scripts

672