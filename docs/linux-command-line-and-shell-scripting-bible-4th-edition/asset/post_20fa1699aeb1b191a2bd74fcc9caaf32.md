
```bash
$ ls -l my_s*t
-rw-rw-r--. 1 christine christine   0 Feb 29 16:12 my_scrap
-rwxrw-r--. 1 christine christine  74 Feb 29 16:12 my_script
$
```

Using the asterisk finds three different files, starting with the name my. As with the question mark, you can place the asterisks anywhere in the filter:

```bash
$ ls -l my_s*t
-rw-rw-r--. 1 christine christine   0 Feb 29 16:12 my_scrap
-rwxrw-r--. 1 christine christine  74 Feb 29 16:12 my_script
$
```

Using the asterisk and question mark in the filter is called file globbing. File globbing is the process of pattern matching using wildcards. The wildcards are officially called metacharacter wildcards. You can use more metacharacter wildcards for file globbing than just the asterisk and question mark. You can also use brackets:

```bash
$ touch my_scrsypt
$ ls -l my_scr[ay]pt
-rw-rw-r--. 1 christine christine   0 Feb 29 16:12 my_scrap
-rw-rw-r--. 1 christine christine   0 Feb 29 16:18 my_scrsypt
$
```

In this example, we used the brackets along with two potential choices for a single character in that position, a or y. The brackets represent a single character position and give you multiple options for file globbing. You can list choices of characters, as shown in the preceding example, and you can specify a range of characters, such as an alphabetic range [a-i] :

```bash
$ ls f*1l
fall fell fill full
$ ls f[a-i]1l
fall fell fill
$
```

Also, you can specify what should not be included in the pattern match by using the exclamation point (!):

```bash
$ ls -1 f[!a]1l
-rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fell
-rw-rw-r--. 1 christine christine   0 Feb 29 16:12 fill
-rw-rw-r--. 1 christine christine   0 Feb 29 16:12 full
$
```

File globbing is a powerful feature when searching for files. It can also be used with other shell commands besides `ls`. You’ll find out more about this later in the chapter.

## Handling Files

The shell provides many file manipulation commands on the Linux filesystem. This section walks you through the basic shell commands you need to handle files.

### Creating files

Every once in a while you run into a situation where you need to create an empty file. For example, sometimes applications expect a log file to be present before they can write to it. In these situations, you can use the `touch` command to easily create an empty file:

```bash
$ touch test_one
$ ls -l test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:24 test_one
$
```

The `touch` command creates the new file you specify and assigns your username as the file owner. Notice in the preceding example that the file size is zero because the `touch` command just created an empty file. The `touch` command can also be used to change the modification time. This is done without changing the file contents:

```bash
$ ls -l test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:24 test_one
$ touch test_one
$ ls -l test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:26 test_one
$
```

The modification time of test_one is now updated to 17:26 from the original time, 17:24.

Creating empty files and altering file time stamps is not something you will do on a Linux system daily. However, copying files is an action you will do often while using the shell.

### Copying files

Copying files and directories from one location in the filesystem to another is a common practice for system administrators. The `cp` command provides this feature.

In its most basic form, the `cp` command uses two parameters — the source object and the destination object: `cp source destination`.

When both the source and destination parameters are filenames, the `cp` command copies the source file to a new destination file. The new file acts like a brand-new file, with an updated modification time:

```bash
$ cp test_one test_two
$ ls -l test_one test_two
-rw-rw-r--. 1 christine christine 0 Feb 29 17:26 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:46 test_two
$
```

The new file test_two shows a different modification time than the test_one file. If the destination file already exists, the `cp` command may not prompt you to this fact. It is best to add the `-i` option to force the shell to ask whether you want to overwrite a file:

```bash
$ ls -l test_one test_two
-rw-rw-r--. 1 christine christine 0 Feb 29 17:26 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:46 test_two
$
$ cp -i test_one test_two
cp: overwrite 'test_two'? n
$
```

If you don't answer y, the file copy does not proceed. You can also copy a file into a preexisting directory:

```bash
$ cp -i test_one /home/christine/Documents/
$
$ ls -l /home/christine/Documents/
total 0
-rw-rw-r--. 1 christine christine 0 Feb 29 17:48 test_one
$
```

The new file is now under the `Documents` directory, using the same filename as the original.

**NOTE**

The preceding example uses a trailing forward slash (/) on the destination directory name. Using the slash indicates `Documents` is a directory and not a file. This is helpful for clarity purposes and is important when copying single files. If the forward slash is not used and the subdirectory `/home/christine/Documents` does not exist, a file named `Documents` is created within the current directory and no error message is displayed. That is problematic, so use a trailing forward slash on your destination directory names.

This last example used an absolute directory reference, but you can just as easily use a relative directory reference:

```bash
$ cp -i test_two Documents/
$ ls -l Documents/
total 0
-rw-rw-r--. 1 christine christine 0 Feb 29 17:48 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:51 test_two
$
```

Earlier in this chapter, you read about the special symbols that can be used in relative directory references. One of them, the single dot (.), is great to use with the `cp` command. Remember that the single dot represents your current working directory. If you need to copy a file with a long source object name to your current working directory, the single dot can simplify the task:

```bash
$ cp /etc/NetworkManager/NetworkManager.conf .
$ ls *.conf
NetworkManager.conf
$
```

It’s hard to see that single dot! If you look closely, you’ll see it at the end of the first example code line. Using the single dot symbol is much easier than typing a full destination object name when you have long source object names.

The `-R` parameter is a powerful `cp` command option. It allows you to recursively copy the contents of an entire directory in one command:

```bash
$ ls -l Documents/
total 0
-rw-rw-r--. 1 christine christine 0 Feb 29 17:48 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:51 test_two
$
$ cp -R Documents/ NewDocuments/
$ ls -l NewDocuments/
total 0
-rw-rw-r--. 1 christine christine 0 Feb 29 17:55 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:55 test_two
$
```

The directory `NewDocuments` did not exist prior to the `cp -R` command. It was created with the `cp -R` command, and the entire `Documents` directory's contents were copied into it. Notice that all the files in the new `NewDocuments` directory have new dates associated with them. Now `NewDocuments` is a complete copy of the `Documents` directory.

> **TIP**
> 
> There are many more `cp` command parameters than those described here. Remember that you can see all the different parameters available for the `cp` command by typing `man cp`.

You can also use wildcard metacharacters in your `cp` commands:

```bash
$ ls
Desktop      public       fall       full       my_scrap     NetworkManager.conf
Documents    Documents   fell       Music      my_script    NewDocuments
Templates    test_one    download   fill_my_file my_script  Pictures
Videos       test_file   
$
$ cp my* NewDocuments/
$ ls NewDocuments/
my_file   my_scrap   my_script   my_scrpyt   test_one   test_two
$
```

This command copied any files that started with `my` to `NewDocuments`. Now the directory contains six files instead of just two.

When copying files, another shell feature can help you besides the single dot and wildcard metacharacters. It is called command-line completion.

### Using command-line completion

When working at the command line, you can easily mistype a command, directory name, or filename. In fact, the longer a directory reference or filename, the greater the chance you will mistype it.

This is where command-line completion (also called tab completion) can be a lifesaver. Tab completion allows you to start typing a filename or directory name, and then press the tab key to have the shell complete it for you:

```bash
$ touch really_ridiculously_long_file_name
$
$ cp really_ridiculously_long_file_name NewDocuments/
$ ls NewDocuments/
my_file   my_script   really_ridiculously_long_file_name
test_two
my_scrap   my_scrpyt   test_one
$
```

After creating a file with a very long name in the preceding example, we typed the command `cp really` and pressed the Tab key, and the shell autocompleted the rest of the filename for us! Of course, the destination directory had to be typed, but still tab completion saved the command from several potential typographical errors.

The trick to using command-line completion is to give the shell enough filename characters so it can distinguish the desired file from other files. For example, if another filename started with `really`, pressing the Tab key would not autocomplete the filename. Instead, you would hear a beep. If this happens, you can press the Tab key again, and the shell shows you all the filenames starting with `really`.
