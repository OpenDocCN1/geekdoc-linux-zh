Table 10.1, you must still edit the Makefile and uncomment the appropriate single instance of REAL_DAEMON_DIR or make an appropriate modified entry. In addition, you will subsequently need to make the following changes before you run make.

Edit the Makefile in /usr/src/tcp_wrappers (or wherever you put the source tree) and change the entry

```
CFLAGS = -O -DFACILITY=${FACILITY} $(ACCESS) $(PARANOID) $(NETGROUP) \
```

to

```
CFLAGS = -DFACILITY=${FACILITY} $(ACCESS) $(PARANOID) $(NETGROUP) \
```

that is, remove -o. Continue editing the Makefile and change the entry

```
linux:
```

```
@make REAL_DAEMON_DIR=${REAL_DAEMON_DIR} STYLE=${STYLE} \\
        LIBS = RANLIB=ranlib ARFLAGS=rv AUX_OBJ=setenv.o \\
        NETGROUP= TLI= EXTRA_CFLAGS="-DBROKEN_SO_LINGER" all
```

to

```
linux:
```

```
@make REAL_DAEMON_DIR=${REAL_DAEMON_DIR} STYLE=${STYLE} \\
        LIBS = RANLIB=ranlib ARFLAGS=rv AUX_OBJ= \\
        NETGROUP= TLI= \\
        EXTRA_CFLAGS="-DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED" all
```

The changes shown here remove setenv.o and add -DSYS_ERRLIST_DEFINED. Now you are ready to run make linux. Example 10-3 displays some of the output. The compilation is complete!

# Example 10-3 Sample make linux Output

```
# make linux
make[1]: Entering directory '/usr/src/tcp_wrappers'
cc -DFACILITY=Log_MAIL -DHOSTS_ACCESS -DPARANOID -DGNETPEERNAME_BUG \
 -DDBROKEN_FGETS -DLIBC_CALLS_STKOK -DDAEARNUMASK=022 -DREAL_DAEMON_DIR='/usr/
sbin' -DSEVERITY=Log_INFO -DRCF931_TIMEOUT=10 -DHOSTS_DENY='/etc/hosts.deny' \
 -DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED \
 -Dvsyslog=mvsySlog -DALWAS_HOSTNAME -c tcpd.c
cc -DFACILITY=Log_MAIL -DHOSTS_ACCESS -DPARANOID -DGNETPEERNAME_BUG \
 -DDBROKEN_FGETS -DLIBC_CALLS_STKOK -DDAEARNUMASK=022 -DREAL_DAEMON_DIR='/usr/
sbin' -DSEVERITY=Log_INFO -DRCF931_TIMEOUT=10 -DHOSTS_DENY='/etc/hosts.deny' \
 -DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED \
 -Dvsyslog=mvsySlog -DALWAS_HOSTNAME -c hosts_access.c
...
<lots of output snipped>
...
cc -DFACILITY=Log_MAIL -DHOSTS_ACCESS -DPARANOID -DGNETPEERNAME_BUG \
 -DDBROKEN_FGETS -DLIBC_CALLS_STKOK -DDAEARNUMASK=022 -DREAL_DAEMON_DIR='/usr/
sbin' -DSEVERITY=Log_INFO -DRCF931_TIMEOUT=10 -DHOSTS_DENY='/etc/hosts.deny' \
 -DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_ERRLIST_DEFINED \
 -Dvsyslog=mvsySlog -DALWAS_HOSTNAME -c tcpdchck.c
```