# The pstree/ptree Command.

Another way to see what processes are running and what processes are child processes is to use the pstree (Linux) or ptree (Solaris) command. The pstree command displays all processes as a tree with its root being the first process that runs, called init. If a user name is specified, then that user's processes are at the root of the tree. If a process spawns more than one process of the same name, pstree visually merges the identical branches by putting them in square brackets and prefixing them with the number of times the processes are repeated. To illustrate, in Example 1.3 the http server process has started up 10 child processes. (See Appendix A for a list of pstree options.)

# EXAMPLE 1.3

```
pstree
init---4x[getty]
init---atd
  |-bash---startx---xinit+-X
  |         |-Fvwm2---FvwmButtons
  |         |-FvwmPager
  |         |-FvwmTaskBar
  |-cardmgr
  |-crond
  |-gpm
  |-httpd---10x[httpd]
  |-ifup-ppp---pppd---chat
  |-inetd
  |-kerneld
  |-kflushd
  |-klogd
  |-kswapd
  |-lpd
  |-2x[md_thread]
  |-5x[mingetty]
  |     |-nmbd
  |-nxtem---bash---tcsh---pstree
  |-portmap
  |-sendmail
  |-smbd
  |-syslogd
  |-update
  |-xclock
  |-xload
```