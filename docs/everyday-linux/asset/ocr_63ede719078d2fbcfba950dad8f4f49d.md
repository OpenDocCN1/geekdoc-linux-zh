Ksendfax uses your modem, of course, to send a fax. By default you need to be root to access the modem, so from an xterm or other terminal, enter the following to start ksendfax as root:

```
su -c ksendfax
```

Click “options” and “preferences” and add the following line to the “Send Fax” field. You will only need to do this one time.

```
fax send '@@Phone' '@@FName'
```

When you have added the line, click “ok.”

![](bbox=[0.15, 0.44, 0.9, 0.93])