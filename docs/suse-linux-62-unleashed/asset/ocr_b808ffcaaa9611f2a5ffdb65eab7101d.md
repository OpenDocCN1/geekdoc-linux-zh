# Internet News
CHAPTER 12 429

reload);

```
$0 stop && $0 start || return=$rc_failed
;;
restart);
$0 stop && $0 start || return=$rc_failed
;;
status);
echo -n 'Checking for service nntpcache daemon: " 
checkproc /usr/sbin/nntpcached && echo OK !! echo No process
;;
check);
echo -n 'Cheaking active, active.times & newsgroups: " 
killproc -USR1 /usr/sbin/nntpcached
echo 'done'
;;
expire);
echo -n 'Performing an expire: " 
killproc -USR2 /usr/sbin/nntpcached
echo 'done'
;;
*)
echo "Usage: $0 {start|reload|restart|status|check|expire}"
esac
```

exit 0
You can now start nntpcache with the following command:

[root]@company /etc/nntpcache]# /sbin/init.d/nntpcache start
Also, whenever you restart your SuSE Linux server, it should automatically start on boot.
Now you have NNTPCache caching running; you can start your favorite newsreaders. If you are using a text-based newsreader such as tin or trn, set your NNTPSERVER environment variable to point to your NNTPCache machine:

$ export NNTPSERVER=nntpcache.mycompany.com
If you need more information on NNTPCache, read the documents in the /usr/doc/nntpcache-1.0.7.1-1/ directory, or visit the NNTPCache home page on the Internet.

![](bbox=[0.858, 0.266, 0.996, 0.412])