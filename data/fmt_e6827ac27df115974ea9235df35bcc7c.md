
# Task 2:

In previous labs, you've used `ss` to list open ports. However, there are other approaches.

Install the `nmap` port scanner: `sudo apt install nmap`

Now run a standard `nmap` scan: `sudo nmap -v -sU -sS -p1-65535 localhost`

This command may take quite some time. It will run a standard UDP and TCP SYN scan of every port on your system. An `nmap` scan, when run from a remote host (which you did not do here), is a great way to get a look at open ports on your system from an outside perspective.

# Notes:

`fuser` and `lsof` are two tools which can be used to link files and processes, but they work differently. `fuser` is handier to answer the question of "Which process opened this file?", while `lsof` would be better to answer "Which files did this process open?"
