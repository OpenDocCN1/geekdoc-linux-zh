
# Table A.6
## Manipulating Files (continued)

| COMMAND | DESCRIPTION |
|---|---|
| sdiff newfile oldfile | View the differences between newfile and oldfile. |
| sdiff -s newfile oldfile | View the differences between newfile and oldfile, without showing identical lines. |
| sed | Make changes throughout a file according to command-line input or a sed script. |
| sed 's/old/new/g' file.htm > file.htm | Search through file.htm and replace every occurrence of "old" with "new". |
| sed -f script.sed file > file | Run the commands in script.sed, apply them to file, and replace file with the manipulated content. |
| split -b 500k file | Split file into 500 KB chunks. |
| sort file | uniq | Sort file and send it to uniq to eliminate duplicates. |
| sort file > sortedfile | Sort the lines in file alphabetically and present the sorted results in sortedfile. |
| sort file1 | tee sorted | mail boss@raycom.com | Sort file1 and, with tee, send it both to the file sorted and to standard output, where it gets mailed to the boss. |
| sort file1 file2 | uniq -d | Sort files and file2 together and find all the lines that are duplicated. |
| sort file1 file2 file3 > bigfile | Sort and combine the contents of file1, file2, and file3 and put the sorted output in bigfile. |
| sort -n file | Sort file numerically. |
| sort -t , +2 file | Sort on the third field in the comma-delimited file. |
| sort -t , file | Sort fields in the comma-delimited file; the character following -t (, ) indicates the delimiter. |
| spell file | Check the spelling of all words in file. Returns a list of possibly misspelled words. |
| tail -15 file | View the last 15 lines of file. |
| tail file | View the last 10 lines of file. |
| tidy file.html | Clean file.html to make it "good" HTML, and optionally also easier to read and maintain. |
| tr A-Za-z a-zA-Z < file | Change uppercase to lowercase and lowercase to uppercase in file. |
| uniq | Use with sorted files to eliminate duplicate lines. |
| wc -b file | Count the bytes in file. |
| wc file | Count the lines, words, and bytes in file. |
| wc -l file | Count the lines in file. |
| wc -w file | Count the words in file. |

# Appendix A
# Table A.7 Getting Information About the System

| Command | Description |
|---------|-------------|
| df /usr/local/src | See what file systems are mounted where, and how much space is used and available. |
| df -k /home | Find out where /usr/local/src is mounted and how much space is available on it. |
| du /home | Get information about disk usage in the current directory as well as in all subdirectories. |
| du -k | Get information about disk usage, measured in 1 KB blocks. |
| du -h | Get information about disk usage, displayed in human-readable terms. |
| file /usr/bin/pico | See out the file type of /usr/bin/pico. See a little information about them. |
| finger | See who else is logged into the system and get a little information about them. |
| finger @stc.org | Get information about user @stc.org. |
| finger ejr | Get information about user ejr on your system. |
| finger ejray@mission.com | Get information about user ejray@mission.com. |
| id | Find the numeric value of your userid and what groups (by name and numeric userid value) you belong to. |
| id otheruser | Check someone else's status to find out what groups they're in. |
| quota | Find out if you're over quota. |
| quota -v | View your current quota settings and space usage. |
| uname | Use to find out what kind of Unix system you're using. |
| uname -a | Print all system information, including the Unix system type, host name, version, and hardware. |
| uname -sr | Find both the system type and release level. |
| watch | Monitor a file or other data for changes. |
| w | Get information about other users on the system and what they're doing. |
| who | Get information about the other users on the system. |
| whoami | Find out what userid you're currently logged in as. |

# Table A.8
## Configuring Your Unix Environment

| COMMAND | DESCRIPTION |
|---|---|
| alias ourterm="longhonking + command -w -many -flags + arguments" | Create the alias ourterm to substitute for the command longhonking command -w -many -flags arguments. |
| set | Find out what environment variables are set and their current values in zsh, bash, and ksh. |
| set VARIABLE="long value" | Use in csh to set the value of VARIABLE with spaces or special characters in it. |
| set VARIABLE=value | Use in csh to set VARIABLE to value. |
| setenv | Use in csh to find out what environment variables are set and their current values. |
| setenv VARIABLE value | Use in csh to make the VARIABLE available to other scripts in the current shell. |
| VARIABLE="long value" | Use in zsh, bash, and ksh to set the value of VARIABLE with spaces or special characters in it. |
| VARIABLE=value | Use in zsh, bash, and ksh to set the VARIABLE to value. |
| export VARIABLE | Use in zsh, bash, and ksh to make the value of VARIABLE available to other scripts. |
