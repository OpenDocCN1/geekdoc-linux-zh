# TABLE 9.1 Common Environment Variables and Their Meanings (continued)

| Variable Name | Explanation |
| :--- | :--- |
| TERM | This variable is the name of the current terminal type. To move a text-mode cursor and display text effects for programs like text-mode editors, Linux has to know what commands the terminal supports. The TERM environment variable specifies the terminal in use. This information is combined with data from additional files to provide terminal-specific code information. TERM is normally set automatically at login, but in some cases you may need to change it. |
| DISPLAY | This variable identifies the display used by X. It's usually :0.0, which means the first (numbered from 0) display on the current computer. When you use X in a networked environment, though, this value may be preceded by the name of the computer at which you're sitting, as in machine4.luna.edu:0.0. This value is set automatically when you log in, but you may change it if necessary. You can run multiple X sessions on one computer, in which case each one gets a different DISPLAY number-for instance, :0.0 for the first session and :1.0 for the second. |
| EDITOR | Some programs launch the program pointed to by this environment variable when they need to call a text editor for you to use. Thus, changing this variable to your favorite editor can help you work in Linux. It's best to set this variable to a text-mode editor, though; GUI editors may cause problems if they're called from a program that was launched from a text-mode login. |

![](bbox=[0.14, 0.6, 0.21, 0.67])

The PATH variable sometimes includes the current directory indicator (.) so that programs in the current directory can be run. This practice poses a security risk, though, because a miscreant can create a program with the same name as some other program (such as ls) and trick another user into running it by simply leaving it in a directory the victim frequents. Even the root user may be victimized this way. For this reason, it's best to omit the current directory from the PATH variable, especially for the superuser. If it's really needed for ordinary users, put it at the end of the path.

Any given system is likely to have several other environment variables set, but these are fairly esoteric or relate to specific programs. If a program's documentation says that it needs certain environment variables set, you can set them system-wide in /etc/profile or some other suitable file, or you can set them in user configuration files, as you deem appropriate.

Although you can see the entire environment by typing env, this output can be long enough to be intimidating. If you just want to know the value of one variable, you can use the echo