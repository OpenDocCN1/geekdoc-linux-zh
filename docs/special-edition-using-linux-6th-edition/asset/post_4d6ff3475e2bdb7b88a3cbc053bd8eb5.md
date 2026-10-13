
will work correctly. That means explicitly declaring any environment variables that you want your script to know about. This also prevents manipulation of your script by unethical users.

There are two rules you should always use when writing scripts:

- If you need an environment variable, declare it.
- If you call a program, call the full path to the executable (to ensure that the script can find it and to prevent cron from running a trojan horse). As an added precaution, you’ll want to write temporary files that you will subsequently read from to a protected directory, and not `/tmp`, for security reasons.

Earlier you learned how to get the contents of a variable. You did this by prefacing the variable with a $. Suppose that you have the variable `KLUDGE='this '`, and another variable `BAR='that'`, and you want to combine these two and add a word in between. If you type `echo $KLUDGEAND$BAR`, you see “that” printed on the screen. This is not what you wanted. The shell thought the first variable was KLUDGEAND, not KLUDGE. To get around this problem, use `{}` to surround the variable:

```
echo ${KLUDGE}AND${BAR}
```

This time you get the correct output:

```
this AND that
```

Another sticky issue that you run into with scripts, and particularly with those that you run non-interactively, is how to handle output. For this, you have redirectors. Normally, the system takes commands and input from stdin (the standard input), or the keyboard. This is device 0. You then see output on the screen, also known as stdout (the standard output, or device 1). But you also have a third channel. This is known as stderr (standard error, device 2). It would be nice if you never needed stderr—but no such luck.

### REDIRECTION

The system ordinarily shows stderr on the screen when you are working interactively. However, with a script that runs when no one is around, and with stdout—if any—that goes to a file, you need to deal with stderr or the system administrator will wonder why the console has error messages when he looks at it in the morning. But first, let’s cover how you’re going to deal with getting just stdin and stdout redirected.

To have the normal output from the script redirected to a file so that you can see the results later, use a redirector (`>`). If you enter `ls > direct`, you create a file called direct in the current directory, and in that file are the results of the `ls` command. If you then enter `ls -l > direct`, you overwrite the previous file direct with a new file direct that contains a long listing of the directory. But that’s not what you wanted. You wanted to append the results of the second command to the file. For that, you use `>>`. So entering `ls -l >> direct` leaves what’s already in the file intact and adds this new listing to the bottom.

I want to point out that `ls > direct` is the same as entering `ls 1> direct` because you are redirecting stdout (device 1) to the file. To include stderr (device 2) in the file so that it has somewhere to go, you can do the following:

```
ls > filename 2>&1
```

What this says is that you want to send a directory listing to filename and, by the way, any error messages are to be included with the listing. You also can send them their own separate ways, as in the following example:

```
ls > filename 2> /dev/null
```

This sends the listing to filename but dumps any error messages on the floor.

Similarly, you can redirect input, such as `cat < filename`. Input and output redirection can also be combined:

```
cat < filename > nextfile 2>&1
```

Those of you who are keeping score on this have probably noticed that you have >, >>, and <, but you don’t have <<. The doubled input redirector does have a legitimate role. Assume that you want to get a file every morning from an FTP site. Because this is repetitious, you’ll write a script. The Linux ftp client will automatically log you in if you create a .netrc file, but you need to send input to the FTP prompt to cd into a new directory (pub), to ensure you are in binary mode, to get the file, and to terminate FTP. That part of the script looks like this:

```
ftp ftp.server.com <<EOF
cd pub \n
binary \n
get file \n
bye \n
EOF
```

What you are going to do is read from the file as input to the command until you reach the EOF. The \n is a new line. So you can see that you have some very powerful allies with scripts.

### DEBUGGING

If you have trouble with your script, the best way to debug it is to enter the line set -x at the top. When the shell encounters the set -x, it will print out all the commands and their arguments until a set +x is encountered. You can surround problem areas in your script or enclose loops this way.

### CASE STUDY: SCRIPTING SUGGESTIONS

As part of furthering your knowledge in shell scripts, look at the scripts in /etc/rc.d/init.d. They will show you how a script can give a usage statement if it requires an argument (the case statements), how to test for conditions (`[` equals test, but also requires a closing `]`) to terminate the test—enter man test for details), and proper use of variables. Other scripts you’ll find on your Linux system will show you how to loop through a (sometimes previously undetermined) number of items using a for ..do .. done syntax (as in /etc/rc.d/rc.modules). Scripts can be a powerful ally. While you’re learning, feel free to borrow from scripts on your system. Also look into sed and awk, which work with lines and paragraphs of text.

To give your scripts a professional touch, the following tips are offered. Just following the first line, but before you begin declaring your environment and executing code, it’s a good idea to include a few commented lines about the script. Lines that begin with a # are not treated as commands by the script, but are ignored as comments. Here, near the top of the file, add a few things such as the name, date, and purpose of the script. Many times I’ve looked at a script and wondered who did this kludgy hack, and there at the top was my own name. I had no one to blame for this except myself, (and perhaps insufficient quantities of coffee or a lack of sleep).

I also recommend that you insert comments throughout the script. This will help you troubleshoot it later (or just figure out what you did in the first place). Script changes need to be noted and dated as well, both at the top and in the body. There’s no such thing as a script with too many comments. Finally, use variables. If you use a path or filename, for example, more than once in a script, assign it to a variable near the top of the script. That way, when you need to change something, you can change the variable, and all references will be changed—and you won’t miss one.

## CHAPTER 15: UNDERSTANDING PAM

In this chapter

- Encryption and Authentication 306
- Using PAM 307
- Troubleshooting 313

### ENCRYPTION AND AUTHENTICATION

Originally, all Linux (and UNIX) systems used /etc/passwd to hold the username/password pair needed to authenticate a user and permit access. The password was saved as a DES (Data Encryption Standard) hash to prevent anyone from reading the actual password. DES uses a 13-character field, the first two characters acting as a salt for the DES algorithm.

The salt acts as a random number passed to the encrypting algorithm. Each salt will produce a different encryption for a particular password, so even if 100 users choose the same (obviously bad) password, examining the encrypted field would not make this apparent as long as each had a different salt. (Microsoft does not use this approach, so examining the encrypted password database for Microsoft NT immediately reveals whether two or more users have the same password.)

The hashed password field permits a password of up to eight characters. The hashed field is like a scrambled egg. It can’t be unscrambled, but using the salt, a plaintext password can be scrambled in the same way and compared with the hashed field, with a match successfully authenticating the user.

> **Note**
>
> A new encryption scheme based on MD5 is slowly being introduced. This encryption scheme allows a 4-character salt and up to a 25-character password. However, weak passwords based on dictionary words can still be easily broken.

In the early days of computing, DES encryption was strong enough that the passwords were considered unbreakable, so allowing anyone to see the hash posed no problem. As time went by and computers became more powerful, a cracker permitted access to the hashed password could break into accounts with weak passwords. To prevent just anyone from gaining access to the hashed password and thereby improve the systems’ security posture, shadow passwords came about.

The shadow password system used a file readable only by root to be used as the storage place for the hashed password. This proved to be a formidable defense against crackers gaining access to the hashed passwords to run dictionary attacks against them.

However, changing to a shadowed system caused problems. For a restricted service, a service that requires username/password pair authentication, to make use of shadowed passwords, it had to be compiled to understand how to use this authentication scheme. Proprietary UNIX systems, as they changed over to shadow passwords, also included modified binaries for restricted services for their users. But Linux users suffered problems as a result of piecemeal upgrades.

At about the same time the Shadow system started becoming popular, Sun Microsystems began working on a way to permit restricted services to make use of alternative authentication systems such as biometric devices, smart cards, and other authentication schemes. They recognized the problem that restricted services would encounter having to be recompiled to include support for each different authentication method. Therefore, they came up with a
