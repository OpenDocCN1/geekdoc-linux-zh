
always to select a file. Together, they make it practical to use long, descriptive filenames.

To use filename completion when you are entering a filename on the command line, type enough of the name to identify the file in the directory and then press TAB; tsh fills in the name and adds a SPACE, leaving the cursor so that you can enter additional arguments or press RETURN. The following example shows the user typing the command cat trig1A and pressing TAB; the system fills in the rest of the filename that begins with trig1:

```
42 $ cat trig1A → TAB cat trig1A.302488 ■
```

If two or more filenames match the prefix that you have typed, tsh cannot complete the filename without more information from you. The shell attempts to maximize the length of the prefix by adding characters, if possible, and then beeps to signify that additional input is needed to resolve the ambiguity:

```
43 $ ls h*
help.text help.trig01
44 $ cat h → TAB cat help. (BEEP)
```

You can fill in enough characters to resolve the ambiguity and then press TAB again. Alternatively, you can press CONTROL-0 and tsh presents a list of matching filenames:

```
45 $ cat help. → CONTROL-0 → cat help.
help.trig01help.text
```

Then tsh redraws the command line you have typed so that you can disambiguate the filename (and press TAB again) or finish typing the rest of the name.

# Tilde Completion

The TC Shell parses a tilde (~) appearing as the first character of a word and attempts to expand it to a user name when you enter a TAB:

```
tsh $ cd ~al → TAB cd ~alex/RETURN
tsh $ pwd
/home/alex
```

By appending a slash (/), tsh lets you know that the completed word is a directory. The slash also makes it easy to continue specifying the pathname.

# Command and Variable Completion

You can use the same mechanism that you use to complete and list filenames with command and variable names. Unless you give a full path, the shell uses the variable path in an attempt to complete a command name; the choices listed are likely to be located in different directories:

```
tcsh $ up → TAB → up(BEEP) → CONTROL-D
update update-- update_screenshot_page\update-config updatedb uptime
tcsh $ upt → TAB → uptime RETURN
9:59am up 31 days, 15:11, 7 users, load average: 0.03, 0.02, 0.00
```

If you select the autolist variable in the following example, the shell lists choices automatically when you invoke completion by pressing TAB; you do not have to press CONTROL-D:

```
tcsh $ set autolist
tcsh $ up → TAB → (BEEP)
update update-nox update_screenshot_page\update-config updatedb uptime
tcsh $ up → TAB → uptime RETURN
10:01am up 31 days, 15:14, 7 users, load average: 0.20, 0.06, 0.02
```

If you set autolist to ambiguous, the shell lists the choices when you press TAB only of the word you enter is the longest prefix of a set of commands. Otherwise, TAB causes the shell to add one or more characters to the word until it is the longest prefix; pressing TAB then lists the choices:

```
tcsh $ set autolist-ambiguous
tcsh $ echo $h → TAB (BEEP)
histfile history
tcsh $ echo $hi → TAB → echo $histtab
histfile history
tcsh $ echo $histo → TAB → echo $history RETURN
1000
```

The shell must rely on the context of the word within the input line to determine whether it is a filename, a user name, a command, or a variable name. If the word is the first on an input line, it is assumed to be a command; if it begins with the special character $, it is viewed as a variable name, and so on. In the following example the second command does not work properly, the context of the word makes it look like a filename prefix to tcsh, not a command prefix. The TC Shell supplies with an argument of updates, a non-executable file; which displays an error message:

```
tcsh $ is up$=
updates
tcsh $ which updatedb ups uptime
/usr/bin/updatedb
/usr/local/bin/ups
/usr/bin/uptime
tcsh $ which up → TAB → which updates
updates: Command not found.
```

# Editing the Command Line

The tsh command line editing feature is similar to that of bash (and zsh, you will see in the next chapter). You can use GNU emacs-style commands or vi-style commands. The default is emacs, but you can change this easily with the bindkey builtin. If you are using emacs-style bindings, you can change to the vi commands with bindkey-v. Similarly, if you are using vi-style bindings, you can change to emacs with bindkey-e. The ARROW keys are bound to the motion commands, so you can move back and forth (up and down) through your history list as well as left and right in the current command.

The bindkey builtin, without an argument, displays the current mappings between editor commands and the key sequences you can enter at the keyboard:

```
tsh $ bindkey | less
```

The less utility is handy because it lets you move and search back and forth through this long list as you read. If you are familiar with emacs or vi, you will recognize some of the commands listed by bindkey.

# Correcting Spelling

You can have tsh attempt to do spelling correction on command names, filenames, and variables (but only using emacs-style key bindings). Spelling correction can take place only at two times: before and after you press RETURN.

# Before You Press RETURN

In order for tsh to correct a word or line before you press RETURN, for this purpose you must give it an indication that what you want to do. The two functions for this are spellword and spell-line. Each of these functions is bound to a key sequence: META- and META-s, respectively. To correct the spelling of the word to the left of the cursor, enter META-s. Entering META-$ invokes the spell-line function, which attempts to correct all words on a line. The following command lines illustrate the use of these functions:

2. On many keyboards the ALT key replaces the META key: Use ALTs in place of META-s. If these substitutions do not work, try ESCAPE followed by s in place of META-s. See "Moving the Cursor by Words" on page 478 for more information on the META key.

# Correcting Spelling

```
tcsh $ ls
bigfile.gz
tcsh $ gunzipp → META-s → gunzip bigfile.gz
tcsh $ gunzip bigfile.gz → META-s → gunzip bigfile.gz
tcsh $ ecno Usfr → → → echo
```

# After You Press RETURN

The variable named correct controls what tcsh attempts to correct after you press RETURN. Set correct to cmd to correct only commands; all to correct commands, variables, and filenames; or complete to complete commands. If you do not set correct, tcsh will not correct anything:

```
tcsh $ unset correct
tcsh $ ls morning
morning
tcsh $ ecno Usfr morbing
usfr: Undefined variable.
```

```
tcsh $ set correct = cmd
tcsh $ ecno Usfr morbing
```
CORRECT>echo Usfr morbing (y|n|e|a)? usfr: Undefined variable.
```

```
tcsh $ set correct = all
tcsh $ ecno Usfr morbing
```
CORRECT>echo Usfr morning (y|n|e|a)? alex morning
```

The preceding sequence of commands first makes sure that correct is not set and establishes the presence of the file named morning. After that it gives the same command three times, with a different setting of correct: one with correct not set; one with correct set to cmd, showing the command being corrected from ecno to echo; and the last with correct set to all, showing the command, variable, and filename being corrected.

Automatic spell checking displays a special prompt that lets you enter y to accept the command line, n to reject it, e to edit it, or a to abort the command. Refer to "prompt3" on page 709 for a discussion of the special prompt used in correction.
