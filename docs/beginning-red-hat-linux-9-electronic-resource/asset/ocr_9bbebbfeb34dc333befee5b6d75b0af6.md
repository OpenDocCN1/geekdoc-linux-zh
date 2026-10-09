# ## Running Crack

All we have to do now is run the following command to start Crack guessing at the passwords our users have set to see if there are any weak ones:

```
$ ./Crack passwords.dat
```

When you see the word *Done*, it doesn't mean that Crack has finished guessing passwords. (If passwords could be guessed that quickly, we might as well not bother with them at all!) What it does mean is that Crack has started a background process running that will spend the next hours, or even days, guessing the passwords in the `passwords.dat` file and logging any matches that it finds. Use the following command to find the background process:

```
$ ps -ef | grep crack
```

If we want to stop the background Crack process, the correct way to do this is to run *SHOME/crack/c50a/scripts/plaster*.

So how do we find out how Crack is doing? Simply run the *Reporter* script that is in the same directory as the Crack program. To find out any passwords that have been guessed, type the following command in the command line window:

```
$ ./Reporter -quiet
```

If you leave off the *-quiet* switch, then you'll get some warning messages about locked accounts, and accounts where there is no valid password. We will expect several of these to show up, as accounts used for running system services such as printing and Web serving (such as `lpd` and `apache`) will normally be configured in this way to prevent anyone from logging in as those users.

> **A final word of warning when using Crack, or any other password cracking program: Make sure that you are authorized to do this by the appropriate person, preferably in writing.**

# # Keeping Software Up to Date

As we mentioned earlier, vulnerabilities in system software that hackers may be able to exploit to gain unauthorized access to our systems are discovered and fixed quite frequently. The Red Hat Network provides an easy way for people running Red Hat systems to be informed of important software updates and to install these updates with the minimum of hassle.