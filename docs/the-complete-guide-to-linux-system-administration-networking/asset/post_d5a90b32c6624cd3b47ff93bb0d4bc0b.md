
## HANDS-ON PROJECTS

### Project 5-1

In this project, you use several basic filtering commands to modify a text file. To complete this project you should have a working Linux system with a valid user account. This project should work on any version of Linux with a standard utility set.

- 1. Log in to Linux using your user name and password.
- 2. If you are using a graphical environment, open a terminal window so you have a shell prompt.
- 3. Use the following command to copy the /etc/passwd file to your home directory as a test file named data1 (we use this file because it has lines that are separated into fields):
  `cp /etc/passwd ~/data1`
- 4. Make sure you are working in your home directory by typing:
  `cd`
- 5. Use this command to look at your working file to see how it is organized and formatted:
  `less data1`
- 6. Each line in this file is divided into fields using a colon. Press q to exit the less command. Now use the cut command as shown below to extract from each line the first and seventh fields (the user name and associated default shell):
  `cut -d : -f 1,7 data1 > data2`
- 7. Review the contents of data2 using the less command as shown here:
  `less data2`
- 8. Press q to exit the less command. Convert the colon (:) character between the remaining two fields of each line of data2 to a tab character using the tr command as shown here and store the result in data3:
  `tr ":" "\t" < data2 > data3`
- 9. Use the following command to sort the lines in the data3 file into alphabetical order and store the result in data4:
  `sort data3 > data4`
- 10. You decide that you should have sorted the file in the opposite order. Reverse all the lines in the data4 file using the tac command as shown below, and store the results in data5:
  `tac data4 > data5`
- 11. Use the following command to add a line number to the beginning of each line in the data5 file and store the result in data6.
  ```
  nl data5 > data6
  ```
- 12. Use the following less command to review the results of these commands:
  ```
  less data6
  ```
- 13. Press q to exit the less command.
- 14. Starting with the data1 file you copied in Step 3, perform all of these filtering operations again on single command line using pipes as shown below, sorting the result in data_new:
  ```
  cut -d : -f 1,7 data1 | tr ":" "\t" | sort | nl | tac > data_new
  ```

![](img/43f64015de86d989e30eff5bb284fb96_255_0.png)

### Project 5-2

In this project, you practice using regular expressions and redirecting input and output in various ways. To complete this project, you need any working Linux system with a regular user account. The file location given for the sample file (linux.words) is based on Red Hat Linux and may differ in other Linux distributions, but you can use locate to find that file on most other versions of Linux.

- 1. Log in to Linux using your user name and password.
- 2. If you are using a graphical environment, open a terminal window so you have a shell prompt.
- 3. Linux uses a dictionary of about 45,000 words to check new passwords, refusing them if the newly entered password or a simple variant of it is in the dictionary. Copy this dictionary file to your home directory as a working file using the following command:
  ```
  cp /usr/share/dict/linux.words ~/words
  ```
- 7. Use the following command to find all words that begin with “w” and end with “w”. In this pattern, the period (.) matches any single character, and the * means to match the previous character zero or more times.
  ```
  grep ^w.*w$ words
  ```
- 8. Use the -c option as shown below to count how many words begin with “s”. How many are there? (This actually displays the number of lines matching the pattern; because each line of this file contains a single word, the result here also gives you the number of matching words.)
  ```
  grep -c ^s words
  ```
- 9. How many words start with either “st” or “sm”? (Use a single command to determine the answer.)
- 10. If the grep command you enter does not find a file to search listed on the command line, it tries to search STDIN. You can enter data directly at the keyboard or pipe another source of data to grep. Use the following command to send the output of the cat command as STDIN. No file name is specified for grep, so it reads the STDIN provided by cat.
  ```
  cat words | grep ^w | less
  ```
- 11. You can also specify a file to use as STDIN without using cat.
  ```
  grep w$ < words
  ```
  In this case, the command looks very similar to the command without redirection (grep w$ words), because grep tries to use a file name first, then relies on STDIN. Some programs always look to STDIN for their input, in which case you could only use the < words method to pass that data as input to the program.

### Project 5-3

In this project, you practice using the sed command. This project uses the httpd.conf configuration file, which is installed by default on most Linux systems. On Red Hat Linux and Fedora, it is located in /etc/httpd/conf, as the project describes. On other versions of Linux, you may need to find it in a different directory for Step 2. The contents of the file should work well in any case. Some aspects of Web server configuration are mentioned in the project simply to provide reasons for the text-processing operations, but you are not expected to learn these.

- 1. Log in to Linux using your user name and password and open a terminal window.
- 2. Use the following command to copy the Web server configuration file, httpd.conf, to your home directory as a working copy for this project.
  ```
  cp /etc/httpd/conf/httpd.conf ~
  ```
- 3. Use the following less command to browse through this configuration file to get an idea of what it contains. Lines beginning with # are comments.
  `less ~/httpd.conf`
- 4. Press q to exit the less command.
- 5. Suppose you are running a Web server on a system with very little memory. You want to remove all the comments from the httpd.conf configuration file. Try this sed command:
  `sed '/#/d' httpd.conf | less`
- 6. Press q to exit the less command after reviewing the output. You see that the sed command removed all of the comments, but left all of the blank lines. Though it makes the configuration file harder to read, you want to remove everything except the actual configuration parameters. Each one starts with a letter or a "<" character. Use this sed command:
  `sed -n '/[^A-Za-z<]/p' httpd.conf > httpd2.conf`
- 7. To check your understanding of regular expressions and sed, describe the purpose of each character between the single quotes in the sed command in Step 6.
- 8. The configuration file includes statements defining icons for a Web server to use for different file types. These statements begin with the AddIcon keyword. You have moved the icons to a different directory than the default, so you need to change the /icons directory name to be /newicons for each line with the AddIcon keyword. Use this sed command to modify the previous version of the configuration file:
  `sed -n '/AddIcon/s/\/icons/\/newicons/p' httpd2.conf | less`
- 9. Press q to exit the less command after reviewing the output. What do you notice about the output of this command? Try this one:
  `sed '/^AddIcon/s/\/icons/\/newicons/p' httpd2.conf | less`
- 10. Press q to exit the less command after reviewing the output. Suppose you noticed that some of the AddIcon lines had not been changed because they were misspelled as AddIcan. This sed command changes those as well:
  `sed '/^AddIc[oa]n/s/\/icons/\/newicons/p' httpd2.conf | less`
- 11. Press q to exit the less command after reviewing the output. Web servers have configuration information that lets them work with multiple languages. This is configured in part by the AddLanguage lines, which include file extensions to define different languages (such as .ru for Russian). Suppose that the standard has changed and you need to insert the characters ".int" in front of each AddLanguage file extension. You use this sed command:
  `sed '/^AddLanguage/a/\. [a-z] [a-z]\.int &/p' httpd2.conf | less`
