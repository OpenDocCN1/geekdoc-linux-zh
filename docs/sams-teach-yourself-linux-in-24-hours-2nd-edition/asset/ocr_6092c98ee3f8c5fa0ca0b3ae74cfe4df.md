# LISTING 6.1 CONTINUED

```
# d - delete any files found on the command line
if [ $delete = true ]
then
mv $2 $3 $4 $5 $HOME/.trash
/bin/echo " rmv finished."
fi

# e - empty the trash?
if [ $empty = true ]
then
/bin/echo "empty the trash? \c"
read answer
case "$answer" in
y) rm -fr $HOME/.trash/* ;;
n) /bin/echo "trashcan delete aborted." ;;
esac
fi

# l - show any files in the .trash directory
if [ $list = true ]
then
ls -l $HOME/.trash
fi
```

The first line of the script invokes the bash shell to run the script. After you type this script using your favorite text editor, make the script executable by using the chmod command:

```
# chmod +x rmv
```

This script moves unwanted files to a directory called .trash in your home directory. When you're sure you want to delete the files, you can then verify the files and empty the trash. Because this script is supposed to act like a regular command, a short, built-in help command is included.

![](bbox=[0.18, 0.92, 0.26, 0.98])

> If you want to try the rmv script, make sure you type it correctly or change the line containing rm -fr $HOME/.trash/* ;; to rm -i $HOME/.trash/* ;; which is much safer than an unconditional delete. If you don't type this line correctly, you might delete your entire home directory!