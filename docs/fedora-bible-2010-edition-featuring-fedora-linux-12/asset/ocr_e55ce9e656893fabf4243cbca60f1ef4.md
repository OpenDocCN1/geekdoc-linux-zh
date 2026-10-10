```
echo
;;
stop)
echo -n "Shutting down quotas: "
daemon /sbin/quotaoff -a
echo
;;
restart)
$0 stop
$0 start
;;
*)
echo "Usage: quota {start|stop|restart}"
exit 1
esac
exit 0
```

The quota script, when started, first runs the quotacheck command to check all file systems for which quota checking is on. Then it turns on quota checking with the quotaon command. The line # chkconfig: - 90 90 identifies the names assigned to the startup script ($90quota or K90quota) when it is added to the individual run-level directories. When you run chkconfig --add quota in the next step, those scripts are automatically put in the correct run-level directories.

# Turn on the quota startup script

If you created a quota file, as described in the previous step, you need to make it executable and set it to start automatically when you start Fedora. To do those things, type the following as root user:

```
# chmod 755 /etc/init.d/quota
# chkconfig --add quota
# chkconfig quota on
```

At this point, links are created so that your quota script starts when Fedora boots.

# Creating quota rules

You can use the edquota command to create quota rules for a particular user or group. (Valid users and groups are listed in the /etc/passwd and /etc/group files, respectively). Here is an example of an edquota command to set quotas for a user named jake.

> NOTE: The edquota command uses the vi text editor to edit your quota files. To use a different editor, change the value of the EDITOR or VISUAL environment variable before running edquota. For example, to use the emacs editor, type the following before running edquota:
> # export EDITOR=emacs