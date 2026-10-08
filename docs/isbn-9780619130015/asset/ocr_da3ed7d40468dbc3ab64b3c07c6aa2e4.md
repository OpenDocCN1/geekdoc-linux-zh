**To display your current path:**
After the $ command prompt, type `pwd` and press **Enter**. The system displays the path of your current working directory.

# ### Navigating the File System

To navigate the UNIX directory structure, use the `cd` (change directory) command.

Its syntax is:

| Syntax | `cd directory` |
| Dissection | ■ `directory` is the name of the directory to which you want to change. The directory name is expressed as a path to the destination, with slashes (/) separating subdirectory names. |

When you log on, you begin in your home directory, which is under the /home directory. When you change directories and then want to return to your home directory, type `cd` and press **Enter**. (Some shells also use the tilde character (~) to denote the user’s home directory.)

You want to go to the mail subdirectory to see if Dominion employees sent you e-mail.

**To change directories:**

1.  After the $ command prompt, type `cd /etc/mail` and press **Enter**. This moves you to the /var/spool/mail subdirectory.
2.  Type `cd` and press **Enter**. The change directory command (`cd`) without arguments returns you to your home directory.

UNIX refers to a path as either an **absolute path** or a *relative path*. An **absolute path** begins at the root level and lists all subdirectories to the destination file. For example, assume that Becky has a directory named lists, located under her home directory. In the lists directory she has a file called todo. The absolute path to the todo file is /home/becky/lists/todo. The path lists each directory that lies in the path to the todo file.

**tip**
Any time the / symbol is the first character in a path, it stands for the root directory. All other / symbols in a path serve to separate the other names.

A *relative path* takes a shorter journey. You can enter the relative path to begin at your current working directory and proceed from there. In Figure 2-1, jean, tricia,