```
xmmission> alias
cd  cd 1*;echo $cwd
clr  clear
cls  clear
copy cp -i
del rm -i
delete rm -i
dir ls -olg
home cd ~
ls ls -F
md mkdir
move mv -i
pwd echo $cwd
type more
xmmission>
```

Code Listing 8.23 Type alias at the shell prompt to see a list of aliases you've set.

+   5. Save the file and exit from the editor.
+   See Chapter 4 for details about saving and exiting in vi and pico.
+   6. su - yourid
+   Start a new log-in shell to test out the alias.
+   7. alias
+   Type alias at the shell prompt for a listing of all the aliases you have defined (Code Listing 8.23)

# Tips

+   - You can put aliases in other files, but it's customary to put them in the .bashrc file (or other appropriate rc file, such as .cshrc), so they'll be set automatically when you log in, rather than having to be manually set.
+   - You can also issue alias commands from the shell prompt to set aliases for the current session.
+   - Be sure to make a backup copy of any configuration files you plan to change before you change them. That way, if you mess up, you still have the original file to work with.