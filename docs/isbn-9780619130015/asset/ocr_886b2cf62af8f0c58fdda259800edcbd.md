**To place several functions inside a shell script:**

1. Use the vi or Emacs editor to create the .myfuncs file inside your source directory.
2. Enter the code for the following functions:

    ```bash
    sort_name()
    {
        sort +1 -t: corp_phones
    }

    sort_date()
    {
        sort +6 -t: corp_phones
    }

    sort_dept()
    {
        sort +4 -t: corp_phones
    }
    ```

3. Save the file and exit the editor.

Your next task is to load the .myfuncs file into memory so its functions may be executed. To do this, type a period (.) followed by a space, followed by the name of the file containing the functions.

**To load the .myfuncs file:**

1. At the command line, type . myfuncs and press Enter. Nothing appears, but the functions are loaded into memory.
2. Test some functions. Type sort_name and press Enter. You see the phone records sorted by individuals' names.
3. Type sort_dept and press Enter. You see the phone records sorted by department number.

You can load functions automatically by your .bash_profile or .bashrc files when you log on. This way, they are always available to any shell script that needs them.

**To modify your .bashrc file to load the .myfuncs script:**

1. Load your .bashrc file into the vi or Emacs editor.
2. At the end of the file, add the following command:

    ```bash
    . ~/source/.myfuncs
    ```