To learn when the system was turned on who -b, to see the run level information you can use who -r command.

```
root@kemal:-# who -b
system boot 2015-09-18 10:14
root@kemal:-# who -r
acılış-seviyesi 5 2015-09-18 10:15
```

Especially using whoami command, we can easily see which identity we are working at the system at that time. Yoo may ask why we would need it. If you are working only in your system, than there is no need for sure but if you are working as a system admin on a multiple user system you may need it much.

Now lets see how to impersonate others' identity. For root user there is already not limitation so they can do any process with any users identity. However if other users want to root or another user's id to process they must know their password. To impersonate other user's id we basically use su command. How they work this is:

+   - su <user_name> switches to other user ID.
- su - <user_name> both switches to other user's id and begins to work in his/her shell.

```
root@kemal:-# su zeyep
zeyep@kemal:/root$ whoami
zeyep
zeyep@kemal:/root$ exit
root@kemal:-# _
```