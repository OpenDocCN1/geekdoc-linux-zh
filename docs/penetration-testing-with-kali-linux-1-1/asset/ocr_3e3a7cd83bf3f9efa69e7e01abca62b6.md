use **kill**, we need the PID of the process we want to send the signal to. Since we gathered Leafpad's PID in the previous step, we can proceed:

```
kali@kali:~$ kill 1397

kali@kali:~$ ps aux | grep leafpad
kali 1313 0.0 0.0 6144 888 pts/0 S+ 10:59 0:00 grep leafpad
```

![](bbox=[0.3, 0.215, 0.87, 0.23])

Because the default signal for kill is *SIGTERM* (request termination), our application has been terminated. This has been verified in Listing 64 by using **ps** after killing Leafpad.

# ### 3.6.3.1 Exercises

+   1. Find files that have changed on your Kali virtual machine within the past 7 days by running a specific command in the background.
+   2. Re-run the previous command and suspend it, once suspended, background it.
+   3. Bring the previous background job into the foreground.
+   4. Start the Firefox browser on your Kali system. Use **ps** and **grep** to identify Firefox's PID.
+   5. Terminate Firefox from the command line using its PID.

# ## 3.7 File and Command Monitoring

It is extremely valuable to know how to monitor files and commands in real-time during the course of a penetration test. Two commands that help with such tasks are *tail* and *watch*.

# ### 3.7.1 tail

The most common use of tail75 is to monitor log file entries as they are being written. For example, we may want to monitor the Apache logs to see if a web server is being contacted by a given client we are attempting to attack via a client-side exploit. This example will do just that:

```
kali@kali:~$ sudo tail -f /var/log/apache2/access.log

127.0.0.1 - - [02/Feb/2018:12:18:14 -0500] "GET / HTTP/1.1" 200 3380 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"
127.0.0.1 - - [02/Feb/2018:12:18:14 -0500] "GET /icons/openlogo-75.png HTTP/1.1" 200 6040 "http://127.0.0.1/" "Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"
127.0.0.1 - - [02/Feb/2018:12:18:15 -0500] "GET /favicon.ico HTTP/1.1" 404 500 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0"
```

![](bbox=[0.3, 0.735, 0.87, 0.75])

The **-f** option (follow) is very useful as it continuously updates the output as the target file grows. Another convenient switch is **-nX**, which outputs the last "X" number of lines, instead of the default value of 10.