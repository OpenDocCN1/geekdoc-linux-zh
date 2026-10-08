the hacker can clean up the evidence in these three areas, it will be very difficult to trace them.



```
meterpreter > clearev
[*] Wiping 371 records from Application...
[*] Wiping 1344 records from System...
[*] Wiping 355 records from Security...
```

Now that you have exploited the Windows 7 system (Chapter 9) and retrieved the "goodies" such as: (1) Password hashes, (2) Microphone recordings, (3) Webcam recordings, (4) Keystrokes entered by the target system, then (5) Pivoting from the target system to the entire network.

At this stage, you need to make certain that no evidence is left behind to trace this attack back to you.

A digital forensic investigator is capable of recreating the events on a target system primarily from the log files and timestamps. This means that you need to remove all the log files or selectively remove certain log files that capture your activity. In addition, if you have accessed or modified any files, the timestamps on those files are clear evidence of tampering. Finally, if your system falls into the wrong hands, your command history can be incriminating.

Let’s see how you can minimize this evidence and cover your tracks!

**Covering Your Tracks with the Meterpreter If you were able to plant Metasploit’s meterpreter on the target system, clearing log files is relatively simple. Most of the Windows meterpreters have a built-in**