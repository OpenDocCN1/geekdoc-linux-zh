# Question 7

There are a variety of tools available to set up a new user. Yet, they essentially perform the same functions on your Linux system. Which of the following operations is not done when you set up a new user? Assume the new username is tr.

+   - a. Copy files like .bash_profile from the /etc/skel directory
+   - b. Add the username and home directory to the /etc/passwd file
+   - c. Set up the user's shell profile in /home/tr/.bash_profile
+   - d. Assign ownership of the /home/tr directory to tr
+   - e. Assign tr to a specific group and set up the /home/tr directory for that group

Answer c is correct. When you set up a new user, you don't need to edit the .bash_profile file. Because files like .bash_profile are copied from /etc/skel to the user's home directory, answer a is incorrect. All usernames and their home directories must be a part of the /etc/passwd file; therefore, answer b is incorrect. The user tr needs to own his/her own home directory to use it; therefore, answer d is incorrect. Because you want the user tr and his/her home directory to be a part of the same group, answer e is incorrect.

# Question 8

One of your users calls you and says that his system is locked up in GIMP, an image editing program. Which of the following commands will help you find the process identifier for GIMP? Assume that user is the only one currently using GIMP on your system.

+   - a. ps aux | grep gimp
+   - b. ps | gimp
+   - c. ps | grep gimp
+   - d. top

Answer a is correct. This command lists all currently running processes and sends the output to the grep command, which looks for the text string gimp. Because the ps command alone just lists your own currently running processes, answers b and c are incorrect. Although the top command would work if GIMP is using all the CPU or memory resources on your system, that may not be the problem. Therefore, answer d is incorrect.