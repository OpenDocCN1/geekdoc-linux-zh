`config_file` . Each record is read in from the configuration file. As long as the `read` command finds a new configuration file record to read, it returns an exit value of 0 for success in the ? variable ([Chapter 11](Chapter 11), “Basic Script Building”). You can use this as a test in a `while` loop in order to read all the records from the configuration file:

```
```
while [ $? -eq 0 ]
do
[...]
read file_name
done
```
```

When the `read` command hits the end of the configuration file, it returns a non-zero status in the ? variable. At that point, the `while` loop is exited.

In the `while` loop, two things need to happen. First, we must add the directory name to our archive list. Even more important is to check if that directory even exists! It would be very easy to remove a directory from the filesystem and forget to update the archive configuration file. We can check a directory’s existence using a simple `if` statement (see [Chapter 12](Chapter 12), “Using Structured Commands”). If the directory does exist, it is added to the list of directories to archive, `file_list` . Otherwise, a warning message is issued. Here is what this `if` statement looks like:

```
```
if [ -f $file_name -o -d $file_name ]
then
    file_list="$file_list $file_name"
else
    echo
    echo "$file_name, does not exist."
    echo "Obviously, I will not include it in this archive."
    echo "It is listed on line $file_no of the config file."
    echo "Continuing to build archive list..."
fi
# 
file_no=$[$file_no + 1]
```
```

Because a record in our archive configuration file can be a filename or a directory, the `if` statement tests for the existence of both, using the `-f` and the `-d` options. The `or` option, `-o`, allows for either the file’s or