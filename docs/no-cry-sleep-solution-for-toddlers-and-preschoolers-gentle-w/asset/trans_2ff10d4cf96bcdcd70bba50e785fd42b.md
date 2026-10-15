
place. In this example, an evaluation of HOME is also used to designate the user’s home directory in the new directory’s pathname. Notice the empty entry between two colons, which specifies the working directory.

```
$ PATH=$PATH:$HOME/mybin:
$ export PATH
$ echo $PATH
/usr/bin:/usr/sbin::/home/chris/mybin
```

If you add a directory to PATH yourself while you are logged in, the directory would be added only for the duration of your login session. When you log back in, the login initialization file, .bash_profile, would again initialize your PATH with its original set of directories. The .bash_profile file is described in detail a bit later in this chapter. To add a new directory to your PATH permanently, you need to edit your .bash_profile file and find the assignment for the PATH variable. Then, you simply insert the directory, preceded by a colon, into the set of pathnames assigned to PATH.

## Specifying the BASH Environment: BASH_ENV

The BASH_ENV variable holds the name of the BASH shell initialization file to be executed whenever a BASH shell is generated. For example, when a BASH shell script is executed, the BASH_ENV variable is checked and the name of the script that it holds is executed before the shell script. The BASH_ENV variable usually holds $HOME/.bashrc. This is the .bashrc file in the user’s home directory. The .bashrc file is discussed later in this chapter. You could specify a different file if you wish, using that instead of the .bashrc file for BASH shell scripts.

## Configuring the Shell Prompt

The PS1 and PS2 variables contain the primary and secondary prompt symbols, respectively. The primary prompt symbol for the BASH shell is a dollar sign, $. You can change the prompt symbol by assigning a new set of characters to the PS1 variable. In the next example, the shell prompt is changed to the -> symbol:

```
$ PS1='->'
-> export PS1
->
```

You can change the prompt to be any set of characters, including a string, as shown in the next example:

```
$ PS1="Please enter a command: "
Please enter a command: export PS1
Please enter a command: ls
mydata /reports
Please enter a command:
```

The PS2 variable holds the secondary prompt symbol, which is used for commands that take several lines to complete. The default secondary prompt is >. The added command lines begin with the secondary prompt instead of the primary prompt. You can change the secondary prompt just as easily as the primary prompt, as shown here:

```
$ PS2="@"
```

Like the TCSH shell, the BASH shell provides you with a predefined set of codes you can use to configure your prompt. With them you can make the time, your username, or your directory pathname a part of your prompt. You can even have your prompt display the history event number of the current command you are about to enter. Each code is preceded by a \ symbol. \w represents the current working directory, \t the time, and \u your username. \! will display the next history event number. In the next example, the user adds the current working directory to the prompt:

```
$ PS1="\w $"
/home/dylan $
```

The codes must be included within a quoted string. If no quotes exist, the code characters are not evaluated and are themselves used as the prompt. PS1=\w sets the prompt to the characters \w, not the working directory. The next example incorporates both the time and the history event number with a new prompt:

```
$ PS1="\t \! ->"
```

The following table lists the codes for configuring your prompt:

| Prompt Codes | Description |
|---|---|
| \! | Current history number |
| \$ | Use $ as prompt for all users except the root user, which has the # as its prompt |
| \d | Current date |
| \a | Shell currently active |
| \t | Time of day |
| \u | Username |
| \w | Current working directory |

## Specifying Your News Server

Several shell system variables are used to set values used by network applications, such as Web browsers or newsreaders. NNTP_SERVER is used to set the value of a remote news server accessible on your network. If you are using an ISP, the ISP usually provides a news server you can access with your newsreader applications. However, you first have to provide your newsreaders with the Internet address of the news server. This is the role of the NNTP_SERVER. News servers on the Internet usually use the NNTP protocol. NNTP_SERVER should hold the address of such a news server. For many ISPs, the news server address is a domain name that begins with nntp. The following example assigns the news server address nntp.myservice.com to the NNTP_SERVER system variables. Newsreader applications automatically obtain the news server address from NNTP_SERVER. Usually, this assignment is placed in the shell initialization file, .bash_profile, so that it is automatically set each time a user logs in.

```
NNTP_SERVER=nntp.myservice.com
export NNTP_SERVER
```
