# Table 4.2 The run commands from a sample rc0.d directory.

| Command | Description |
|---|---|
| K00ANNOUNCE | Announce that the system is going down |
| K70uucp | Kill UUCP operations |
| K75cron | Kill cron |
| K80lp | Kill the line printer spooler |
| K86mmdf | Kill SCO's mmdf mailer |

# Listing 4.1 The killidle script can be used in place of SCO's idleout program on other versions of UNIX.

```
# killidle
#
# Kill any user login idle for too long

IDLEOUT=$1:20:

if [ $IDLEOUT ]
then
  IDLEOUT=20
fi

who -u |
awk '{
  name = $1;
  terminal = $2;
  idle = $5;
  pid = $7;
  if (idle != ".*") {
    split(idle, idletime, ":");
    if (idletime[2] >= IDLEOUT) {
      print "Timeout Warning: ", name, "on", terminal, "idle for", idle, "minutes (killed pid:", pid ")";
      system("kill -9 " pid);
    }
  }
}'
:" IDLEOUT=$IDLEOUT
```