If you want to allow queueing of print jobs, but want to start or stop the printing, use the `enable` and `disable` commands. When you disable printing, users can submit print jobs, but nothing gets printed until you enable printing again. For example, here is the command I use to disable printing on the HPLaserjetRoom210 printer:

```
`disable  HPLaserjetRoom210`
```

![](bbox=[0.15, 0.27, 0.22, 0.37])

If you're trying to print, but nothing seems to be coming out of the printer, check the printer status with the `lpc status` command and make sure that the `cupsd` scheduler is present and that both queueing and printing are enabled. To allow the queueing of print jobs, use the `accept` command. To start printing, use the `enable` command.