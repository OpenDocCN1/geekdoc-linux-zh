# Advanced Bash-Scripting Guide

```
today=$(date +%F) # Used for a filename.
home=$HOME # Set HOME to an internal variable.

# In some other path is used, change it here.
depthdefault=3 # Set to a simple default recursion.
depth=$depthdefault # Otherwise user feedback doesn't tie in properly.
RefA="" # Set blank referencing page.
Flag="" # Default to not saving,
# or whatever else might be wanted in future.

lister="" # Used for passing a list of urls directly to wget.
Woptions="" # Used for passing some options for itself.
infile="" # Used for the run function.
newfile="" # Used for the run function.
savePath=$HOME/.wgetrc`
Config="" # This is where some variables can be stored,
Cookie_List="$HOME/cookielist" # If permanently changed from within the script.
flag="" # So we know the cookies are kept
# Part of the cookie file selection routine.

# Define the options. Easy to change letters if needed.
# These are the optional options; you don't want to be asked.

save=s # Save command instead of executing it.
cook=c # Change cookie file for this session.
help=# Usage guide.
list # Pass the -i option and URL list.
runr # Run saved commands as an argument to the option.
input=i # Run saved commands interactively.
wopt=w # Enter options to pass directly to wget.
--------------------------------------------------------------------------------
```

```
if [ -z "$1" ]; then # Make sure we get something for wget to eat.
echo "You must at least enter a URL or option!"
echo "-Help for usage.
exit $SE_NO_OPTS
fi
```

```
--------------------------------------------------------------------------------
if [ ! -e "$Config" ]; then # See if configuration file exists.
echo "Creating configuration file, $Config"
echo "This is the configuration file for wetter2" >> "$Config"
echo "Your customised settings will be saved in this file" >> "$Config"
elelse
source $Config # Import variables we set outside the script.
fi
```

```
if [ ! -e "$Cookie_List" ]; then
# Set up a list of cookie files, if there isn't one.
echo "Hunting for cookies..."
find -name cookies.txt >>"$Cookie_List # Create the list of cookie files.
fi # Isolate this in its own 'if' statement,
# in case we got interrupted while searching.
```

```
if [ -z "$Flag" ]; then # If we haven't already done this .
# Make a nice space after the command prompt.
echo
echo "Looks like you haven't set up your source of cookies yet."
```

Appendix A. Contributed Scripts

673