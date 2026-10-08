```
19 whoami
20 cd /tmp
21 cat database.log
22 cd
23 history
24 history -h
25 history -r
26 history 10
sys1 27:
```

You can see that you have a variety of ways to produce a list of commands previously issued. Table 7-1 summarizes the commands issued in this section.

# Table 7-1 Command-Line History

| Command | Description | Example |
| :--- | :--- | :--- |
| history | The history list is produced with each command numbered. | history |
| history -h | The history list is produced without line numbers. | history -h |
| history -r | The history list is produced in reverse order with each command numbered. | history -r |
| history n | The last n commands from the history list are produced with each command numbered. | history 10 |

# Re-Executing Commands from the History List

You can re-execute commands from the history list using a variety of techniques. We’ll re-execute commands from the history using the most common techniques.

You can repeat the last command with !!, the second command with !2, and the last command that started with "c" with !c. Let’s issue