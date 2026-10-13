```
150 Opening BINARY mode data connection for netlitng.tgz (28081 bytes).
226 Transfer complete.
20081 bytes received in 8.35 secs (3.3 Kbytes/sec)
ftp> bye
221 Goodbye.
#
```

The session shows that I specified the ftp server at MetaLab as the host computer I wanted to connect to and retrieve files. By convention, many system administrators create and maintain a user called ftp and a directory called ft to accommodate the distribution of information, software, and software updates.

![](bbox=[0.25, 0.48, 0.32, 0.6])

> An ftp user with a directory under the /home directory exists on your OpenLinux system. This directory (/home/ftp) is where you end up if you log in anonymously. If you log in to your computer with your username and password, you end up in your home directory.

By convention, when you use the ftp program to connect to other computers, you enter your username at the Name: prompt as anonymous, followed by a password in the form of a mail address, such as user@somewhere.com.

You can see that after I logged in, I changed the directory to the pub/Linux directory. I then changed to the apps directory and changed directory to the appliance directory. If I had known the full path to the directory I wanted, I could have specified that pathname in a single cd command, for example:

```
cd pub/Linux/apps/appliance
```

I then enabled the ftp command's binary transfer mode, retrieved the file netlitng.tgz with the get command, and then logged off and exited the ftp program with the bye command. As you can see, using the ftp command is not hard and is an easy way to retrieve files.

You can also open an anonymous ftp connection to your own computer to demonstrate how ftp works without having an Internet connection available. You can specify the hostname of your computer, which you can get with the hostname command or by using your computer's Internet Protocol address, for example:

```
# hostname
presario.localhost.localdomain
# ftp presario
Connected to presario.localhost.localdomain.
220 presario.localhost.localdomain FTP server (Version wu-2.4.2-academ
[BETA-17](1) Wed Aug 19 02:55:52 MST 1998) ready.
```