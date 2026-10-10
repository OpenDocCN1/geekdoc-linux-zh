Don Quixote performs the same procedure but issues all his commands on the same single command line as such:

```
$ cd ; ls -R > outfile ; exit<Enter>
```

# # Line Continuation with the Backslash

*Line continuation* is a shell feature that is useful when the options and arguments appended to a single command cause you to type past the length of a single command line. Simply type as far as you can and finish with a single backslash (\ \) followed by pressing Enter immediately. No other character can follow the backslash. The shell takes you to the next line and automatically presents you with an angle bracket (>), called the secondary prompt, which indicates that the shell is expecting more input from you:

```
$ command(s) continued_command\<Enter>
> continued_command(s)<Enter>
```

The secondary prompt does not interfere with the interpretation of the command. Do not confuse this prompt with the redirection angle bracket, which is a key you are actually required to type. See Example 7.30. You can change the secondary prompt from the angle bracket to another symbol or even to a phrase of your choice by changing the value in the `PS2` variable (we will discuss environment variables in a later chapter).

# ### Example 7.30 Using the Backslash (\) to Continue (or, Split) Commands

To compare his own telephone list file to Juana's *RFL_Tel2* file, Preston types the following:

```
# cat /home/gutieju/a/dm in/phone#RFL_Tel2 \<Enter>
> /root/RFL_et_al_Tel#<Enter>
```

# # Shell History Commands

One of the shortcomings of working from the command line is the occasional (because of inadvertent typographical errors) or even frequent (for