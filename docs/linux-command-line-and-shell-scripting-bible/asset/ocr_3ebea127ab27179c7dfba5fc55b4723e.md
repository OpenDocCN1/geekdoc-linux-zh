```
}
function memusage (
  clear
  cat /proc/meminfo
)
```

```
PS3="Enter option: "
select option in "Display disk space" "Display logged on users"
"Display memory usage" "Exit program"
do
  case $option in
    "Exit program")
      break ;;
    "Display disk space"
      diskspace;
        Display logged on users"
      whoseon ::
    "Display memory usage"
      memusage ::
  *)
    clear
  esac echo "Sorry, wrong selection";
done
clear
$
```

When you run the program, it automatically produces the following menu:

+   $ ./smenuel
1) Display disk space 3) Display memory usage
2) Display logged on users 4) Exit program
ter option:

When you use the select command, remember that the result value stored in the variable is the entire text string and not the number associated with the menu item. The text string values are what you need to compare in your case statements.

# Adding Color

In the old days of Unix, script programmers were limited to monochrome terminals, so interactive shell scripts didn't have to worry about using colors. These days, with all of the fancy terminal emulation packages around, adding colors and special effects to your interactive scripts has almost become a necessity. This section discusses and demonstrates how to add special text features to your script output.