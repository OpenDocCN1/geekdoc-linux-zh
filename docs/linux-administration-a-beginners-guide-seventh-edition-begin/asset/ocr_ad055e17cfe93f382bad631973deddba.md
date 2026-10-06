# CHAPTER 8 Core System Services

# 217

| Value | Description |
| --- | --- |
| respawn | The process will be restarted whenever it terminates. |
| wait | The process will be started once when the runlevel is entered, and **init** will wait for its completion. |
| once | The process will be started once when the **runlevel** is entered; however, init won't wait for termination of the process before possibly executing additional programs to run at that particular runlevel. |
| boot | The process will be executed at system boot. The **runlevels** field is ignored in this case. |
| bootwait | The process will be executed at system boot, and **init** will wait for the completion of the boot before advancing to the next process to run. |
| ondemand | The process will be executed when a specific runlevel request occurs. (These runlevels are a, b, and c.) No change in runlevel orders. |
| initdefault | Specifies the default runlevel for **init** on startup. If no default is specified, the user is prompted for a console |
| sysinit | The process will be executed during system **boot**, before any of the **boot** or **bootwait** entries. |
| powerwait | If **init** receives a signal from another process that there are problems with the power, this process will run. Before continuing, **init** will wait for this process to finish. |
| powerfail | Same as **powerwait**, except that **init** will not wait for the process to finish. |
| powerok | This process will be executed as soon as **init** is informed that the power has been restored. |
| ctrlaltldel | The process is executed when **init** receives a signal indicating that the user has pressed the CTRL-ALT-DEL key combination. Keep in mind that X Window System servers capture this key combination, so **init** may not receive this signal if the X Window System is active. |

Table 8-2 Available Options for the action Field in /etc/initabb