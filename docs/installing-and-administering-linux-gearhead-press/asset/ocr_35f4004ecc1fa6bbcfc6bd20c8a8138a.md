Start the script with the nohup command, reference it by using an explicit path, and put it in the background. Do not forget to redirect the output from sc3 and then log out.

```
```
$ nohup ./sc3 > sc3.out 2> sc3err &<Enter>
$ exit<Enter> (You will see a message telling you that you have jobs running.)
$ exit<Enter>
```
```

+   23.  Log in. Check to see whether the process is still running.

```
```
Login: username<Enter>
Password: <Enter>
$ ps a<Enter>
```
```

+   24.  When the process has finished, display the file that contains your output. (Hint: If you did not specify an output file, nohup sends the output to nohup.out.)

```
```
$ more /home/directoryname/sc3.out<Enter>
```
```

+   25.  Use the ls -R /<Enter> command to start a long-running job in the background.

```
```
$ ls -R / > outfile 2> errfile &<Enter>
```
```

Note the process ID that is provided when you begin the background process.

+   26.  If you did not record the process ID when you first started the command in the background, how would you find it?
+   After you know the process ID, kill the process. Check to be sure it was killed.

```
```
$ ps a<Enter>
$ kill PID<Enter>
```
```