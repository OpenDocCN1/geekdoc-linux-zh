```
make dep
make
make install
```

Each one of these commands will produce some output on the screen. The output for each command will all differ to some extent, but they will look similar to the output screen in Figure 2.5.

# Damage & Defense

# The "make suidinstall" Option

Kismet needs root access to configure the wireless card to use the Radio Frequency Monitor mode (known as rfmon). It also needs root access to start the packet capture. The final *make install* command can also be run as *make suidinstall*. Running this option allows Kismet to run with root user privileges from any regular user account. This is potentially a big security problem on multiuser systems, as it makes your laptop vulnerable to misuse if you have users that you do not want to have full administrative privileges. Users who have full administrative privileges, have the ability to impact the entire system, and this can be very bad for those people who are malicious or simply don't know what they are doing.

If you have no other users on the machine besides the root account and trusted accounts, you can install Kismet using *make suidinstall*. This will allow you to run Kismet from any regular user account without changing to the root account.

If you have other, unprivileged users on the computer, you should install Kismet normally, which will only allow it to be run from the root account. When you want to run Kismet from any normal account, you would then use the superuser command *su* to access the root account, and start Kismet from there. The *sudo* command may also be used. There is a slight difference between this *su* and the *sudo* commands. The *sudo* command switches you to the root user until such time as you type "exit", which will drop you to your normal user status. On the other hand, the *sudo* command allows you to execute a single command as the root user, and then instantly drop back to the normal user state, but it must be typed prior to each command. If you are going to run more than a few commands as the root user, then you probably would prefer to use the *su* command, as it will save you some time while typing.