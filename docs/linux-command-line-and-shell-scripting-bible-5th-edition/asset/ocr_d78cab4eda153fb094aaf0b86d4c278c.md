The `ls` command has lots of parameters that can come in handy as you do file management. If you type `man ls` at the shell prompt, you see several pages of available parameters for you to use to modify the `ls` command output.

Don’t forget that you can also combine many of the parameters. You can often find a parameter combination that not only displays the desired output, but is also easy to remember, such as `ls -aiF`.

# ### Filtering listing output

As you’ve seen in the examples, by default the `ls` command lists all the non-hidden directory files. Sometimes, this can be overkill, especially when you’re just looking for information on a few files.

Fortunately, the `ls` command also provides a way for you to define a filter on the command line. It uses the filter to determine which files or directories it should display in the output.

Before using the filter command, let’s create some files to play with via the `touch` command (covered in the next section). If the file already exists, the command won’t hurt the file:

```
```
$ touch my_script my_scrapt my_file
$ touch fall fell fill full
$ ls
  Desktop   Downloads  fell  full  my_file   my_script   Public   test_file
  Documents   fall     fill  Music my_scrapt Pictures  Templates  Videos
$ 
```
```

The filter works as a simple text-matching string. Include the filter after any command-line parameters you want to use:

```
```
$ ls -l my_script
-rwxr-xr-x   1 christine christine  74 Feb 29 16:12 my_script
$ 
```
```

When you specify the name of a specific file as the filter, the `ls` command only shows that file’s information. Sometimes, you might not know the exact filename you’re looking for. The `ls` command also recognizes standard wildcard characters and uses them to match patterns within the filter:

+   - A question mark (?) represents one character.
+   - An asterisk (*) represents any number of characters.

The question mark can be used to replace exactly one character anywhere in the filter string. For example:

```
```
$ ls -l my_scri?t
-rw-rw-r--   1 christine christine    0 Feb 29 16:12 my_scrapt
-rwxrw-r---   1 christine christine  74 Feb 29 16:12 my_script
$ 
```
```