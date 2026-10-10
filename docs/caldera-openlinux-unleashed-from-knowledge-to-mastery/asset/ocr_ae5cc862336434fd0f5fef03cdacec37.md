```
# verify RHS in newaliases?
O CheckAliases=False

# default messages to old style headers if no special punctuation?
# OldStyleHeaders=True

# SMTP daemon options
#O DaemonPortOptions=Port=esmt p

# privacy flags
O PrivacyOptions=authwarnings

# who (if anyone) should get extra copies of error messages
#O PostMasterCopy=Postmaster

# slope of queue-only function
#O QueueFactor=000000

# queue directory
O QueueDirectory=/var/spool/mqueue

# timeouts (many of these)
#O Timeout.initial=5m
#O Timeout.connect=5m
#O Timeout.connect=5m
#O Timeout.helo=5m
#O Timeout.mail=10m
#O Timeout.rcpt=1h
#O Timeout.datainit=5m
#O Timeout.datalock=1h
#O Timeout.datafinal=1h
#O Timeout.rset=5m
#O Timeout.quit=2m
#O Timeout.misc=2m
#O Timeout.command=1h
#O Timeout.ident=30s
#O Timeout.filopen=60s
O Timeout.queuereturn=5d
#O Timeout.queuereturn.normal=5d
#O Timeout.queuereturn.urgent=2d
#O Timeout.queuereturn.non-urgent=7d
O Timeout.queuwarn=4h
#O Timeout.queuwarn.normal=4h
#O Timeout.queuwarn.urgent=1h
#O Timeout.queuwarn.non-urgent=12h
#O Timeout.hoststatus=30m

# should we not prune routes in route-addr syntax addresses?
#O DontPruneRoutes

# queue up everything before forking?
```