
Cipher: aes128-cbc
MAC: hmac-sha1
Compression: zlib

## Linux Hack

Algorithms server to client:

Cipher: aes128-cbc

MAC: hmac-sha1

Compression: zlib

localhost$

Ajay Kumar Tiwari

## Additional SSH Info

On a side note, to setup SSH key based authentication, refer openSSH and SSH2 tutorials.

## Linux Hack

Ajay Kumar Tiwari

## Chapter 4: Essential Linux Commands

## Hack 17. Grep Command

grep command is used to search files for a specific text. This is incredibly powerful command with lot of options.

Syntax: grep [options] pattern [files]

### How can I find all lines matching a specific keyword on a file?

In this example, grep looks for the text John inside /etc/passwd file and displays all the matching lines.

```
# grep John /etc/passwd
```

jsmith:x:1082:1082:John Smith:/home/jsmith:/bin/bash

jdoe:x:1083:1083:John Doe:/home/jdoe:/bin/bash

Option -v, will display all the lines except the match. In the example below, it displays all the records from /etc/passwd that doesn’t match John.

Note: There are several lines in the /etc/passwd that doesn’t contain the word John. Only the first line of the output is shown below.

```
# grep -v John /etc/passwd
```

jbourne:x:1084:1084:Jason Bourne:/home/jbourne:/bin/bash

### How many lines matched the text pattern in a particular file?

In the example below, it displays the total number of lines that contains the text John in /etc/passwd file.

```
# grep -c John /etc/passwd
```

2

You can also get the total number of lines that did not match the specific pattern by passing option -cv.

```
# grep -cv John /etc/passwd
```

39

### How to search a text by ignoring the case?

Pass the option -i (ignore case), which will ignore the case while searching.

```
# grep -i john /etc/passwd
```

jsmith:x:1082:1082:John Smith:/home/jsmith:/bin/bash

jdoe:x:1083:1083:John Doe:/home/jdoe:/bin/bash

### How do I search all subdirectories for a text matching a specific pattern?

Use option -r (recursive) for this purpose. In the example below, it will search for the text “John” by ignoring the case inside all the subdirectories under /home/users.

This will display the output in the format of “filename: line that matching the pattern”. You can also pass the option -l, which will display only the name of the file that matches the pattern.

```
# grep -ri john /home/users
```

/home/users/subdir1/letter.txt:John, Thanks for your contribution.

/home/users/name_list.txt:John Smith

/home/users/name_list.txt:John Doe

```
# grep -ril john /root
```

/home/users/subdir1/letter.txt

/home/users/name_list.txt

Ajay Kumar Tiwari

## Hack 18. Find Command

find is frequently used command to find files in the UNIX filesystem based on numerous conditions. Let us review some practice examples of find command.

Syntax: find [pathnames] [conditions]

### How to find files containing a specific word in its name?

The following command looks for all the files under /etc directory with mail in the filename.

```
# find /etc -name "*mail*"
```

### How to find all the files greater than certain size?

The following command will list all the files in the system greater than 100MB.

```
# find / -type f -size +100M
```

### How to find files that are not modified in the last x number of days?

The following command will list all the files that were modified more than 60 days ago under the current directory.

```
# find . -mtime +60
```

Ajay Kumar Tiwari

### How to find files that are modified in the last x number of days?

The following command will list all the files that were modified in the last two days under the current directory.

```
# find . -mtime -2
```

### How to delete all the archive files with extension *.tar.gz and greater than 100MB?

Please be careful while executing the following command as you don’t want to delete the files by mistake. The best practice is to execute the same command with ls -l to make sure you know which files will get deleted when you execute the command with rm.

```
# find / -type f -name *.tar.gz -size +100M -exec ls -l {} \;
```

```
# find / -type f -name *.tar.gz -size +100M -exec rm -f {} \;
```

### How to archive all the files that are not modified in the last x number of days?

The following command finds all the files not modified in the last 60 days under /home/jsmith directory and creates an archive files under /tmp in the format of ddmmyyyy_archive.tar.

```
# find /home/jsmith -type f -mtime +60 | xargs tar -cvf /tmp/`date '+%d%m%Y'_archive.tar`
```

On a side note, you can perform lot of file related activities (including finding files) using midnight commander GUI, a powerful text based file manager for Unix.

## Linux Hack

Ajay Kumar Tiwari

## Hack 19. Suppress Standard Output and Error Message

Sometime while debugging a shell script, you may not want to see either the standard output or standard error message. Use /dev/null as shown below for suppressing the output.

### Suppress standard output using > /dev/null

This will be very helpful when you are debugging shell scripts, where you don’t want to display the echo statement and interested in only looking at the error messages.

```
# cat file.txt > /dev/null
```

```
# ./shell-script.sh > /dev/null
```

### Suppress standard error using 2> /dev/null

This is also helpful when you are interested in viewing only the standard output and don’t want to view the error messages.

```
# cat invalid-file-name.txt 2> /dev/null
```

```
# ./shell-script.sh 2> /dev/null
```

## Hack 20. Join Command

Join command combines lines from two files based on a common field.

In the example below, we have two files – employee.txt and salary.txt. Both have employee-id as common field. So, we can use join command to combine the data from these two files using employee-id as shown below.

## Linux Hack

Ajay Kumar Tiwari

```
$ cat employee.txt
100
200
300
400
Jason Smith
John Doe
Sanjay Gupta
Ashok Sharma
```

```
$ cat bonus.txt
100
200
300
400
$5,000
$500
$3,000
$1,250
```

```
$ join employee.txt bonus.txt
100
200
300
400
Jason Smith $5,000
John Doe $500
Sanjay Gupta $3,000
Ashok Sharma $1,250
```

## Hack 21. Change the Case

### Convert a file to all upper-case

```
$ cat employee.txt
100
200
300
400
Jason Smith
John Doe
Sanjay Gupta
Ashok Sharma
$ tr a-z A-Z < employee.txt
100 JASON SMITH
200 JOHN DOE
300 SANJAY GUPTA
400 ASHOK SHARMA
```

Ajay Kumar Tiwari

### Convert a file to all lower-case

```
$ cat department.txt
100
200
300
400
FINANCE
MARKETING
PRODUCT DEVELOPMENT
SALES
```

```
$ tr A-Z a-z < department.txt
```

```
100
200
300
400
finance
marketing
product development
sales
```

## Hack 22. Xargs Command

xargs is a very powerful command that takes output of a command and pass it as argument of another command. Following are some practical examples on how to use xargs effectively.

- 1. When you are trying to delete too many files using rm, you may get error message: /bin/rm Argument list too long – Linux. Use xargs to avoid this problem.

```
find ~ -name '*.log' -print0 | xargs -0 rm -f
```

- 2. Get a list of all the *.conf file under /etc/. There are different ways to get the same result. Following example is only to demonstrate the use of xargs. The output of the find command in this example is passed to the ls –l one by one using xargs.

## Linux Hack

Ajay Kumar Tiwari

```
# find /etc -name "*.conf" | xargs ls -l
```

- 3. If you have a file with list of URLs that you would like to download, you can use xargs as shown below.

```
# cat url-list.txt | xargs wget -c
```

- 4. Find out all the jpg images and archive it.

```
# find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz
```

- 5. Copy all the images to an external hard-drive.

```
# ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory
```

## Hack 23. Sort Command

Sort command sorts the lines of a text file. Following are several practical examples on how to use the sort command based on the following sample text file that has employee information in the format:

employee_name:employee_id:department_name.

```
$ cat names.txt
```

Emma Thomas:100:Marketing

Alex Jason:200:Sales

Madison Randy:300:Product Development

Sanjay Gupta:400:Support

Nisha Singh:500:Sales
