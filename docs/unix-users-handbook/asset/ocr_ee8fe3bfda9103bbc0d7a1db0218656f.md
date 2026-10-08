```
134 history -n
133 history
132 history 0
131 history
130 more .profile
129 env | grep HIS
128 env
127 exit
126 env | grep HIS
125 more .profile
124 history 1
123 env | more
122 env
121 inv
120 history 1
119 alias
118 history 200
117 history 128 | more
116 history 128
115 history
114 alias history="fc -l"
113 history
112 alias hisotry="fc -l"
111 history
110 fc -l
martyp $
```

Having access to this history list is a great feature of the Korn-Shell. You can view all the commands you have issued, including your typing errors, in any format you wish. In the next section, we start using the commands in the history list by recalling them.

# Re-executing Commands with r

You can reissue a command with the **r** command. To reissue the last command, you simply type **r**. In the following example, I issue the command **history 5** to view the last five commands from the history list. I then type **r** to reissue the last command, and again the last five commands are listed: