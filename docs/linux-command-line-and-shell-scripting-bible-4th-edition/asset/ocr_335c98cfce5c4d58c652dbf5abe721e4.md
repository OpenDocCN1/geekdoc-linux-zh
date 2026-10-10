```
newrecord ;;
2) listrecords ;;
3) break ;;
*) dialog --msgbox "Invalid selection" 10 30
esac
done
rm -f $temp 2> /dev/null
```

This script creates a simple graphical front end that allows you to quickly enter employee data to create an SQL file that you can easily import into a database.

# ## Summary

Interactive shell scripts have a reputation for being dull and boring. You can change that by using a few techniques and tools available on most Linux systems. First, you can create menu systems for your interactive scripts by using the case command and shell script functions.

The menu command allows you to paint a menu, using the standard echo command, and read a response from the user, using the read command. The case command then selects the appropriate shell script function based on the value entered.

The dialog program provides several prebuilt text widgets for creating Windows-like objects on a text-based terminal emulator. You can create dialogs for displaying text, entering text, and choosing files and dates by using the dialog program. Doing so brings even more life to your shell script.

If you're running your shell scripts in a graphical X Windows environment, you can utilize even more tools in your interactive scripts. For the KDE desktop, there's the kdialog program. This program provides simple commands to create window widgets for all the basic window functions. For the GNOME desktop, there are the gdialog and zenity programs. Each of these programs provides window widgets that blend into the GNOME desktop just like a real