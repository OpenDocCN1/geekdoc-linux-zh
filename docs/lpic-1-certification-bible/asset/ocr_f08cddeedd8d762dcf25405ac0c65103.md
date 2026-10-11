**Table 12-4** (*continued*)

| Option | Function |
|:-------|:---------|
| `-s` | Displays a single line summary for each queue and subqueue. Works only with LPRng. |
| `<tclassleep time>` | Keeps displaying the spool queues but waits the specified seconds between updates. Works only with LPRng. |
| `<job id> ... all` | Displays information about specified job IDs or all. A job ID can be a user name, job identifier, job number, or a pattern. Works only with LPRng. |

# Listing the contents of print queues

To see the jobs in one or more print queues you can use the `lpq` command. To display the queue of the default printer, you would use no arguments. For example:

```
```
Printer: lp@redhat (dest lp@4.18.168.26)
Queue: no printable jobs in queue
Status: job 'jason@redhat+967' removed at 11:59:50.603
```
```

To view a nondefault printer named `hpjl`, you would use the command
`lpq` -Phpjl. The printer name is the name defined in the `/etc/printcap` file.

# Moving jobs in the print queue

After using `lpq` to see the jobs in the queue, you can use `lpc` to move print jobs around in the queue. For example, to move job numbers 30, 35, and 40 to the top of the queue for the printer named `lp` you would enter:

```
```
[root@redhat /root]# lpc topq lp 30 35 40
```
```

# Checking the status of a print queue

To check the status of a print queue you use the `lpc` command with the `status` option. For example:

```
```
debian:~# lpc status lp
lp:
queueing is enabled
printing is enabled
no entries
no daemon present
```
```