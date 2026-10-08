The result of running this command in the background produces a job number in brackets and the process id, or PID, as the second number. All the outputs of this command, including errors, are written to the file cprogs. The prompt was immediately returned after we issued the command, and after it completed, the output of time was sent to the screen. We could have begun issuing additional commands immediately after issuing the command in the background.

You have control over both foreground jobs and background jobs. To suspend a foreground job, you type the "control" and "z" keys simultaneously, as shown in the following example:

```
marty $ find /usr -name *.c
/usr/openwin/share/include/X11/Xaw/Template.c
/usr/openwin/share/src/dig_samples/DnD/main.c
/usr/openwin/share/src/dig_samples/DnD/owner.c
/usr/openwin/share/src/dig_samples/DnD/requestor.c
/usr/openwin/share/src/dig_samples/Tooltalk/olit_tt.c
/usr/openwin/share/src/dig_samples/Tooltalk/
tt_callbacks.c
/usr/openwin/share/src/dig_samples/Tooltalk/tt_code.c
/usr/openwin/share/src/dig_samples/ce1/ce_mapl.c
/usr/openwin/share/src/dig_samples/ce2/ce_simple.c
/usr/openwin/share/src/dig_samples/dnd_olit/oltdnd.c
/usr/openwin/share/src/dig_samples/dnd_xview1/
xview_dnd.c
/usr/openwin/share/src/dig_samples/dnd_xview2/
xview_dnd2.c
/usr/openwin/share/src/dig_samples/selection_olit/
olit_sel.c
/usr/openwin/share/src/dig_samples/tooltalk_simple/tt-
send.c
/usr/openwin/share/olit/oldials/oldials.c
/usr/openwin/share/olit/olitbook/ch10/draw.c
^Z[3] + Stopped (SIGTSTP) find /usr -name *.c
```

After ctrl-z is pressed, the find command is interrupted at the point at which you type ctrl-z. The command is suspended at this point, and you are shown the job number, in this case "3," and its status is listed as "Stopped". This command has only been suspended; it is not gone forever. You can start this process in the foreground with fg or run it in the background with bg. Using bg runs the command as if you had followed it with an "&". It is started from the point at which

![](bbox=[0.88, 0.32, 0.98, 0.41])