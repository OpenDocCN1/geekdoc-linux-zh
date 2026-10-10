```
This is a test program 29090
Loop #1

[2]+  Stopped                 ./test2.sh
$ . /test2.sh
This is a test program 29105
Loop #1

[3]+  Stopped                 ./test2.sh
$ jobs -l
[1]   29075 Stopped              ./test2.sh
[2]-  29090 Stopped              ./test2.sh
[3]+  29105 Stopped              ./test2.sh
$ kill -9 29105
$ jobs -l
[1]-  29075 Stopped              ./test2.sh
[2]+  29090 Stopped              ./test2.sh
$
```

In Listing 26.2 we started, then stopped, three separate processes. The jobs command listing shows the three processes and their status. Note by the PID numbers that the default process (the one listed with the plus sign) is 29105, the last process started.

We then used the kill command to send a SIGKUP signal to the default process. In the next jobs listing, the job that previously had the minus sign, 29090, is now the default job.

# ## Restarting Stopped Jobs

Under Bash job control, you can restart any stopped job as either a background process or a foreground process. A foreground process takes over control of the terminal you're working on, so be careful about using that feature.

To restart a job in background mode, use the bg command along with the job number:

```
$ bg 2
[2]+ ./test2.sh &
Test 2 Loop #2 output
$ Test 2 Loop #3 output
Test 2    Loop #4 output

$ jobs
[1]+  Stopped                 ./test2.sh
[2]-  Running                 ./test2.sh &
$ Test 2 Loop #6 output
```