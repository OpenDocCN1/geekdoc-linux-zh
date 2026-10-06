Let's make an example about this. We have two files name file_A and file_B. Let's say, we open the file_A with vim file_A command, then worked on it with pressing the "i", then we quit with esc after finishing our work, and we pass on the command mode(Or we did not process any work, we pres the i then esc to get in to command mode) Then, we want to add file_B contents to the file file_A. For this we use :r file_B command, and press "enter". After that we see the contents added to file_A

```
root@kemal:~# cat file_A
kali linux
root@kemal:~# cat file_B
commands
root@kemal:~# _
```

![](bbox=[0.166, 0.412, 0.834, 0.781])

If you pay attention to the above visual, we use :r file_B command. After the command the file contents will be as shown below:

§