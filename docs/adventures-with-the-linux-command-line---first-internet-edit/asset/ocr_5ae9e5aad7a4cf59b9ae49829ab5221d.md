```
# Create a temporary file and make sure it goes away when we're
tmp_file=$(mktemp 2>/dev/null) | tmp_file=/tmp/test$
trap "rm -f $tmp_file" 0 1 2 3 15
```

```
# Generate the dialog box
dialog --title INPUT BOX \
clear \
--inputbox \
\nn, this is an input dialog box. You can use \n\nthis to ask questions that require the \n\ninput as a string of length longer than the \n\nwidth of the input box, in that case, the \n\ninput field will be automatically scrolled. \n\nYou can use BACKSPACE to correct errors. \n\nTry entering your name below: \"
16 5 1 2 $tmp_file
```

```
# Get the exit status
return_value=$?

# Act on
case $return_value in
$DIALOG_OK)
echo "Result: $(cat $tmp_file)";
$DIALOG_CANCEL)
echo "Cancel pressed.";
$DIALOG_HELP)
echo "Help pressed.";
$DIALOG_EXTRA)
echo "Extra button pressed.";
$DIALOG_ITEM_HELP)
echo "Item-help button pressed.";
$DIALOG_ESC)
if test -s $tmp_file; then
cat $tmp_file
else
echo "ESC pressed.";
fi
nesac
```

The first part of the script defines some constants that are used to represent the six possible status values supported by dialog. They are used to tell the calling script which button on the dialog box (or, the Esc key) was used to terminate the dialog. The construct to do this is somewhat effortless. First, each line begins with the null command "-" which is a command that does nothing. Yes, really. It Intentionally does nothing, because sometimes we need a command (for syntax reasons) but actually want to do anything. Following the null command is parameter expansion. The expansion is simpler in form than we consider in Chapter 34 of TLCL.

```
${parameter:=value}
```

This sets a default value for a parameter (variable) that is either unset (it does not exist at all) or is set, but empty. The example code is being very cautious and

# 82 dialog