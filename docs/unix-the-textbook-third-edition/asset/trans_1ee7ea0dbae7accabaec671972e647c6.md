

to the table and the output of the following cut and paste commands. You can display a table of first and last names by using the -f option. Note that -f1,2 specifies the first and the second fields of the student_addresses file.

```
% cut -f1,2 student_addresses
John Doe
Pam Meyer
Jim Davis
Jason Kim
Amy Nash
%
```

We generate a table of names (first and last) and work phone numbers by slicing the first, second, and fifth fields of the table in the student_addresses file.

```
$ cut -f1,2,5 student_addresses
John Doe 312.999.1111
Pam Meyer 666.555.1212
Jim Davis 713.413.0000
Jason Kim 434.555.2211
Amy Nash 888.827.3333
%
```

To generate a table of names and e-mail addresses, we use the following command. Here, -f1-3 specifies fields 1–3 of the student_addresses file.

```
% cut -f1-3 student_addresses
John Doe jdoe@xyz.com
Pam Meyer meyer@uop.pk
Jim Davis jamesd@aol.org
Jason Kim j_kim@up.org
Amy Nash nash@state.gov
%
```

We recommend that you run this command on your machine to determine whether the desired output is produced. If the desired output is not produced, you have not used the <Tab> character as the field separator for some or all of the records. In such a case, correct the table and try the command again.

login IDs and home directories. The first two lines of the output are for comments, as they start with #.

```
$ cut -d: -f5,1,6 /etc/passwd
# $FreeBSD$
#
root:Charlie &: /root
toor:Bourne-again Superuser:/root
daemon:Owner of many system processes:/root
...
sshd:Secure Shell Daemon:/var/empty
smmsp:Sendmail Submission User:/var/spool/clientmqueue
...
sarwar:Syd Mansoor Sarwar:/home/sarwar
...
$
```

Note that the -d option is used to specify : as the field separator, and it is also displayed as the field separator in the output of the command. For blank delimited files, use one or more space characters (blanks) after -d\, as shown in the following example. The cat sample command is used to display the blank delimited file, called sample, and the cut -d\ -f1,6 sample command is used to display fields 1 and 6 of this file.

```
$ cat sample
1 John CS Senior john@net2net.com 3.45
2 Jane CS Junior jane@net2net.com 3.76
3 Sara CS Senior sara@net3net.vom 3.33
$ cut -d\ -f1,6 sample
1 3.45
2 3.76
3 3.33
$
```

The paste command complements the cut command; it concatenates files horizontally (the cat command concatenates files vertically). Hence, this command can be used to paste tables in columns. The following is a brief description of the command.

# SYNTAX

```
paste [options] file-list
```

+   **Purpose:** Horizontally concatenate files in file-list; use standard input if - (i.e., a hyphen) is used as a file
+   **Output:** Files in file-list pasted (horizontally concatenated)
+   **Commonly used options/features:**
+   - **-d list** Use list characters as line separators; <Tab> is the default character

Consider the file student_records, which contains student names (first and last), major, and current GPA.

```
% cat student_records
John Doe ECE 3.54
Pam Meyer CS 3.61
Jim Davis CS 2.71
Jason Kim ECE 3.97
Amy Nash ECE 2.38
%
```

We can combine the two tables, student_records and student_addresses_shortened, horizontally and generate another by using the paste command in the following session. In order to keep the resultant table small, we have used a shortened version of the original student_addresses file called student_addresses_shortened, which contains the first name, last name, and work phone number only, as shown below. We generated this table by using the cut -f1,2,5 student_addresses > student_addresses_shortened command. Note that the output of the paste command is displayed on the display screen and is not stored in a file. The resultant table has seven fields.

```
% cat student_addresses_shortened
John Doe 312.999.1111
Pam Meyer 666.555.1212
Jim Davis 713.413.0000
Jason Kim 434.555.2211
Amy Nash 888.827.3333
% paste student_records student_addresses_shortened
John Doe ECE 3.54 John Doe 312.999.1111
Pam Meyer CS 3.61 Pam Meyer 666.555.1212
Jim Davis CS 2.71 Jim Davis 713.413.0000
Jason Kim ECE 3.97 Jason Kim 434.555.2211
Amy Nash ECE 2.38 Amy Nash 888.827.3333
%
```

Suppose that you want to use the student_addresses_shortened and student_records tables to generate and display a table that has student names, majors, and home phone numbers. You may do so in one of two ways. When you use the first method, you cut the appropriate fields of the two tables, put them in separate files with the fields in the order you want to display them, paste the two tables in the correct order, and remove the tables. The following session illustrates this procedure and its result. Note that the new table is not saved as a file when the following commands are executed. If you want to save the new table in a file, use the paste table1 table2 > students_table command. The students_table contains the columns of table1 and table2 (in that order) pasted together.

