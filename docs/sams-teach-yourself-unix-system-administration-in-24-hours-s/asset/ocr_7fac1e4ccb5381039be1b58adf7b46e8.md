you can more easily manage access for these admins. If you have three UID 0 admins, for example, and one no longer needs access, it's considerably easier (and safer) to delete the account than to constantly be changing the root password on a system.

# Workshop

# Quiz

+   1. There are a variety of additions to the adduser command that would improve it, not the least of which is checking to see whether the specified account name already exists in the database. How would you do that?
+   2. Jump onto the Web for this question: Go to Google (www.google.com) and see if you can find a program that advertises its capability to crack encrypted password strings, or even an entire /etc/passwd file.
+   3. Throughout the last hour or two we've used basename. Use the man system to ascertain what it actually does.

# Answers

+   1. To ensure you're not creating two accounts with the same name, immediately after the prompt for the account name grep for that account name in the password file. This can be done with
+   
+   ```bash
+    egrep "^${account}:\ " /etc/passwd
+   ```
+   though you'd want to capture the output and analyze the results in a conditional test of some sort.
+   2. I hopped onto Google and used the following search string:
+   
+   ```bash
+   +UNIX +password +cracker +download
+   ```
+   (The + forces Google to ensure that all of the words appear in each match it presents.) It returned more than 9,000 matches. More interestingly, Google also has some categorization of a subset of their enormous database, and a link to Computers -> Security -> Unix-> Exploit Software shows up on the results page, too. That proves the best area to explore, and it's distressingly easy to find a half dozen programs available for download that promise to crack Unix-encrypted passwords.

> It's worth noting that none of these programs really crack any passwords. The encryption used for Unix passwords is one-way: You can encode it, but you can't decode it. The programs work by guessing a password, encrypting it, and then comparing that encryption key to the encrypted password itself. If they match, it's "cracked" the password. A good reason for picking weird and impossible-to-guess passwords, if you ask me!