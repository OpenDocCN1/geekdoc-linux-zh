
## Linux Hack
Ajay Kumar Tiwari

### Sort a text file in ascending order
```
$ sort names.txt
```
Alex Jason:200:Sales
Emma Thomas:100:Marketing
Madison Randy:300:Product Development
Nisha Singh:500:Sales
Sanjay Gupta:400:Support

### Sort a text file in descending order
```
$ sort -r names.txt
```
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
Madison Randy:300:Product Development
Emma Thomas:100:Marketing
Alex Jason:200:Sales

### Sort a colon delimited text file on 2nd field (employee_id)
```
$ sort -t: -k 2 names.txt
```
Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales

### Sort a tab delimited text file on 3rd field (department_name) and suppress duplicates
```
$ sort -t: -u -k 3 names.txt
```
Emma Thomas:100:Marketing
Madison Randy:300:Product Development
Alex Jason:200:Sales
Sanjay Gupta:400:Support

### Sort the passwd file by the 3rd field (numeric userid)
```
$ sort -t : -k 3n /etc/passwd | more
```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin

### Sort /etc/hosts file by ip-address
```
$ sort -t . -k 1,1n -k 2,2n -k 3,3n -k 4,4n /etc/hosts
```
127.0.0.1 localhost.localdomain localhost
192.168.100.101 dev-db.thegeekstuff.com dev-db
192.168.100.102 prod-db.thegeekstuff.com prod-db
192.168.101.20 dev-web.thegeekstuff.com dev-web
192.168.101.21 prod-web.thegeekstuff.com prod-web

### Combine sort with other commands

- ps -ef | sort : Sort the output of process list
- ls -al | sort +4n : List the files in the ascending order of the file-size. i.e sorted by 5th filed and displaying smallest files first.
- ls -al | sort +4nr : List the files in the descending order of the file-size. i.e sorted by 5th filed and displaying largest files first.

## Hack 24. Uniq Command

Uniq command is mostly used in combination with sort command, as uniq removes duplicates only from a sorted file. i.e In order for uniq to work, all the duplicate entries should be in the adjacent lines. Following are some common examples.

1. When you have an employee file with duplicate entries, you can do the following to remove duplicates.
```
$ sort namesd.txt | uniq
```
```
$ sort -u namesd.txt
```
2. If you want to know how many lines are duplicates, do the following. The first field in the following examples indicates how many duplicates where found for that particular line. So, in this example the lines beginning with Alex and Emma were found twice in the namesd.txt file.
```
$ sort namesd.txt | uniq -c
```
2
2
1
1
1
Alex Jason:200:Sales
Emma Thomas:100:Marketing
Madison Randy:300:Product Development
Nisha Singh:500:Sales
Sanjay Gupta:400:Support

3. The following displays only the entries that are duplicates.
```
$ sort namesd.txt | uniq -cd
```
2 Alex Jason:200:Sales
2 Emma Thomas:100:Marketing

## Hack 25. Cut Command

Cut command can be used to display only specific columns from a text file or other command outputs.

Following are some of the examples.

### Display the 1st field (employee name) from a colon delimited file
```
$ cut -d: -f 1 names.txt
```
Emma Thomas
Alex Jason
Madison Randy
Sanjay Gupta
Nisha Singh

### Display 1st and 3rd field from a colon delimited file
```
$ cut -d: -f 1,3 names.txt
```
Emma Thomas:Marketing
Alex Jason:Sales
Madison Randy:Product Development
Sanjay Gupta:Support
Nisha Singh:Sales

### Display only the first 8 characters of every line in a file
```
$ cut -c 1-8 names.txt
```
Emma Tho
Alex Jas
Madison
Sanjay G
Nisha Si

### Misc Cut command examples

- cut -d: -f1 /etc/passwd Displays the unix login names for all the users in the system.
- free | tr -s ' ' | sed '/^Mem/!d' | cut -d" " -f2 Displays the total memory available on the system.

## Hack 26. Stat Command

Stat command can be used either to check the status/properties of a single file or the filesystem.

Display statistics of a file or directory.
```
$ stat /etc/my.cnf
```
```
File:
Size:
Device:
Access:
(0/
Access:
Modify:
Change:
`/etc/my.cnf’
346 Blocks: 16 IO Block: 4096regular file
801h/2049dInode: 279856Links: 1
(0644/-rw-r--r--) Uid: (0/root)Gid:
  root)
2009-01-01 02:58:30.000000000 -0800
2006-06-01 20:42:27.000000000 -0700
2007-02-02 14:17:27.000000000 -0800
```
```
$ stat /home/ramesh
```
File: `/home/ramesh’
Size: 4096Blocks: 8IO Block:
4096directory
Device: 803h/2051dInode: 5521409Links: 7
Access: (0755/drw xr-xr-x) Uid: ( 401/ramesh)Gid: (
401/ramesh)
Access: 2009-01-01 12:17:42.000000000 -0800
Modify: 2009-01-01 12:07:33.000000000 -0800
Change: 2009-01-09 12:07:33.000000000 -0800

### Display the status of the filesystem using option -f
```
$ stat -f /
```
File:
ID:
Blocks:
1876998
Inodes:
"/"
0Namelen: 255Type: ext2/ext3
Total: 2579457Free: 2008027Available:
  Size: 4096
Total: 1310720Free: 1215892

## Hack 27. Diff Command

diff command compares two different files and reports the difference. The output is very cryptic and not straight forward to read.

Syntax: diff [options] file1 file2

What was modified in my new file when compare to my old file?

The option -w in the diff command will ignore the white space while performing the comparison.

In the following diff output:

- The lines above –, indicates the changes happened in first file in the diff command (i.e name_list.txt).
- The lines below –, indicates the changes happened to the second file in the diff command (i.e name_list_new.txt). The lines that belong to the first file starts with < and the lines of second file starts with >.

```
# diff -w name_list.txt name_list_new.txt
```
2c2,3

< John Doe

–

> John M Doe

> Jason Bourne

## Hack 28. Display total connect time of users

Ac command will display the statistics about the user’s connect time.

### Connect time for the current logged in user

With the option -d, it will break down the output for the individual days. In this example, I’ve been logged in to the system for more than 6 hours today.

On Dec 1st, I was logged in for about 1 hour.
```
$ ac -d
```
```
Dec 1
Dec 2
Dec 3
Dec 4
Today
total
total
total
total
total
1.08
0.99
3.39
4.50
6.10
```

### Connect time for all the users

To display connect time for all the users use -p as shown below. Please note that this indicates the cumulative connect time for the individual users.
```
$ ac -p
john
madison
sanjay
nisha
  3.64
0.06
  88.17
 105.92
45
ramesh
total 309.21
111.42
```

### Connect time for a specific user

To get a connect time report for a specific user, execute the following:
```
$ ac -d sanjay
```
Jul 2

Aug 25

Sep 3

Sep 4

Dec 24

Dec 29

Today

total

total

total

total

total

total

total

12.85

5.05

1.03

5.37

8.15

1.42

2.95

## Chapter 5: PS1, PS2, PS3, PS4 and PROMPT_COMMAND

## Hack 29. PS1 - Default Interaction Prompt

The default interactive prompt on your Linux can be modified as shown below to something useful and informative. In the following example, the default PS1 was “\s-\v\$”, which displays the shell name and the version number. Let us change this default behavior to display the username, hostname and current working directory name as shown below.
```
-bash-3.2$
export PS1="\u@\h \w> "
ramesh@dev-db ~> cd /etc/mail
ramesh@dev-db /etc/mail>
```
[Note: Prompt changed to “username@hostname current-dir>” format]

Following PS1 codes are used in this example:

- \u – Username
- \h – Hostname
- \w - Full pathname of current directory. Please note that when you are in the home directory, this will display only ~ as shown above

Note that there is a space at the end in the value of PS1. Personally, I prefer a space at the end of the prompt for better readability.

Make this setting permanent by adding export PS1="\u@\h \w> " to either .bash_profile (or) .bashrc as shown below.
