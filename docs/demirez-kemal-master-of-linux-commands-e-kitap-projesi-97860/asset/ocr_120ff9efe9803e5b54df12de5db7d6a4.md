# 278 | Master of Linux Commands

```
root@kemal:/var/log# file btmp
btmp: dBase III DBT, version number 0, next free block index 7
root@kemal:/var/log# strings btmp
root
uuARVeY
guest
root@kemal:/var/log# _
```

# Lastlog

See the addresses when users open sessions we can use lastlog command. Of course, those users could be people who use the system services. That shows the information about the users run the services and adres information. For any user’s information last -u <user_name> command can be used.

```
root@kemal:-# lastlog -u root
Kullanıcı adı Kimden Sonucu
root Port **Hiç giriş yapmadı**
root@kemal:-# _
```

# Utmp-Wtmp

Our other two important files are /var/run/utmp and /var/log/wtmp files. User login informations are kept in these files. Records relating to active log files kept in utmp file and records relating to inactive sessions of the past kept in wtmp file. These two files can not be read with any text editor or the cat command because they are data file. We use string command to see the strings in them.

§