```
```text
root@kali:~:# cd /etc
root@kali:/etc# cat shadow
root:$6$NSaFWsOpSQdGLXUOJ32FE3bDIAU05KkeLD9ErvmmX1xnhB/HmlL0rqSL1bePkr7RxkDY4i5dI6g/Mv1rqqTZhq05q:18066:0:99999:7:::
dakom:*$17926:0:99999:7:::
bin:*$17926:0:99999:7:::
sys:*$17926:0:99999:7:::
sync:*$17926:0:99999:7:::
games:*$17926:0:99999:7:::
man:*$17926:0:99999:7:::
lp:*$17926:0:99999:7:::
mail:*$17926:0:99999:7:::
news:*$17926:0:99999:7:::
uucp:*$17926:0:99999:7:::
proxy:*$17926:0:99999:7:::
www-data:*$17926:0:99999:7:::
backup:*$17926:0:99999:7:::
list:*$17926:0:99999:7:::
irc:*$17926:0:99999:7:::
gnats:*$17926:0:99999:7:::
nobody:*$17926:0:99999:7:::
apt:*$17926:0:99999:7:::
systmond-1msyncic:*$17926:0:99999:7:::
```
```

In this chapter we will discuss methods of cracking passwords and some tools to do so. There is no single tool or technique that will work on every password, so it’s important to think **strategically** when trying to crack passwords.

We can break down password cracking into several categories, but probably the most important distinction is **offline vs. online**. On nearly every modern system and application, passwords are stored as hashes (see Appendix A on Cryptography Basics for Hackers). This is one-way encryption. An algorithm takes the plain-text password and creates a unique indecipherable cipher (hash) of it and stores it. When you log in again, the system takes the password you enter, encrypts it again, and checks to see whether that encrypted password matches the one it has stored. Far and away the most effective method for cracking passwords is to (1) locate and grab those hash files, (2) take them offline, and (3) commit the resources to cracking them.

To see what these hashes look like, log into your Kali system as root and go to the /etc directory and display that file **shadow** with the cat command.