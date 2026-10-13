# Question 5

Which of the following commands creates the /home/mj/project/book directory? Assume /home/mj is your home directory. Your pwd is /home/jm, and neither the project nor the book directory currently exists.

+   a. mkdir -p ~/project/book
+   b. mkdir -rF /home/mj/project/book
+   c. mkdir -p project/book
+   d. mkdir -r /home/mj/project/book

Answer a is correct. The tilde (~) represents your home directory (as discussed in Chapter 7). The -p switch for mkdir creates all specified levels of directories. Because there is no -r or -F switch for the mkdir command, answers b and d are incorrect. Because you're currently in the /home/jm directory, answer c is incorrect.

# Question 6

You've set up your own shell named kash. You want to know the number of users who set up kash as their default shell. There are no other words in any of the noted files that include the string kash. Which of the following commands would give you this number?

+   a. grep kash | wc -l /etc/passwd
+   b. wc -l /etc/passwd | grep kash
+   c. grep /etc/passwd kash | wc -l
+   d. grep kash /etc/passwd | wc -l

Answer d is correct. The first term after the grep command is the search term that is used to search through standard input—in this case, the /etc/passwd file. This returns each line that includes the string kash. The output is sent to the wc -l command, which counts the number of lines. There is no search file in answer a, so it is incorrect. The number of lines in the /etc/passwd file is unrelated to the number of users with the kash shell, so answer b is incorrect. Because /etc/passwd is not a search term, answer c is incorrect.