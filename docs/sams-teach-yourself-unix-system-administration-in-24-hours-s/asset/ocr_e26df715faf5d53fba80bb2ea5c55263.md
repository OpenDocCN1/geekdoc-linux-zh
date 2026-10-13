For example, the very last line, uniquely identified as inittab line x, only applies to run state (init level) 5, and forces a respawn of the /etc/X11/prefdm program with the -nodæmon flag specified.

![](bbox=[0.22, 0.28, 0.28, 0.36])

> > The prefdm script manages login screens within the X Window System environment.

3. Let's define the most common init levels in Table 13.1 and the known init actions in Table 13.2.

# TABLE 13.1 Common init Levels

| Level | Meaning |
|---|---|
| 0 | Halt |
| 1 | Single-user mode (also called s mode on some systems) |
| 2 | Multiuser, but no remote file systems mounted; often also no networking daemons running |
| 3 | Full multiuser mode |
| 5 | Full multiuser + X11 graphics |
| 6 | Reboot |

# TABLE 13.2 Defined init Actions

| Action | Meaning |
|---|---|
| boot | Process will be executed during system bootup |
| bootwait | Like boot, but init waits for completion |
| ctrlaltdel | Process will be executed when the console keyboard device driver receives a Control-Alt-Del key sequence |
| initdefault | Specifies the default run level to boot into on system boot |
| once | Like wait, but init doesn't wait for completion |
| respawn | Process is guaranteed to be running—the system will restarted it if it dies |
| sysinit | Process will be executed during boot, but before any boot or bootwait entries |
| wait | The process will be started once (as opposed to respawn), and init will wait for it to complete |