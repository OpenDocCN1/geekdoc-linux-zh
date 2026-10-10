```
```sh
        "Display memory usage")
               memusage ;;
      *)
          clear
          echo "Sorry, wrong selection";;
      esac
      done
      clear
```

```

The `select` statement must all be on one line in the code file. That’s indicated by the continuation character (\~CA) in the listing. When you run the program, it automatically produces the following menu:

```
```
$ ./menu1
1) Display disk space      3) Display memory usage
2) Display logged on users 4) Exit program
Enter option:
```

```

When you use the `select` command, remember that the result value stored in the variable is the entire text string and not the number associated with the menu item. The text string values are what you need to compare in your `case` statements.

# # Doing Windows

Using text menus is a step in the right direction, but there’s still so much missing in these interactive scripts, especially if you compare them to the graphical Windows world. Fortunately, some resourceful people out in the open source world have helped us out.

The `dialog` package is a nifty little tool originally created by Savo Lam and currently maintained by Thomas E. Dickey. This package re-creates standard Windows dialogs in a text environment using ANSI escape control codes. You can easily incorporate these dialogs in your shell scripts to interact with your script users. This section describes the `dialog` package and demonstrates how to use it in shell scripts.

> **NOTE**
> The `dialog` package isn’t installed in all Linux distributions by default. If it’s not installed by default, because of its popularity it’s almost always included in the software repository. Check your specific Linux distribution documentation for how to load the `dialog` package. For the Ubuntu Linux distribution, the following command installs it:
> ```sh
> sudo apt-get install dialog
> ```
> To install the `dialog` package in Red Hat-based systems, such as Rocky Linux, use the `dnf` command:
> ```sh
> sudo dnf install dialog
> ```
> The package installer installs the `dialog` package plus any libraries required for it to work on your system.