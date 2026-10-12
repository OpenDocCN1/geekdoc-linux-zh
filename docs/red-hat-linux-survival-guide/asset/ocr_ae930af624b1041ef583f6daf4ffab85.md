The xdm can be run automatically after boot by changing the default run level to 5. To change the run level of your system to 5, modify the following line in the /etc/inittab file:

```
id:3:initdefault:
```

To change the default run level, simply replace the 3 with 5. And make sure that you have the following lines in the same file:

```
# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
```