# Fg-Bg

Finally, lets talk about executing process in background. When a process is running, the terminal that the process is started, new command cannot be entered until the process completed. But if we sent the working process to the background we can use another command. There are two ways to send a command or working process to background: Use ctrl+Z to cut the process and send it to background with bg command. Or put bring back the command from the background we can use fg command.

```
root@kemal:-# tail -f
tail: uyari: standart girdiyi sonsuza dek takip etmek verimli degildir\~
[1]+ Durdu tail -f
root@kemal:-# bg
[1]+ tail &
root@kemal:-# jobs
[1]+ Durdu tail -f
root@kemal:-# fg
tail -f
~
root@kemal:-# _
```