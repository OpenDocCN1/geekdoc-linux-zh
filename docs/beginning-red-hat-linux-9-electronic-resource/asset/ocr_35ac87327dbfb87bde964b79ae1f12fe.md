# Moving Files and Directories

To move a file or directory, we use the `mv` (move) command. This requires two arguments – the file or directory to be moved, and the destination:

```
$ mv squidgy.txt squeezy.txt
```

This is a classic example of "moving a file". In this example, we're using `mv` not to move the file to a different directory but simply to *change the name* of the file. In Linux, "moving" a file really means "changing its path".

It's also possible to move multiple files at the same time. For example, this command moves the files `squeezy.txt` and `stodgy.txt` from the present working directory to the directory `/etc/textures`:

```
mv squeezy.txt stodgy.txt /etc/textures
```

# Try It Out Creating, Moving, and Removing Files and Directories

Let's step through a simple example in which we create a directory with a file in it, then rename the file. Once we are done experimenting, we will clean everything up by deleting both the file and the directory.

+   1. Change the present working directory to your home directory. For example, if you were logged in with the username `deepakt`, then you would simply type this:
+   
+   ```sh
+   $ cd
+   ```

+   2. Just to check that the above step worked, use `pwd` to check the present working directory:
+   
+   ```sh
+   $ pwd
+   /home/deepakt
+   ```

+   3. Now create a subdirectory called `test`, and make it the working directory:
+   
+   ```sh
+   $ mkdir test
+   $ cd test
+   ```

+   4. Now create a new file called `nomme.txt`:
+   
+   ```sh
+   $ touch nomme.txt
+   ```

+   5. To prove that the `touch` command really did create a new file, you can use the `ls` command to list the contents of the `test` directory: