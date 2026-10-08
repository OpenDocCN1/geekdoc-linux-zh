# Hour 6

The last word on the line is what's important. The /etc/passwd file is one of the database files UNIX uses to track accounts. Each line in the file is called a password entry or password file. On my password entry, you can see that the login shell specified is /bin/ksh. If you try this and you don't have an identical entry, you should have /bin/sh or /bin/ksh.

+   2. If your entry is /bin/ksh, enter exactly what is shown here:
% echo "alias rm='/bin/rm -i" >> ~/.cshrc
% source ~/.cshrc
Now rm includes the -i flag each time it's used:
% touch testme
% rm testme
rm: remove testme? n

+   3. If your entry is /bin/ksh, enter exactly what is shown here, paying particular attention to the two quotation mark characters in the example:
$ echo "alias rm='/bin/rm -i" >> ~/.profile
$ ~/.profile
Now rm includes the -i flag each time it's used.

> One to pay special attention to the difference between the single quote ('\'), the double quote (""), and the backquote (\'). UNIX interprets each differently, although single and double quotes are often interchangeable. The backquotes, also known as grave accents, are more unusual and delineate commands within other commands.

![](bbox=[0.171, 0.489, 0.243, 0.545])

CAUTION

+   4. If your entry is /bin/sh, you cannot program your system to include the -i flag each time rm is. The Bourne shell, as is known, is the original Komm shell of UNIX. The Bourne shell lacks an alias feature, a feature that both the Korn shell (ksh) and the C shell (csh) include. As a result, I recommend that you change your login shell to one of these alternatives, if available.

To see what awaits you, look in the /bin directory on your machine for the specific shells:
ls -l /bin/sh /bin/ksh /bin/csh
-rwxr-xr-xr 1 root 102400 Apr 8 1991 /bin/csh*
-rwxr-xr-xr 1 root 139264 Jun 26 14:35 /bin/csh*
-rwxr-xr-xr 1 root 28672 Oct 10 1991 /bin/sh-*

Most of the examples in this book focus on the C Shell because I think it's the easiest of the three shells to use. To change your login shell to csh, you can use the csh—changing login shell—command:

```
% csh
Changing login shell for taylor.
```

![](bbox=[0.071, 0.883, 0.143, 0.943])

6

124