3. Use the following less command to browse through this configuration file to get an idea of what it contains. Lines beginning with # are comments.

less ~/httpd.conf

4. Press q to exit the less command.

5. Suppose you are running a Web server on a system with very little memory. You want to remove all the comments from the httpd.conf configuration file. Try this sed command:

sed '/#/d' httpd.conf | less

6. Press q to exit the less command after reviewing the output. You see that the sed command removed all of the comments, but left all of the blank lines. Though it makes the configuration file harder to read, you want to remove everything except the actual configuration parameters. Each one starts with a letter or a "<" character. Use this sed command:

sed -n '/[^A-Za-z<]/p' httpd.conf > httpd2.conf

7. To check your understanding of regular expressions and sed, describe the purpose of each character between the single quotes in the sed command in Step 6.

8. The configuration file includes statements defining icons for a Web server to use for different file types. These statements begin with the AddIcon keyword. You have moved the icons to a different directory than the default, so you need to change the /icons directory name to be /newicons for each line with the AddIcon keyword. Use this sed command to modify the previous version of the configuration file:

sed -n '/AddIcon/s/\/icons\/\/newicons/p' httpd2.conf | less

9. Press q to exit the less command after reviewing the output. What do you notice about the output of this command? Try this one:

sed '/^AddIcon/s/\/icons\/\/newicons/p' httpd2.conf | less

10. Press q to exit the less command after reviewing the output. Suppose you noticed that some of the AddIcon lines had not been changed because they were misspelled as AddIcan. This sed command changes those as well:

sed '/^AddIc[oa]n/s/\/icons\/\/newicons/p' httpd2.conf | less

11. Press q to exit the less command after reviewing the output. Web servers have configuration information that lets them work with multiple languages. This is configured in part by the AddLanguage lines, which include file extensions to define different languages (such as .ru for Russian). Suppose that the standard has changed and you need to insert the characters ".int" in front of each AddLanguage file extension. You use this sed command:

sed '/^AddLanguage/a/\. [a-z] [a-z]\.int &/p' httpd2.conf | less