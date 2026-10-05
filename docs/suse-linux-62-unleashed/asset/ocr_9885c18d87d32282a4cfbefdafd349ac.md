# LISTING 11.1 CONTINUED

```
echo -e "$return"
fi
;
stop)
echo -n "Shutting down service http"
killproc -TERM /usr/sbin/httpd || return=$rc_failed
echo -e "$return"
;
restart)
$0 stop && sleep 3 && $0 start || return=$rc_failed
;
reload)
echo -n "Reload service http"
killproc -HUP /usr/sbin/httpd || return=$rc_failed
echo -e "$return"
;
status)
echo -n "Checking for service http: "
checkproc /usr/sbin/httpd && echo OK || echo No Error
;
*)
echo "Usage: $0 {start|stop|status|restart|reload}"
exit 1
esac
```

# Inform the caller not only verbely and set an exit status.
test '$return' = "$rc_done" || exit 1
exit 0

# Configuration File Listings

What follow are complete listings of the server configuration files for Apache 1.3.6 as installed in SuSE 6.2. If you have a different version of the server installed, or even if you have this version installed, you may notice some differences between your configuration files and the ones listed here.

Listing 11.2 shows the server configuration file.