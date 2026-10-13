# FIGURE 2-20

Commands in lftp.

```
[root@Maui ~]# lftp ftp.redhat.com
lftp ftp.redhat.com:~> help
! <shell-command>
alias [<name> <value>]
cache [<SUBCMD>]
cd [<dir>]
close [ -a ]
debug [<level>|off] [ -o <file> ]
exit [<code>|bg]
glob [OPTS] <cmd> <args>
history -w file|-r file|-c|-l [cnt]
kill all|<job_no>
lftp [OPTS] <site>
mget [OPTS] <files>
mkdir [-p] <dirs>
more <files>
mrm <files>
[re]list [<args>]
pget [OPTS] <file> [ -o <file>]
pwd
quote <cmd>
rm [-r] [-f] <files>
sache [<session_no>]
site <site_cmd>
torrent [-O <dir>] <file>
version
zcat <files>
lftp ftp.redhat.com:~> 
(commands)
bookmark [SUBCMD]
cat [-b] <files>
chmod [OPTS] mode file...
[re]cls [opts] [path/]pattern
d u [options] [dirs]
get [OPTS] <file> [ -o <file>]
help [<cmd>]
jobs [-v]
lcd [<dir>]
ls [<args>]
mirror [OPTS] [remote [local]]
module name [args]
mput [OPTS] <files>
mv <file1> <file2>
open [OPTS] <site>
put [OPTS] <file> [ -o <file>]
queue [OPTS] [<cmds>]
repeat [OPTS] [delay] [command]
rmdir [-f] <dirs>
set [OPT] <var> [<val>]
source <file>
user <user@URL> [<pass>]
wait [<jobno>]
zmore <files>
```

Almost all commands from the FTP prompt are run at the remote host, similar to a Telnet session. You can run regular shell commands from that prompt; just start the command with an exclamation point (!). This is only a subset of the commands available through lftp. If you don't remember something, the command help cmd yields a brief description of the command itself.

# CERTIFICATION SUMMARY

Given the importance of virtualization in today's computing environment, it's no surprise that Red Hat has made KVM part of the requirements associated with the RHCSA. Assuming a valid connection to appropriate repositories, installation of KVM-related packages is fairly easy. You may need to use a command like modprobe kvm to make sure appropriate modules are loaded. The Virtual Machine