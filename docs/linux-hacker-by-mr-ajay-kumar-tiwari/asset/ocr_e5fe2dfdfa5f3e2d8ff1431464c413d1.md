# Linux Hack

Ajay Kumar Tiwari

/dev/sda1ext2 64G 44G 17G 73% /
/dev/sdb1ext2 137G 67G 70G 49% /home/user
noneproc000 -/proc
nonesysfs000 -/sys
nonedevpts000 -/dev/pts
nonetmpfs 2.0G0 2.0G 0% /dev/shm

# Hack 93. Kill Command

kill command can be used to terminate a running process. Typically this command is used to kill processes that are hanging and not responding.

Syntax: kill [options] [pids|commands]

# How to kill a hanging process?

First, identify the process id of the particular process that you would like to kill using the ps command. Once you know the process id, pass it as a parameter to the kill command. The example below shows how to kill the hanging apache httpd process. Please note that typically you should use “apachectl stop” to stop apache.

```
```
# ps aux | grep httpd
USERPID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
apache 311860.01.6 23736 17556 ?Jul26
0:40 /usr/local/apache2/bin/httpd
apache 311870.01.3 20640 14444 ?Jul26
0:37 /usr/local/apache2/bin/httpd
# kill 31186 31187
```
```