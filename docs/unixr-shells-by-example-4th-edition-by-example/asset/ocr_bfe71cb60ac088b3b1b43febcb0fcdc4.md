# EXAMPLE 9.23 (CONTINUED)

```
3  % pushd perlclass
   ~/perlclass  ~  /home

4  % dirs -v
   0       ~/perlclass
   1       ~
   2       /home

5  % popd
   ~       /home
   % pwd
   /home/ellie

6  % popd
   /home
   % pwd
   /home

7  % popd
   popd: Directory stack empty.
```

# EXPLANATION

+   1. First the pwd command displays the present working directory, /home/ellie. Next the pushd command with .. as its argument pushes the parent directory (..) onto the directory stack. The output of pushd indicates that /home is at the top of the directory stack and the user's home directory (~), /home/ellie, is at the bottom of the stack. pushd also changes the directory to the one that was pushed onto the stack; that is, .., which translates to /home. The new directory is displayed with the second pwd command.
+   
+   2. pushd, without arguments, exchanges the two top directory entries on the stack and changes to the swapped directory; in this example, the directory is switched back to the user's home directory, /home/ellie.
+   
+   3. The pushd command will push its argument, ~/perlclass, onto the stack, and change to that directory.
+   
+   4. The built-in dirs command displays the numbered directory stack, with 0 being the top level.
+   
+   5. The popd command removes a directory from the top of the stack, and changes to that directory.
+   
+   6. The popd command removes another directory from the top of the stack, and changes to that directory.
+   
+   7. The popd command cannot remove any more directory entries because the stack is empty, and issues an error message saying so.