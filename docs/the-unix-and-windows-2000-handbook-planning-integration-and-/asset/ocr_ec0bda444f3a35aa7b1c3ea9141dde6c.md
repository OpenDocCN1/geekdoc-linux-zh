# RC SCRIPTS

Most work is done in the processes run in what are often called the run-level scripts (/sbin/rc2 or /sbin/rc3, etc.). These scripts work on a hierarchy of directories that is found in /etc/rc2.d and /etc/rc3.d, respectively. If you look at part of /sbin/rc2, you will see how the basic process works.

The first thing the script does is to determine the state of the system using the who -r command.

```
set `/usr/bin/who -r`
```

If the system is booting up, it sets the boot variable to yes.

```
if [ $x9 = "xS" -o $x9 = "x1" ]
```

```
then
```

```
echo 'The system is coming up. Please wait.'
```

```
BOOT=yes
```

The next test is to determine if the system is coming up to level 2, or going down. In other words, is the current state of the system higher or lower than level 2?

```
elif [ $x7 = "x2" ]
```

```
then
```

```
echo 'Changing to state 2.'
```

```
if [ -d /etc/rc2.d ]
```

```
then
```

```
for f in /etc/rc2.d/K*
```

```
{
```

```
if [ -s $(f) ]
```

```
then
```

```
case $(f) in
```

```
*.sh) . $(f) ::
```