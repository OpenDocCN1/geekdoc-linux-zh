# Advanced Bash-Scripting Guide

```
echo "If you gave url's on the command-line, I'll use those first."
# Report wget standard behaviour to the user.
lister- -i $urlfile # This is what we want to pass to wget.
return
fi
done
```

```
cookie_func() # Give the user the option to use a different cookie file.
{
while [ 1 ]; do
echo "Change the cookies file. Press return if you don't want to change
it."
read Cookies
# NB: this is not the same as Cookie, earlier.
# There is an 's' on the end.
# Bit like chocolate chips.
if [ -z "Cookies" ]; then # Escape clause for wusses
return
elif [ -e "Cookies" ]; then
echo "File does not exist. Try again." # Keep going. . . .
else
CookiesOn=--local-cookies $Cookies # File is good use it!
return
}
done
```

```
run_func()
{
if [ -z "OPTARG" ]; then
# Test to see if we used the in-line option or the query one.
if [ -d "$SavePath" ]; then # If directory doesn't exist . . .
echo "$SavePath does not appear to exist."
echo "Please supply path and filename of saved wget commands:"
read newFile
until [ -f "$newFile" ]; do # Keep going till we get something.
echo "Sorry, file does not exist. Please try again."
# Try really hard to get something.
read newFile
done
```

```
if [ -z $( grep wget $${newFile} ) ]; then
# Assume they haven't got the right file and bail out.
echo "Sorry, that file does not contain wget commands.  Aborting."
exit
fi
# This is bogus code.
# It doesn't actually work.
# If anyone wants to fix it, feel free! 
```

```
filePath="${newFile}"
else
echo "Save path is $SavePath"
```

Appendix A. Contributed Scripts