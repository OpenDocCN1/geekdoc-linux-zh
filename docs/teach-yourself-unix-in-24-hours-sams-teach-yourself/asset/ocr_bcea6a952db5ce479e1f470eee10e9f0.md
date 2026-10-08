The best way to avoid trouble is to develop good security habits now when you're first learning about UNIX—learn how to recognize what makes a good, secure password; pick one for your account; and keep it a secret.

If you ever need someone else use your account for a short time, remember that you can use the password command to change your password to something secure. Then, you can let that person use your account, and when he or she is done, you can change the password back to your original password.

With that in mind, log into your UNIX system now, and try changing your password. First, it is easy to see if the program warns you that it is too short or otherwise a poor choice. Then, try entering two different secrets to see if the program notices the difference. Finally, pick a good password, using the preceding guidelines and suggestions, and change your account password to be more secure.

# Task 2.4: Who Are You?

While you are logged in the system, you can learn a few more UNIX commands, including a couple that can answer a philosophical conundrum that has bothered men and women of thought for thousands of years: Who am I?

+   1. The easiest way to find out “who you are” is to enter the whoami command:
% whoami
taylor
%

Try it on your system. The command lists the account name associated with the current login.

+   2. Ninety-nine percent of the commands you type with UNIX do not change if you modify the punctuation and spacing. With whoami, however, adding spaces to transform the statement into proper English—that is, entering am i—dramatically changes the result. On my system, it gets the following:
% who am i
mentor..utech.edu.taylor ttyp4 Feb 8 14:34

This tells me quite a bit about my identity on the computer, including the name of the computer itself, my account name, where and when I logged in. Try the command on your system and see what results you get.

In this example, mentor is a hostname—name of the computer I am logged in to—and.edu is the full domain name—the address of mentor. The exclamation point (!) separates the domain name from my account name, taylor. The

![](bbox=[0.066, 0.896, 0.137, 0.966])