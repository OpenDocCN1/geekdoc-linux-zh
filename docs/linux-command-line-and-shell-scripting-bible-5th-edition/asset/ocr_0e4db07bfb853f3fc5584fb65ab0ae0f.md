# Chapter 3: Basic Bash Shell Commands

The new file test_two shows a different modification time than the test_one file. If the destination file already exists, the cp command may not prompt you to this fact. It is best to add the -i option to force the shell to ask whether you want to overwrite a file:

```
$ ls -l test_one test_two
-rw-rw-r--. 1 christine christine 0 Feb 29 17:26 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:46 test_two
$
$ cp -i test_one test_two
cp: overwrite ‘test_two’? n
$
```

If you don't answer y, the file copy does not proceed. You can also copy a file into a preexisting directory:

```
$ cp -i test_one /home/christine/Documents/
$
$ ls -l /home/christine/Documents/
total 0
-rw-rw-r--. 1 christine christine 0 Feb 29 17:48 test_one
$
```

The new file is now under the Documents directory, using the same filename as the original.

> **NOTE**
> The preceding example uses a trailing forward slash (/) on the destination directory name. Using the slash indicates that Documents is a directory and not a file. This is helpful for clarity purposes and is important when copying single files. If the forward slash is not used and the subdirectory /home/christine/Documents does not exist, a file named Documents is created within the current directory and no error message is displayed. That is problematic, so use a trailing forward slash on your destination directory names.

This last example used an absolute directory reference, but you can just as easily use a relative directory reference:

```
$ cp -i test_two Documents/
$ ls -l Documents/
total 0
-rw-rw-r--. 1 christine christine 0 Feb 29 17:48 test_one
-rw-rw-r--. 1 christine christine 0 Feb 29 17:51 test_two
$
```

Earlier in this chapter, you read about the special symbols that can be used in relative directory references. One of them, the single dot (.), is great to use with the cp command. Remember that the single dot represents your current working directory. If you need to copy a file with a long source object name to your current working directory, the single dot can simplify the task:

```
$ cp /etc/NetworkManager/NetworkManager.conf .
$ ls ./.conf
NetworkManager.conf
$
```