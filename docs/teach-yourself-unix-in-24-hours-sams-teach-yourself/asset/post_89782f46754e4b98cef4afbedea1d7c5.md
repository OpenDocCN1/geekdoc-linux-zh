
## Introduction to Command Shells

You learned earlier that vi can have default information stored in the .exrc file, the program also can read configuration information from the environment variable EXINIT. I make all my pattern searches case insensitive (that is, searching for precision will match Precision), I set the appropriate vi variable in the EXINIT. Mine is set to :set ignorecase. If you want line numbers to show up always, you could easily have your EXINIT set to :set number.

Another program that I frequently use is rn, or read Netnews. Electronic mail is the electronic equivalent of letters and magazines that you receive through the postal service, Networks is the electronic equivalent of a super bulletin board. The difference is that there are thousands of different boards, and any time a note is tacked onto any board, copies of the note go to other UNIX systems throughout the world. Now, you can see that I have three environment variables defined for the rn program: RNINIT, my personal rn configuration options; SUBLINE, indicating the format for displaying subject lines of new messages; and ORGANIZATION, indicating exactly what organization I am associated with this system. They are as shown earlier.

There are many environment variables that you can define for yourself. UNIX programs have environment variables of their own, allowing you to tailor the program's behavior to your needs and preferences. UNIX itself has a few environment variables, until you're an expert, I recommend that you stick with viewing these variables and ensuring that they have reasonable values, rather than changing them. Particularly focus on the set of variables defined in Table 14.1. If they're wrong, it could be trouble; whereas, if other environment variables are wrong, it's not going to be too much trouble.

## Task 14.5: Exploring csh Configuration Files

The C shell uses two files to configure it, and although neither of them need to be present, both can be found in your home directory: .login and .cshrc. The difference between them is subtle but very important. The .login file is read every time a C shell is started. As a result, when you log in and enter :vi, vi carries out the command by starting a new shell and then feeding the command to csh. Therefore, new csh shells started from within programs such as vi will not see key shell variables that started in :login.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_326_0.png)

## ACTION

- 1. To begin, use cat to list the contents of my .login file. Remember that any line beginning with a # is a comment and is ignored.

```bash
% cat .login
#
# @($)Revision: 62.2 $
setenv TERM vt100
stty "^H" "^U" intr "^C" eof "^D"
stty crtybs crterase      # special DMIX stuff for bs processing
# shell vars
set noclobber history=100 savehist=50 filec
# set up some global environment variables...
setenv ignorecase
# Some RN related variables...
setenv RNINIT      -hmessage -reference -hdate-r -hsender -summary
hthely -dhistr -htlines -hline -hfoillow -hnews -hkey -hresent -htreturn
hto -ht-original -hx-sun -hx-nodeoriginator -hnntp
setenv SUBLINE       "-st--%s"
setenv ORGANIZATION  "Educational Computing group, School of Education
setenv NAME "Dave Taylor"

newmail

mesg y
```

This is pretty straightforward, once you remove all the comments. Three different kinds of environmental configuration commands are: setenv, stty, and set.

The setenv command defines environment variables; indeed, you can see that all of the variables shown in the previous unit are defined in my .login file. I use stty to set specific configuration options related to my terminal (stty "set tty driver options"). I use this to ensure that ^h erase (Backspace), ^u is a convenient shortcut allowing me to kill an entire line, and ^c sends an interrupt to a running program. I indicate the end of a file (EOF) with ^d. The second line of the preceding output example indicates that the CRT is capable of backspacing and erasing characters on the display.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_327_0.png)

## Introduction to Command Shells

Here's more arcane UNIX nomenclature: CRT (as used in stty crtabs or cathode-ray tube) is the technology used in the screen of a standard terminal. Terminal is not accurate anymore, however, because the command stty crtabs also works on my LCD (liquid-crystal diode, if you must know) laptop.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_328_0.png)

Finally, the set commands are configurations for the C shell. I have told the C shell to warn me before it overwrites existing files with file redirection (noclobber), to remember the last 100 commands (history=100), and to remember 50 of those if I log out and log back in (savehist=50). I also want the C shell to try, if possible, to complete filenames for me, the file. Notice there are two types of settings: on/off options (such as noclobber and options to which I must assign a specific numeric).

The C shell also has conditional statements and a variety of other commands to indicate what commands to run. Here I'm using the if (expression) then to define a set of commands that should be used only when the shell is interactive (that is, I'm going to be able to enter commands). An example of this noninteractive shell is the vi used to create a list when I enter this within the editor. $prompt true if there is a prompt for the shell (that is, if it is interactive). not, the variable is false, and the shell jumps to the endif before resuming execution of the commands.

If it is an interactive shell, however, I create a few aliases and define some C shell configuration options, to ensure that the are always set in subshells. The umask value is set, and I then invoke prompt, which is a command alias that runs the command setprompt="$system (cwd) \ :"

> SUMMARY If you're thinking that there is a variety of ways to configure the shell, you are correct. You have an incredibly diverse set of commands in both your .login and .csh files, enabling you to customize many aspects of the C shell and the UNIX environment. You may use either the Bourne or the Korn shell, the configuration information is kept in a similar file called .profile.
