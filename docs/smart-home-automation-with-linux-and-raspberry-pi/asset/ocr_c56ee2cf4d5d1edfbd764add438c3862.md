to the following:

```
```bash
[ -f ~/i_am_on_holiday ] || /usr/local/minerva/etc/alarm 1
```
```

The first expression checks for the existence of the given file and skips the alarm call if it exists. Because this can be any file, located anywhere, it doesn’t need to belong to the crontab owner for it to affect the task. One possible scenario would be to use Bluetooth to watch for approaching mobile devices, creating a file in a specific directory for each user (and deleting it again, when they go out of range, that is, have left the house). Once everyone was home, a cron job set to check this directory every minute could send an e-mail reminding you to leave the computer and be sociable!

For more complex timing scenarios, you can use cron to periodically run a separate script, say every minute. If you return to the “next train” script from earlier, you could gain every last possible minute at home by retrieving the first suitable train from here:

```
```bash
NEXT_TRAIN= `whattrain.php 30 35 | head -n 1`
```
```

In this scenario, a suitable train is one that leaves in 30 to 35 minutes, which gives you time to get ready. If this command produces an output, then you can use the speech synthesizer to report it:

```
```bash
if [ `echo $NEXT_TRAIN | wc -l` -ne 0 ]; then
    say default $NEXT_TRAIN
fi
```
```

The same script could be used to automatically vary the wake-up time of your alarm clock! In Chapter 7, you’ll learn how Minerva supports even more complex actions by sending a status message to different places, according to whether you are at home, at work, or on the train.

# Occasional Control with At

In addition to the periodic events, you will often want to invoke extra events, such as a reminder in ten minutes to check on the cooking. Again, Linux is prepared with the at command, such as the following:

```
```bash
echo "say default Check on dinner" | at now + 10 minutes
```
```

This syntax is necessary because, by default, at accepts the commands interactively from the command line (finishing with a Ctrl+D). Every at event goes into a queue, enabling complete recipes to be produced for multipart events.

Alas, this example works fine in its current scenario but has a fatal issue for tasks requiring finer granularity as the scheduler works only with whole minutes, meaning that a task for “now + 1 minute” actually means “at the start of the next minute,” which might be only five seconds away! So, you need to employ the “sleeping seconds” trick:

```
```bash
echo "sleep `date +%S`; say default Check on dinner" | at now + 10 minutes
```
```

It is also possible to use at to trigger events at a specific time:

```
```bash
echo "say default Time for CSI" | at 21:00
```
```

This always takes place when that time is next reached, meaning that it could be on the following day.