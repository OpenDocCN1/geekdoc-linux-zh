```
```bash
if grep -i confirm /proc/cmdline >/dev/null || [ -f \
/var/run/confirm ]; then
	 rm -f /var/run/confirm
	 CONFIRM=yes
	 echo "Entering interactive startup"
else
	 CONFIRM=
	 echo "Entering non-interactive startup"
fi
```
```

```
```bash
# Get first argument. Set new runlevel to this argument.
[ -n "$argvl" ] && runlevel="$argvl"
```
```

```
```bash
# Tell linuxconf what runlevel we are in
[ -d /var/run ] && echo "/etc/rc$runlevel.d" > \
/var/run/runlevel.dir
```
```

```
```bash
# Is there an rc directory for this new runlevel?
if [ -d /etc/rc$runlevel.d ]; then
	 # First, run the KILL scripts.
	 for i in /etc/rc$runlevel.d/K*; do
		 # Check if the script is there.
		 [ ! -f $i ] && continue
```
```

```
```bash
		 # Don't run [KS]??foo.{rpmsave,rpmorig}
```
```

```
```bash
		 [ "$${i%.rpmsave}" 1= "$${i}" ] && continue
		 [ "$${i%.rpmorig}" 1= "$${i}" ] && continue
		 [ "$${i%.rpmnew}" 1= "$${i}" ] && continue
```
```

```
```bash
		 # Check if the subsystem is already up.
		 subsys=$(i:/etc/rc$runlevel.d/K??
		 [ ! -f /var/lock/subsys/5subsys ] && \
```
```

scripts