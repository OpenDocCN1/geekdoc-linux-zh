The keylogger in Metasploit is a little different.

It’s a software keylogger. The advantage is that it can be installed remotely. The disadvantage is that it can only record keystrokes on one process at a time (conceivably, you could have multiple meterpreters, keylogging multiple processes such as MS

Word, Notepad, Chrome, and Firefox, all at the same time).

To employ our keylogger, we need to decide what process we want to capture keystrokes from and then migrate (move) the meterpreter to that process.

The first step is to enter ps at the meterpreter prompt. Just like in Linux, this will list all the processes running on the target system.

meterpreter > ps 204 | Page

![](bbox=[0.12, 0.53, 0.88, 0.85])